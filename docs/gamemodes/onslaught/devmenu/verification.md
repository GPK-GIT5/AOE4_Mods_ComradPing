<!-- DEVMENU In-Game Verification — Onslaught mod -->
<!-- Policy: in-game debuggers only. No scripts are authoritative verification gates. -->
<!-- Updated: 2026-05-19 -->

## SP Verification (single-player, cheats enabled)

AREA | ACTION | EXPECTED SCARLOG TOKEN
Full self-diagnostics | `DevMenu_DiagRunAll()` in console | `[DEVMENU-DIAG]` lines; final line contains pass/fail counts
Modifier accounting | `DevMenu_DiagModifierAccount()` | `[DEVMENU-DIAG] modifier_account: applies=N removes=N net=N`
Invuln replication state | `DevMenu_DiagReplInvuln()` | `[DEVMENU-REPL] invuln pid=N val=…` per player
FoW replication state | `DevMenu_DiagReplFoW()` | `[DEVMENU-REPL] fow pid=N val=…` per player
Instant Build replication | `DevMenu_DiagReplInstBuild()` | `[DEVMENU-REPL] instant_build pid=N val=…` per player
Toggle chrome sync | Click any CHEAT toggle → check card | Card reflects new state in same frame (SP); no cross-toggle visual change
MP gate mode | `DevMenu_GetMPGateMode()` | Returns `"warn"` (default), `"block"`, or `"allow"`
Boot integrity | Load map with cheats enabled | `[DEVMENU][BOOT] integrity check …` lines in scarlog; no FAIL lines
Unit spawner table | `DevMenu_UnitSpawner_Dump()` | `[SPAWNER-DUMP]` lines listing idx → SBP name
Icon audit | `DevMenu_UnitSpawner_AuditIconCoverage()` | `[ICON_COVERAGE]` summary line at end; check fallback count

## MP Verification (2-player session, both peers must check scarlog)

SCENARIO | PRESSING PEER EXPECTED | NON-PRESSING PEER EXPECTED
Any MED-risk CHEAT action | `[DEVMENU-MPGATE] … level=MED … -> proceed` + toast appears | Same `[DEVMENU-NET]` handler log line at matching game time
Any HIGH/CRIT/UNKNOWN action | `[DEVMENU-MPGATE] … -> BLOCKED` + toast with risk label | No handler fires; no OOS
DEV probe not on safe list | `[DEVMENU-MPGATE] … -> BLOCKED` toast | No probe fires; no OOS
DEV probe on safe list | Probe output e.g. `[DEVMENU-DIAG]` | Same probe output at matching game time (read-only: identical result)
OOS check (any action) | No OOS dialog appears | No OOS dialog appears; CRCs match

To confirm lockstep parity: compare `[DEVMENU-NET]` log lines between both peers' scarlogs — matching key + matching game time = lockstep-safe.

## DiagRunAll Coverage Map

`DevMenu_DiagRunAll()` (UI/devmenu_diag.scar) covers:

PROBE | LOG PREFIX | CHECKS
API availability | `[DEVMENU-DIAG]` | Network_CallEvent, SGroup_WarpToPos, Entity_Kill, Modifier_ApplyToEntity, etc.
Invuln replication | `[DEVMENU-REPL] invuln` | Per-player gInvulnerableCheat state
FoW replication | `[DEVMENU-REPL] fow` | Per-player gFoWCheat state
Instant Build replication | `[DEVMENU-REPL] instant_build` | Per-player gInstantBuildCheat state
Modifier accountant | `[DEVMENU-DIAG] modifier_account` | Net modifier leak check
F1 — block-actions state | `[DEVMENU-DIAG] F1` | _DEVMENU_BLOCK_ACTIONS_SET table presence
F2 — block-victim notify | `[DEVMENU-DIAG] F2` | _DEVMENU_BLOCK_VICTIM_NOTIFY_LAST_TIME is table type
F3 — teleport state | `[DEVMENU-DIAG] F3` | teleport_last_pos x/y/z fields present

## Adding a New NET_ACTIONS Key (verification checklist)

1. SP: press the new CHEAT button → `[DEVMENU-NET] KEY` appears in scarlog at the sim tick
2. SP: `DevMenu_DiagRunAll()` → no new FAIL lines
3. MP: press the button → both peers show `[DEVMENU-NET] KEY` at identical game time
4. MP: no OOS dialog during or after the action
5. MP gate: confirm the new action_name is in `_DEVMENU_MP_RISK` with correct level

## Adding a New _DEVMENU_DEV_MP_SAFE Entry (verification checklist)

1. Confirm function has NO sim writes (no Entity/Squad/Player/World setters outside read-only API)
2. If sim writes exist: network-route them through `Network_CallEvent("DevMenu_NetworkDispatch", …)` first
3. SP + MP: call the function → scarlog output is identical on both peers
4. No OOS dialog
