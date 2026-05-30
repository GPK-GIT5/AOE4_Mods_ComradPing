# 2026-05-09 - CBA AI Sync Error Postmortem (Frame 41 -> 376 -> 392 -> 441)

## Status
- Resolved in validation run: no sync error for approximately 30 minutes of runtime (user-confirmed).
- Root causes identified with paired peer-log evidence.
- Determinism hardening implemented in CBA AI placement and rally paths.

## Executive Summary
This incident started as an early startup out-of-sync (OOS) at frame 41, then shifted later as fixes were applied (frame 376, then 392, then 441). The shifting frame was expected and indicated progressive elimination of earlier divergence points.

Two confirmed deterministic failures were isolated and fixed:
1. Local-only rally mutation in AI production buildings (peer-asymmetric simulation state).
2. Peer-divergent placement influence from AI_FindConstructionLocation during queued building placement.

After both fixes, the scenario ran stably for approximately 30 minutes with no OOS.

## Scope and Evidence Standard
- In scope: confirmed simulation determinism failures in CBA AI construction/production flow.
- Out of scope: unrelated balancing/content changes in the repository.
- Evidence standard used for confirmation:
  - paired peer bundles from the same match,
  - frame dump comparison for previous and first divergent frame,
  - cross-peer parity checks on HB/HB_BUILD/prod_cycle lines,
  - direct event-level comparison in warnings/scarlog around divergence window.

## Timeline of Investigation and Fixes
1. Initial symptom (startup): frame-41 OOS.
- Focus area: early AI construction bootstrap.
- Added instrumentation for placement attempts and heartbeat parity.

2. First hardening pass:
- Added invalid-position sentinel guard for construction location outputs.
- Added richer per-attempt placement diagnostics.
- Outcome: frame-41 OOS removed; divergence shifted later (frame 376).

3. Mid-game instrumentation expansion:
- Extended heartbeat horizon to cover late windows.
- Added HB_BUILD telemetry (queue/tracked/assigned/pending/free plus staging/production fields).
- Added production cycle telemetry (prod_cycle) with queue/building aggregates.
- Outcome: confirmed Lua-side parity while OOS shifted to frame 392.

4. Root cause A isolated at frame 392:
- Cross-peer evidence showed identical random stream and matching HB/HB_BUILD/prod_cycle, but differing formation group count by exactly one.
- Identified local-only rally assignment path as source of per-peer movement divergence after production spawn.
- Fix applied: replace local-only rally command path with sim-broadcast rally update on completed production buildings.
- Outcome: frame-392 failure removed; divergence shifted later (frame 441).

5. Root cause B isolated at frame 441:
- At identical t=55.00 window, queued placement coordinates diverged across peers for the same player/building pass.
- Debug attempt logs showed AI_FindConstructionLocation returning different results across peers in same logical context and influencing final placement.
- Fix applied: determinism guard disabling AI_FindConstructionLocation as gameplay decision input in placement; keep deterministic retry + clamp + Entity_CalcConstructionPlacement pipeline.
- Outcome: user verified stable runtime for approximately 30 minutes without OOS.

## Confirmed Root Causes
### RC-1: Local-only rally mutation in simulation path
- Category: deterministic state mutation error.
- Mechanism:
  - Rally for completed production buildings was updated through a local-input command path gated to local AI ownership.
  - One peer mutated simulation rally state while another did not.
  - Newly spawned units followed different rally destinations, causing movement/formation drift and CRC divergence.
- Evidence signature:
  - Random stream parity present.
  - HB/HB_BUILD/prod_cycle parity present.
  - Formation group count diverged by one at first divergent frame.
- Fix:
  - Use simulation-broadcast rally update on the production building entity group.

### RC-2: Peer-divergent AI_FindConstructionLocation influence
- Category: nondeterministic engine helper usage in gameplay decision path.
- Mechanism:
  - AI_FindConstructionLocation produced different candidate outputs on peers in the same tick/context.
  - Returned candidate was consumed into final queued building position.
  - Foundation placement diverged and propagated to simulation mismatch.
- Evidence signature:
  - First explicit cross-peer mismatch in placement_queued coordinates at same timestamp.
  - DEBUG_ATTEMPT logs showed one peer path as success with offset while other peer path was invalid/ignored.
- Fix:
  - Remove AI_FindConstructionLocation from gameplay placement decision input.
  - Preserve deterministic placement pipeline and diagnostics.

## Contributing Factors (Not Primary Root Causes)
1. Shifting OOS frame after each partial fix.
- This was a normal effect of peeling back earlier divergence points, but can be misread as regression.

2. Earlier setup-parity noise in prior bundles.
- Historical runs included lobby/setup mismatches that complicated early attribution before clean paired comparisons.

3. Insufficient late-window telemetry at start of investigation.
- Early tooling was optimized for startup failures; late-window failures required expanded heartbeat and production/build telemetry.

