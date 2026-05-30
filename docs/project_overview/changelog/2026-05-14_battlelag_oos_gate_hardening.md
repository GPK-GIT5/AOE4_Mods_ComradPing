# BattleLag OOS & Gate Hardening — 2026-05-14

## Incident summary

OOS at gametick **132**, game session `233147133`, ~52 seconds in.
Two human peers: Comrad Ping (jin_dynasty, Device 1 / host) and
Comrad Alternative (malian, Device 2). Map: `cba_walls_4v4_sarena`.

## Log evidence

| Property | Value |
|---|---|
| Session ID | `de58afd` |
| Diverging frame | 132 |
| Frame 131 CRC (both peers) | `edf2a53a` — in-sync up to this point |
| Frame 132 CRC — Device 1 | `a00918de` |
| Frame 132 CRC — Device 2 | `9d923b3a` |
| Random stream seed | `-1094534581` (identical both peers) |
| Random stream index | `562` (identical both peers) |
| Network disconnect reason | `1000 — OnSyncErrorDetected` |
| Disconnect time | `21:08:59` |

Device 1 log: `C:\Users\Jordan\Documents\My Games\Age of Empires IV\LogFiles\AoE4_05_13_20h-54m-38s`
Device 2 log: `C:\Users\Jordan\Documents\_logFIles\AoE4_05_13_20h-55m-25s`

## Root cause

`Debug_BattleLagTest()` was invoked via DevMenu on Device 1 at `21:08:57`.
The harness spawned ~385 MAA squads via direct SCAR calls (`CBA_Rewards_SpawnAndMove`)
running on Device 1's local sim only. Device 2 never received these spawns.
The entity-state CRC diverged 1.3 seconds later at frame 132.

Random stream and pathfinding state were **identical** on both peers at frames 131
and 132 — confirming the divergence was purely entity-state from the local-only spawns,
not RNG drift or pathfinding.

### Why the gate did not prevent it

`_devmenu_dev_safe_call` implemented a **confirm-once** advisory pattern:
- First button press → WARN log + toast → **return** (no execution)
- Second button press → PROCEED log → **execute** (no block)

This meant any non-allowlisted probe could be run in MP with two button presses.
The scarlog confirms the exact sequence:

```
21:08:55  [DEVMENU-MPGATE] dev probe Debug_BattleLagTest not on _DEVMENU_DEV_MP_SAFE
          allowlist (multiplayer session) -> WARN (first use; may desync — run again to confirm)
21:08:57  [DEVMENU-MPGATE] dev probe Debug_BattleLagTest not on _DEVMENU_DEV_MP_SAFE
          allowlist (multiplayer session) -> PROCEED (confirmed this session, expect desync)
21:08:57  CBA DEBUG — BATTLE LAG HARNESS [spawns begin]
21:08:59  OnSyncErrorDetected
```

The gate was functioning as coded — but the two-click design made OOS trivially
reproducible from the UI and created a false impression that "confirming" was
an acceptable path rather than a policy violation.

## Secondary findings

### 1. Ottoman civ missing from `_AUTOAGE_CIV_MENUS`

24 `[AUTOAGE][WARN] unresolved menu race=ottoman` warnings fired during game 2
init (`21:08:53–21:08:57`), repeating 4× before the BattleLag test even started.
`_AUTOAGE_CIV_MENUS['ottoman']` resolves `ott_age2/3/4` and `ott_*_wonders`,
none of which exist in the engine's construction-menu registry. Ottoman was
present as an AI player in this lobby. This mirrors the known Jin gap fixed on
2026-05-11 and requires the same attrib-XML lookup treatment.

### 2. DataCRC mismatch between peers

Device 1 reported:
- Peer 0 DataCRC: `7808be93`
- Peer 1 DataCRC: `5b574458`

Device 2 reported no DataCRC mismatch. The engine did not abort on this (game
ran 52 seconds). One device had a different mod/archive fingerprint. Likely a
stale mod cache or loose-file override.

### 3. Game 1 ended via connectivity loss, not OOS

Session `233145138` (game 1, same session). Device 2 experienced a ~99.5-second
OS-level freeze at `21:06:28` (`NetworkManager::DispatchEvents` warning:
`Time between calls was 99528 ms`). Relay dropped both peers with `reasonID=2`
(connection lost). This is **not** an OOS — no `OnSyncErrorDetected`.

