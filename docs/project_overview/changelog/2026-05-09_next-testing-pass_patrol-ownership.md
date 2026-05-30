# Next Testing Pass: Patrol Ownership Stability

Date: 2026-05-09
Scope: Verify patrol ownership stabilization after dispatch-hold guard in patrol issuance.

## Code Change Under Test
- File: Gamemodes/Onslaught/assets/scar/cba_ai/patrol.scar
- Change: _AI_IssuePatrolOrder now skips waypoint issuance while hold is active and current owner is main_dispatch or combat_response.
- New debug line: [AI_PLAYER][PATROL_SKIP] ... reason=hold_active owner=... remain=...s

## Run Setup
1. Keep patrol ownership capture ON.
2. Use same mod set and lobby pattern used in the 13h-48m-40s run.
3. Collect full bundle from both peers if available:
   - scarlog.*
   - warnings.*
   - network.*
   - simmessages.*
   - DataCRC000.txt

## Validation Targets
1. Overwrite reduction
- Compare PATROL_OVR count and transition mix vs prior run baseline:
  - main_dispatch -> patrol_waypoint should drop materially.
  - zero-dt overwrites should drop materially.

2. Hold effectiveness
- Confirm PATROL_SKIP appears during active dispatch/combat hold windows.
- Confirm patrol_waypoint does not immediately rewrite dispatch target during those windows.

3. Behavioral safety
- Verify no prolonged idle patrol behavior after hold expires.
- Verify MAA still transitions correctly:
  - patrol_stop -> maa_solo_engage remains possible when intended.

4. Sync-risk sanity
- Confirm no new OutOfSync/SyncError markers appear.
- Confirm network disconnect lines only occur at teardown.

## Fast Triage Commands (PowerShell)
Use in the run folder.

```powershell
$scar = 'scarlog.2026-05-09.xx-xx-xx.txt'

'TAG_COUNTS'
'PATROL_CMD=' + (Select-String $scar -Pattern '\[AI_PLAYER\]\[PATROL_CMD\]' | Measure-Object).Count
'PATROL_OVR=' + (Select-String $scar -Pattern '\[PATROL_OVR\]' | Measure-Object).Count
'PATROL_HOLD=' + (Select-String $scar -Pattern '\[PATROL_HOLD\]' | Measure-Object).Count
'PATROL_SKIP=' + (Select-String $scar -Pattern '\[PATROL_SKIP\]' | Measure-Object).Count

'OVR_TRANSITIONS'
Select-String $scar -Pattern '\[PATROL_OVR\]' | ForEach-Object {
  if($_.Line -match 'prev=(?<prev>[^ ]+) new=(?<new>[^ ]+) dt=(?<dt>[0-9.]+)s'){
    [pscustomobject]@{ prev=$matches.prev; new=$matches.new; dt=[double]$matches.dt }
  }
} | Group-Object prev,new | Sort-Object Count -Descending | Select-Object -First 12

'ZERO_DT_OVR'
Select-String $scar -Pattern '\[PATROL_OVR\].*dt=0\.00s' | Select-Object -First 20
```

## Pass/Fail Criteria
Pass if all are true:
1. PATROL_SKIP > 0 in active combat/dispatch windows.
2. main_dispatch -> patrol_waypoint overwrites reduced compared with baseline run.
3. zero-dt PATROL_OVR reduced compared with baseline run.
4. No new desync markers introduced.

Fail if any are true:
1. Patrol remains stuck or inactive after hold expiration.
2. Overwrite pattern unchanged or worse.
3. New sync-risk markers appear.
