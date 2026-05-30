# Onslaught AI Player RCA + Official Standards Gap Plan (Pre-Implementation)

Date: 2026-04-04
Scope: Runtime failures/anomalies in AI construction and patrol/rally flows; standards comparison against official SCAR examples.
Primary target: Gamemodes/Onslaught/assets/scar/gameplay/cba_ai_player.scar

## 1) Deep Root-Cause Analysis (Evidence-Driven)

### RCA-1: Secondary-zone construction can enter stale reissue loops and end in stale abandon
Severity: High

Symptoms observed:
- Repeated reissues for the same secondary-zone archery range with issue counter increasing over time.
- Eventual stale foundation abandon after 35s and team release.
- Follow-on zone drift correction and offmap placement warning.

Evidence:
- P8 repeated reissues:
  - scarlog line 3156: order archery_range issues=4 queue_age=30.0s
  - scarlog line 3296: order archery_range issues=2 queue_age=10.0s (new cycle)
  - scarlog line 3376: order archery_range issues=4 queue_age=30.0s
  - scarlog line 3403: order archery_range issues=5 queue_age=40.0s
  - scarlog line 3435: order archery_range issues=6 queue_age=50.0s
- Stale abandon:
  - scarlog line 3163: abandoned stale foundation archery_range (35.0s, 4 issues)
- Zone drift + placement failure around same sequence:
  - scarlog line 3180: secondary_zone_count corrected 2 -> 1
  - scarlog line 3181: placement failed (offmap) for archery_range

Likely underlying causes:
1. Queue-entry lifecycle can oscillate between reissue/discovery/reissue without guaranteed terminal outcome for secondary chain entries.
2. Placement candidate generation for secondary zone has insufficient robust fallback when map bounds or local geometry repeatedly reject candidates.
3. Team availability shrinks over time (P8 syncs 4 -> 3 -> 2 teams), increasing chance of delayed progression and stale timeout under load.

Code branches implicated:
- _AI_ProcessConstructionQueue: reissue/stale-abandon/blocked-retry paths.
- _AI_PlaceBuilding: 6-attempt candidate loop and offmap failure return.
- _AI_ReconcileZoneCounts: post-hoc correction confirms drift is occurring.

### RCA-2: Production queue path has race-window risk between discovery and operation
Severity: Medium

Symptoms observed:
- No crash in this run, but potential for silent no-op queue attempts when building state changes between list build and queue operation.

Code evidence:
- _AI_FindAllCompletedBuildings performs alive checks while building result list.
- _AI_ManageBuildingQueues uses returned entities but does not re-check Entity_IsAlive immediately before queue operations.

Likely underlying cause:
- Time-of-check/time-of-use window between entity collection and queue command loop.

Risk profile:
- Medium: typically caught by pcall, but can cause quiet underproduction or skewed telemetry in heavy combat/destruction windows.

### RCA-3: Patrol/rally appears deterministic in this run but still under-specifies terminal outcome accounting
Severity: Medium

Observed behavior in this run:
- Patrol cycling is stable and does not show explicit rally timeout/cancel spam.
- No evidence in this scarlog of return-to-spawn regression after waypoint change.

Evidence:
- Continuous waypoint advancement across players with valid targets, e.g. lines 3108-3113, 3136-3141, 3168-3173.
- No recurring rally_timeout/rally_cancel storms in tail segment.

Underlying systemic concern (not acute failure in this run):
- Threat/rally state transitions are event-driven but not currently tracked in a strict per-event terminal accounting model.
- This can make rare oscillation or non-engagement edge cases hard to prove absent/invariant.

### RCA-4: Team-capacity attrition under sustained gameplay is a systemic stressor
Severity: Medium

Evidence:
- P8 villager team sync reductions over time:
  - line 3155: synced 4 teams (8 villagers)
  - line 3263: synced 3 teams (6 villagers)
  - line 3345: synced 2 teams (4 villagers)

Impact:
- Lower construction throughput and greater stale timeout probability for queued entries.
- Increased sensitivity to secondary-chain stalls and reissues.

## 2) Side-by-Side Gap Mapping vs Official SCAR Examples

Official references used:
- game_data/extracted/aoe4/scar_dump/scar campaign/scenarios/cdn_challenge_missions/challenge_mission_earlyeconomy/challenge_mission_earlyeconomy_preintro.scar
- game_data/extracted/aoe4/scar_dump/scar campaign/scenarios/campaign/salisbury/sal_chp3_brokenpromise/sal_chp3_brokenpromise.scar

### Alignment (already good)
1. Construction command family alignment
- Onslaught uses LocalCommand_PlayerSquadConstructBuilding for villagers.
- Official early-economy example uses the same command for house/mill/lumber/landmark.

2. Worker-driven construction intent
- Official campaigns commonly use squad-driven Cmd_Construct and LocalCommand_PlayerSquadConstructBuilding.
- Onslaught follows worker-command approach for production buildings.

3. Error-safe wrappers
- Onslaught consistently wraps risky engine calls via pcall.

### Gaps / Deviations requiring adjustment or explicit guardrails
1. Pre-operation liveness re-validation gap
- Official style frequently validates operational assumptions directly at action points.
- Onslaught queue production path lacks final liveness re-check before queue operations.

2. Deterministic terminal outcome accounting gap for queued construction entries
- Official mission flows are typically short and scripted with explicit completion points.
- Onslaught long-running autonomous queue needs stronger invariant: every queued entry must end in exactly one terminal state (completed, abandoned_stale, abandoned_maxissue, blocked_retry_then_completed, etc.).

3. Placement robustness gap in autonomous long-run mode
- Official examples often construct at fixed markers with known-valid positions.
- Onslaught autonomous placement must survive arbitrary map geometry and should have stronger multi-stage fallback (including alternate anchor strategy), not only randomized retries in one zone context.

