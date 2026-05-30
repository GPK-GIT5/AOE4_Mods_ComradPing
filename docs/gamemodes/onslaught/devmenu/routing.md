<!-- DEVMENU Action Routing & MP Gate — Onslaught mod -->
<!-- Root: Gamemodes/Onslaught/assets/scar/devmenuUI/ (abbreviated as UI/) -->
<!-- Updated: 2026-05-19 -->

## CHEAT Action Call Chain (sim-mutating)

STEP | FUNCTION | FILE | NOTES
1 | `DevMenu_Click_Cheat_N()` | devmenu.scar | UI click; reads `_DEVMENU_ENTRIES[N].action`
2 | `DevMenu_Do*()` | devmenu_actions.scar | Named handler per action
3 | `_devmenu_mp_gate(action_name)` | devmenu_mp_gate.scar:≈220 | Returns true = blocked; false = proceed
4 | `_devmenu_mp_net_action(player, KEY, ...)` | devmenu_mp_gate.scar | Serializes args; calls Network_CallEvent
5 | `Network_CallEvent("DevMenu_NetworkDispatch", msg)` | engine/network.scar | Routes through lockstep bus
6 | `_DEVMENU_NET_ACTIONS[KEY](pid, args)` | devmenu_mp_gate.scar:572 | **Sim write here — all peers, same tick**

SP path skips steps 4–5; `DevMenu_Do*` calls sim API directly after gate returns false.

## DEV Action Call Chain (read-only / allowlisted)

STEP | FUNCTION | FILE | NOTES
1 | `DevMenu_Click_Dev_N()` | devmenu.scar | UI click; reads `_DEVMENU_DEV_CATEGORIES[cat].submenu[N].action`
2 | wrapper global e.g. `DevMenu_RunDeterminismTest()` | devmenu_dev_actions.scar | Thin wrapper
3 | `_devmenu_dev_safe_call(fn_name, ...)` | devmenu_dev_actions.scar:≈65 | **Allowlist check — hard block if MP and not listed**
4 | `_DEVMENU_DEV_MP_SAFE[fn_name] == true` check | devmenu_dev_actions.scar:22 | Fail-closed; no confirm-once bypass
5 | `_G[fn_name](...)` | debug/*.scar | Executes; read-only per allowlist contract

## MP Gate Decision Matrix

`_devmenu_mp_gate(action_name)` in devmenu_mp_gate.scar:≈220.

CONDITION | SP | MP mode=warn | MP mode=block | MP mode=allow
force_allow flag set | pass | pass | pass | pass
action not in _DEVMENU_MP_RISK | pass | **BLOCK** (UNKNOWN) | **BLOCK** | pass
level = LOW | pass | log + pass | log + pass | pass
level = MED | pass | log + pass | log + pass | pass
level = HIGH/CRIT | pass | **BLOCK** | **BLOCK** | pass

Blocked actions: log `[DEVMENU-MPGATE] … -> BLOCKED` + show toast with risk level. Pass actions: log `[DEVMENU-MPGATE] … -> proceed`.

Default mode: `warn`. Change via `DevMenu_CycleMPGateMode()` or `DevMenu_SetMPGateMode("allow"|"warn"|"block")`.

## Dev Probe Gate Decision Matrix

`_devmenu_dev_safe_call(fn_name)` in devmenu_dev_actions.scar:≈65.

CONDITION | SP | MP mode=warn | MP mode=block | MP mode=allow
fn_name in _DEVMENU_DEV_MP_SAFE | pass | pass | pass | pass
fn_name NOT in safe list | pass | **BLOCK** | **BLOCK** | pass

Blocked: log `[DEVMENU-MPGATE] … -> BLOCKED` + toast. No confirm-once path exists.

## BlockNotify Flow

Context: `DEVMENU_BLOCK_ACTIONS_SET` (Block Actions DEV feature) — not a CHEAT entry.

STEP | TRIGGER | FUNCTION
1 | DEV menu button press | `DevMenu_BlockActions_SetVictim(victim_pid, blocker_pid, duration)`
2 | Network route via `Network_CallEvent("DevMenu_NetworkDispatch", "DEVMENU_BLOCK_ACTIONS_SET …")` | lockstep callback fires on all peers
3 | Victim peer: `DevMenu_BlockVictimNotify(victim_pid)` | renders block-state toast + sets `_DEVMENU_BLOCK_VICTIM_NOTIFY_LAST_TIME` table
4 | Duration expires: `DevMenu_BlockActionsExpired(pid)` | dismisses toast, resets table entry to nil

## Network Registration

All `DevMenu_NetworkDispatch` actions are registered once at boot via `Network_RegisterEvent("DevMenu_NetworkDispatch")` in devmenu.scar. `_DEVMENU_NET_ACTIONS` keys are dispatched by the `GE_BroadcastMessage` callback parsing `args[1]`.

Invariant: every key in `_DEVMENU_NET_ACTIONS` must be a callable global when `Network_Callback` fires. A nil lookup causes a fatal SCAR error on ALL peers with no recovery (KI-DEBUG-007 pattern).
