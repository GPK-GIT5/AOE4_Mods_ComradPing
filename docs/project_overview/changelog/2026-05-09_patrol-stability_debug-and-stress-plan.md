# Patrol Stability Debug and Stress Plan (2026-05-09)

## Purpose
Tighten detection of residual patrol ownership contention and improve confidence that sync stability holds in longer runs.

## Analyzer Script
Use the new analyzer to get consistent metrics and machine-readable output.

```powershell
pwsh -File scripts/analyze_patrol_stability.ps1 \
  -LogBundlePath "C:\Users\Jordan\Documents\My Games\Age of Empires IV\LogFiles\AoE4_05_09_14h-27m-15s" \
  -LateOverwriteMinute 5 \
  -OutputJsonPath "data/generated/stats/patrol_stability_2026-05-09.json" \
  -OutputCsvPath "data/generated/stats/patrol_overwrites_2026-05-09.csv"
```

## Primary Gates
1. PATROL_OVR should trend down and stay low.
2. dt=0 PATROL_OVR must be zero.
3. patrol_stop->maa_solo_engage PATROL_OVR must be zero.
4. No PATROL_OVR after minute 5 from first overwrite event.

## Targeted Debugging Tools
1. Transition matrix from analyzer output:
   - prev->new counts by player and dt bucket.
2. Sequence digest logs every N seconds:
   - player, owner, seq, target bucket, hold owner, hold remain.
3. Guard counters in telemetry summary:
   - hold_blocked_count
   - hold_violation_count
   - same_tick_owner_flip_count
4. Optional peer comparison:
   - run scripts/compare_peer_heartbeats.ps1 for first deterministic divergence point.

## Stress Tests
1. Solo-engage flip stress:
   - Setup conditions that frequently trigger dispatch_no_ally then rapid enemy superiority changes.
   - Goal: force or eliminate patrol_stop->maa_solo_engage dt=0 transitions.
2. Timeout-dispatch overlap stress:
   - Reduce regroup timeout and increase dispatch cadence.
   - Goal: measure maa_timeout_engage->main_dispatch overwrite pressure.
3. Long soak test:
   - 45 to 60 minute 8-AI run with fixed options and seed.
   - Goal: verify no late-session overwrite recurrence.
4. Cross-peer parity test:
   - Same scenario and options on two peers.
   - Goal: confirm heartbeat and patrol digest alignment over full run.

## Reliability Practices
1. Keep raw command logs behind a verbosity gate.
2. Always emit compact periodic summaries for easier run-to-run comparisons.
3. Store analyzer JSON output per run to enable trend plots and regression alerts.