4. Documented deviation needed: outpost instant completion
- Onslaught intentionally uses Entity_ForceConstruct for outposts.
- This is acceptable if explicitly scoped and never generalized to production buildings.

## 3) Precise Actionable Adjustments (Draft, No Implementation Yet)

Priority order: P0 (must), P1 (should), P2 (hardening)

### P0-A: Add final entity vitality guard at every production queue operation boundary
Goal:
- Eliminate TOCTOU queue-operation risk and silent underproduction.

Scope:
- _AI_ManageBuildingQueues loop over all_buildings entities.

Change:
- Before Entity_IsProductionQueueAvailable and Entity_GetProductionQueueSize, add immediate Entity_IsAlive check and skip dead entities deterministically.

Dependencies:
- None.

Resources:
- 1 engineer, ~30-45 minutes including validation pass.

Success criteria:
- Zero dead-entity queue attempts in scarlog after change.
- No regressions in queued_total telemetry.

### P0-B: Enforce explicit terminal-state accounting for each construction queue entry
Goal:
- No silent/ambiguous queue lifecycles; every entry exits via explicit outcome.

Scope:
- _AI_ProcessConstructionQueue + telemetry counters/log schema.

Change:
- Introduce terminal outcome enum/counter increments per entry.
- Add invariant check: processed_entries == sum(outcome buckets).
- Emit concise periodic audit log when invariant fails.

Dependencies:
- None (can be done in same patch batch as P0-A).

Resources:
- 1 engineer, ~1.5-2.5 hours.

Success criteria:
- Invariant holds for full match segment.
- No queue entry persists past stale timeout without terminal log.

### P1-A: Strengthen secondary-zone placement fallback strategy
Goal:
- Reduce offmap repeated failures and secondary chain stalls.

Scope:
- _AI_PlaceBuilding candidate generation and fallback anchors.

Change:
- Keep current attempt loop, but add staged fallback sequence:
  1) normal zone candidate attempts,
  2) reduced-radius attempts around zone center,
  3) anchor shift toward base-center midpoint,
  4) final abort with structured reason code.
- Log per-failure reason code (offmap, calc_fail, no_location).

Dependencies:
- None.

Resources:
- 1 engineer, ~2-3 hours including scarlog verification.

Success criteria:
- Offmap warnings reduced significantly in secondary chain scenarios.
- Fewer stale abandons caused by never-materializing foundations.

### P1-B: Add capacity-aware queue throttling based on active team count
Goal:
- Prevent over-queuing when villager teams have materially shrunk.

Scope:
- Queue admission logic (pending_limit derivation and secondary-chain queueing).

Change:
- Dynamic pending limit clamps to active team count with floor/ceiling safeguards.
- Distinguish startup burst policy from sustained-game policy.

Dependencies:
- Recommended after P0-B to retain strong accounting.

Resources:
- 1 engineer, ~1-2 hours.

Success criteria:
- Reduced reissue bursts under low-team conditions.
- Stable queue age distribution (fewer high-age entries).

### P1-C: Formalize patrol/rally terminal-state instrumentation
Goal:
- Make engagement lifecycle auditable and standards-comparable.

Scope:
- _AI_ManagePatrol, _AI_TryRallyAllies, _AI_CheckRallyStatus.

Change:
- Per-threat event lifecycle tracking with terminal labels:
  - threat_detected -> rally_wait|rally_commit|rally_timeout|threat_hold
- Add counters and periodic reconciliation summary.

Dependencies:
- None; can run parallel with construction hardening.

Resources:
- 1 engineer, ~1.5-2 hours.

Success criteria:
- Every threat event has exactly one terminal resolution in logs.
- No ambiguous repeated state churn without terminal label.

### P2-A: Document official deviations and guardrails inline
Goal:
- Preserve maintainability and avoid accidental standard drift.

Scope:
- cba_ai_player.scar comments near outpost instant-build and autonomous placement behavior.

Change:
- Add explicit “deliberate deviation” comments and non-expansion constraints.

Dependencies:
- None.

Resources:
- 1 engineer, ~20-30 minutes.

Success criteria:
- Future contributors can distinguish intentional design from accidental divergence.

## 4) Edge Cases and Exception Handling Checklist (Pre-Implementation)

1. Foundation discovered with repeated same entity id across multiple entries (possible overlap/collision risk).
2. Team shrink during active construction (entry assigned to now-understrength team).
3. Entry reaches max issues with no entity and blocked_retry enabled but new placement also invalid.
4. Secondary zone fully blocked by terrain around sacred site.
5. High combat attrition causing concurrent queue stale removals + production queue updates.
6. Patrol threat appears while squad count drops to zero mid-rally.

## 5) Implementation Readiness Gate (What must be true before coding)

1. Agreement on terminal outcome taxonomy for construction and patrol events.
2. Approval of dynamic queue throttling policy under team attrition.
3. Approval of placement fallback hierarchy and logging verbosity budget.
4. Confirmation that outpost instant-build remains intentional and scoped.

## 6) Verification Checkpoints (Post-Change Targets)

1. Construction integrity:
- terminal_outcomes == processed_queue_entries every audit window.
- stale-abandon rate decreases in secondary chain scenarios.

2. Placement robustness:
- offmap warning frequency reduced and tagged with reason code.

3. Production safety:
- zero dead-entity queue attempts logged.

4. Patrol determinism:
- 100% of threat events resolve to a terminal state label.

5. Standards conformance:
- Branch-by-branch matrix updated as aligned/justified deviation/fixed.

---
This document intentionally stops at analysis + adjustment planning, with no implementation changes applied yet.
