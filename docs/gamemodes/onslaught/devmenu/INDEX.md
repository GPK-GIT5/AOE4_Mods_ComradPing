<!-- DEVMENU Reference Index — Onslaught mod -->
<!-- Root: Gamemodes/Onslaught/assets/scar/devmenuUI/ (abbreviated as UI/) -->
<!-- Updated: 2026-05-19 -->

## Modules

FILE | ROLE | KEY TABLE(S) | LINE
devmenu.scar | root; lifecycle, boot check, UI dispatch | `_devmenu{}`, `_DEVMENU_NET_ACTIONS` (registered) | boot-check L≈80
devmenu_mp_gate.scar | MP risk classification, network dispatch, replication probes | `_DEVMENU_MP_RISK:85`, `_DEVMENU_NET_ACTIONS:572` | —
devmenu_data.scar | CHEAT menu flat list | `_DEVMENU_ENTRIES:118` | —
devmenu_categories.scar | DEV menu two-level navigation (source of truth) | `_DEVMENU_DEV_CATEGORIES:29`, `_DEVMENU_DEV_CATEGORY_INDEX` | —
devmenu_actions.scar | CHEAT action handlers (DevMenu_Do*) | — | —
devmenu_dev_actions.scar | DEV action handlers + MP-safe allowlist | `_DEVMENU_DEV_MP_SAFE:22` | —
devmenu_dev_data.scar | DEV flat fallback entries (legacy) | — | —
devmenu_xaml.scar | XAML UI builders, XML escape | — | —
devmenu_diag.scar | Diagnostic probes | `DevMenu_DiagRunAll` | —
devmenu_unit_spawner.scar | Per-civ unit spawner sub-page | `_DEVMENU_UNIT_SBP_ICON`, `_DEVMENU_ICON_CONFIRMED_PATHS` | —
devmenu_unit_spawner_debug.scar | SBP sweep debugger | — | —

## Routing Paths

**CHEAT (sim-mutating):**
1. `DevMenu_Click_Cheat_N()` — UI click handler (devmenu.scar)
2. → action string lookup in `_DEVMENU_ENTRIES`
3. → `DevMenu_Do*()` (devmenu_actions.scar) — calls `_devmenu_mp_gate(action_name)` first
4. → if MP: `_devmenu_mp_net_action(player, KEY)` → `Network_CallEvent("DevMenu_NetworkDispatch", msg)`
5. → lockstep callback `DevMenu_NetworkDispatch` fires on **all peers**
6. → `_DEVMENU_NET_ACTIONS[KEY](pid, args)` (devmenu_mp_gate.scar:572) — sim write here

**DEV (read-only / allowlisted):**
1. `DevMenu_Click_Dev_N()` — UI click handler (devmenu.scar)
2. → action string lookup in `_DEVMENU_DEV_CATEGORIES.submenu[i].action`
3. → wrapper global (devmenu_dev_actions.scar) calls `_devmenu_dev_safe_call(fn_name)`
4. → checks `_DEVMENU_DEV_MP_SAFE[fn_name]` — hard-blocks if MP and not on list
5. → `_G[fn_name](...)` executes (debug/ scar file)

## Sheet Dispatch

Question | Sheet
What entries are in the CHEAT/DEV menu? | tables.md → _DEVMENU_ENTRIES / _DEVMENU_DEV_CATEGORIES
What does each NET_ACTIONS key do / what args? | tables.md → _DEVMENU_NET_ACTIONS
Which probes are allowed in MP? | tables.md → _DEVMENU_DEV_MP_SAFE
How does the MP gate decide to block/pass? | routing.md → MP gate decision matrix
Full call chain for a CHEAT or DEV action? | routing.md → routing paths
How to verify a change in-game? | verification.md