4. API ambiguity between local command APIs and simulation mutation APIs.
- Local-input helpers are easy to misuse in deterministic multiplayer logic without explicit policy guardrails.

## Implementation Changes Applied
1. Placement sentinel guard and attempt diagnostics.
- Area: CBA AI building placement.
- Purpose: reject invalid construction-location outputs and expose branch-level diagnostics.

2. Extended heartbeat coverage.
- Area: CBA AI state heartbeat.
- Purpose: track deterministic parity deeper into runtime windows where shifted OOS occurred.

3. Added HB_BUILD telemetry with staging/production detail.
- Area: CBA AI state/build heartbeat formatter.
- Purpose: isolate construction queue assignment/pending/staging divergence quickly.

4. Added production-cycle telemetry (prod_cycle).
- Area: CBA AI production loop.
- Purpose: compare per-player queue behavior and building queue state across peers.

5. Rally mutation fix (RC-1).
- Area: CBA AI building completion path for production structures.
- Purpose: ensure rally updates occur as synchronized simulation state, not local input only.

6. AI_Find determinism guard (RC-2).
- Area: CBA AI placement candidate resolution.
- Purpose: prevent peer-divergent helper output from altering gameplay placement decisions.

## Validation Matrix
1. Static code verification
- Relevant CBA AI files compile clean (no diagnostics in edited files).
- Confirmed no active LocalCommand_EntityPos usage in CBA AI building gameplay path.

2. Bundle-based peer validation
- Previous-frame parity verified in paired bundles before first divergent frame.
- Frame dump diff used at each stage to identify first true divergence surface.
- HB/HB_BUILD/prod_cycle parity checks used to classify Lua-side vs engine-side drift.

3. Root-cause confirmation method
- For each confirmed root cause, required direct cross-peer mismatch evidence at event level (not hypothesis-only).

4. Exit criterion
- Stable runtime without OOS for approximately 30 minutes in comparable scenario (user-confirmed).

## Assumptions and Their Validation State
1. Assumption: production queue logic was causing peer-random divergence.
- Result: not confirmed as primary cause in later bundles; telemetry remained identical across peers.

2. Assumption: movement/formation asymmetry could explain frame-392 despite random parity.
- Result: confirmed (RC-1).

3. Assumption: placement helper could still introduce peer-asymmetric coordinates in late window.
- Result: confirmed (RC-2).

## Prevention Measures
1. Determinism API policy
- Do not use LocalCommand_* APIs for simulation-affecting AI gameplay behavior.
- Restrict local-input APIs to explicit local UI/input contexts only.

2. Placement determinism policy
- Treat AI_FindConstructionLocation as advisory-only unless deterministic parity has been proven under peer comparison.
- Keep deterministic retry/clamp/calc pipeline as authoritative for gameplay placement.

3. First-divergence discipline
- Always classify by first divergent frame/event from paired peers before applying fixes.
- Avoid broad speculative edits without cross-peer proof signature.

## Monitoring Recommendations
1. Keep low-cost deterministic telemetry available behind debug flags:
- HB (global entity/resource fingerprint),
- HB_BUILD (queue/assignment/pending/staging/production),
- prod_cycle (per-player production queue summary).

2. Add a recurring parity check script/runbook for paired bundle triage:
- previous-frame CRC parity,
- first divergent frame dump diff,
- normalized peer comparison for placement_queued/build_order_issued/foundation_discovered lines.

3. Trigger alerts during debug sessions for these signatures:
- peer mismatch in placement_queued coordinates at same tick,
- formation/squad-group count drift with random parity,
- non-zero heartbeat error channels in monitored window.

## Action Items
1. Add coding guidance entry:
- Document LocalCommand_* prohibition for sim-affecting AI code in repository instructions.

2. Add deterministic regression scenario:
- Multi-peer AI build/produce stress case spanning at least 60 seconds and at least one late construction cycle wave.

3. Add repeatable triage helper:
- Scripted peer diff helper focused on first divergence extraction and key telemetry parity.

4. Keep this report as canonical reference for future OOS investigations:
- Reuse sections: timeline, root causes, contributors, fixes, validation, prevention, monitoring, action items.

## Primary Files Involved
- Gamemodes/Onslaught/assets/scar/cba_ai/building.scar
- Gamemodes/Onslaught/assets/scar/cba_ai/state.scar
- Gamemodes/Onslaught/assets/scar/cba_ai/production.scar
- Gamemodes/Onslaught/assets/scar/cba_ai/lifecycle.scar
- Gamemodes/Onslaught/assets/scar/debug/cba_debug_core.scar

## Final Outcome
The sync-error chain was resolved by removing two deterministic failure mechanisms in the AI simulation path, validated through paired-peer evidence and confirmed by an approximately 30-minute stable run with no OOS.