### 4. Siege test failures (game 1, 9/78)

Phase failures from the automated siege test during game 1:

| Phase | Failure |
|---|---|
| P1 | Ram gate stuck after entity kill (`CanConstruct=false` when should be unlocked) |
| P4 | SE upgrade does not re-unlock ram after kill |
| P6 | Jin workshop not found (workshop classification gap) |
| P7 | ST gate stuck after scaffold kill |
| P9 ×4 | Workshop misclassified as production building (counter goes to prod, not workshop) |
| P11 | Workshop count never reaches cap (`count=0 cap=2`) |

Stress tests (AdvStress_BuildingOscillation 80/80, ConcurrentThrash 13/13,
SiegeCascadeSaturation 4/4) all passed.

---

## Fix — 2026-05-14

### 1. Removed confirm-once bypass from `_devmenu_dev_safe_call`

**File:** `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_actions.scar`

- Removed `_devmenu_dev_mp_confirmed` table (confirm-once state)
- Collapsed `warn`/`block`/confirm-once branches into a single hard block
  for any mode other than `"allow"`
- Log message now reads `-> BLOCKED (audit + network-route, then add to
  _DEVMENU_DEV_MP_SAFE)` with no second-click path
- `"allow"` mode remains for verified SP-soak passes only

### 2. Tightened `_devmenu_mp_gate` for HIGH/CRIT/UNKNOWN actions

**File:** `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_mp_gate.scar`

- Changed `return mode == "block"` → `return mode ~= "allow"` for
  HIGH/CRIT/UNKNOWN risk levels
- `"warn"` mode now blocks these actions (same as `"block"`) instead of
  proceeding with a log line. Only `"allow"` passes through.
- Updated all stale comments that described "warn mode proceeds"

### 3. Network-routed `Debug_BattleLagTest` / `Debug_BattleLagStop`

**File:** `Gamemodes/Onslaught/assets/scar/debug/cba_debug_battle_lag.scar`

- Extracted harness execution to `_BL_ExecuteStart()` / `_BL_ExecuteStop()`
  (local, idempotent — duplicate-callback safe)
- `Debug_BattleLagTest()` in MP: calls
  `_devmenu_mp_net_action(player, "BATTLE_LAG_START")` which routes via
  `Command_PlayerBroadcastMessage` → `GE_BroadcastMessage` → fires
  `_BL_ExecuteStart()` on **all peers at the same lockstep sim tick**
- `Debug_BattleLagStop()` same pattern with `BATTLE_LAG_STOP`
- Registered `_DEVMENU_NET_ACTIONS.BATTLE_LAG_START/STOP` as lockstep callbacks
- Registered `_DEVMENU_MP_RISK["battle_lag_start/stop"]` at level `"MED"`

### 4. Added BattleLag functions to `_DEVMENU_DEV_MP_SAFE`

**File:** `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_actions.scar`

Added:
```lua
["Debug_BattleLagTest"]   = true,
["Debug_BattleLagStop"]   = true,
["Debug_BattleLagStatus"] = true,
["Debug_BattleLagConfig"] = true,
```

Status/Config were already read-only (no sim writes). Start/Stop are now
safe because they route through the lockstep bus.

---

## Remaining limitations / follow-up actions

| Item | Owner | Notes |
|---|---|---|
| Ottoman civ `_AUTOAGE_CIV_MENUS` gap | Follow-up | Extract ottoman construction menu IDs from attrib XMLs (same method as Jin fix on 2026-05-11). Currently warn-and-skip; no OOS risk but AutoAge silently skips menu locks for ottoman AI players. |
| DataCRC mismatch (Device 1 `7808be93` vs Device 2 `5b574458`) | Follow-up | Identify which device has extra archive/mod data. Verify both devices run identical mod list before next MP session. |
| Siege test failures (P1/P4/P6/P7/P9/P11) | Follow-up | Ram/ST gate lock after kill, Jin workshop classification, workshop cap detection. Out of scope for this fix — separate investigation needed. |
| `_BL_ExecuteStart` target resolution in MP | By design | Target position is resolved independently on each peer from deterministic sim state (`_CBA.center`, sacred beacon, player anchor). No position is serialized. If `_CBA.center` is nil and no beacon exists on some peers but not others, targets could diverge. This is acceptable for a performance harness — add `_CBA` nil guard logging if needed. |
