<!-- DEVMENU Data Structures — Onslaught mod -->
<!-- Root: Gamemodes/Onslaught/assets/scar/devmenuUI/ (abbreviated as UI/) -->
<!-- Updated: 2026-05-19 -->

## _DEVMENU_ENTRIES (UI/devmenu_data.scar:118)
CHEAT panel flat list. Each entry: `category label action [toggle_state_fn] [quick_panel_only] [mp_locked] [dev_only]`.

SECTION | N | KEYS
speed | 3 | SpeedDecrease, SpeedDefault, SpeedIncrease (mp_locked)
resources | 7 | DoEconomy, DoResourcesAll, DoResourcesFood, DoResourcesWood, DoResourcesGold, DoResourcesStone, DoResourcesOil
progression | 2 | DoAgeUp, DoPopCapMax
combat | 5 | DoInvulnerable (toggle), DoInvulnSelectedUnits (qp_only), DoSpawnArmy, DoSpawnArmyAtCamera (qp_only), DoSpawnPhotonMan
contextual | 4 | DoTeleportSelected (qp_only), DoConvertSelected (qp_only), DoDestroySelected (qp_only), DoBurnSelected (qp_only)
world | 4 | DoFoW (toggle), DoExploreAll, DoSheepToWolves, DoKillGaia
production | 1 | DoInstantBuild (toggle)
ui | 2 | ToggleQuickPanel (toggle), ToggleSpawnPanel (toggle)
misc | 3 | DoSwapAlarmSfx (dev_only mp_locked), DoLoseInstantly (dev_only mp_locked), DiagRun (dev_only mp_locked)

Toggle entries require `toggle_state_fn` — getter name for current state. `quick_panel_only` entries appear only in the sidebar quick panel.

## _DEVMENU_DEV_CATEGORIES (UI/devmenu_categories.scar:29)
DEV panel two-level navigation. `key` is the stable identifier; do NOT reuse across categories.

KEY | LABEL | N_ITEMS | NOTES
logging | Logging | 8 | ALL, SHARED, AI, AUTOAGE_INFO, AUTOAGE_DIAG, TRACE, KEEP_CAP, FORCE_TEAM_POSITIONS; all toggles
testing_debug | Testing & Debug | 10 | Grouped: core_validation(3), jin_onboarding(3), system_probes(4)
validation | Validation | 5 | Subset of testing_debug; direct validation runners only
data_extract | Data | 1 | DataValidation runner
stress | Stress Test Menu | 30+ | Grouped: bundles(3), foundation(5), ai_tests(2), siege_tests(2+1adv), player_ui(4), ui_pressure(3), advanced(5), battle_lag(4), session_controls(2)
ai_behavior | AI Behavior | 1 | RunAIBehavior (8-scenario)
leaver | Leaver | 3 | RunMilitaryVerify, RunLeaverTest, RunLeaverMatrix
limits_ui | Limits | 1 | RunLimitsInspect
determinism | Determinism | 3 | RunDeterminismTest, RunMPSafetyAudit, CycleMPGateMode
debugger_tools | Debugger Tools | 6 | MP probes(5) + frame timing(1); locked in active UI (consolidated under spawner_debug)
spawner_debug | Spawner Debugger | 6 | Dump, RunDebug, CancelDebug, IconAudit, DiagRunAll, DiagModifierAccount

Archived (not in active UI): `qa_runner`, `ui_prompts` — in `_DEVMENU_DEV_CATEGORIES_ARCHIVED`.

## _DEVMENU_NET_ACTIONS (UI/devmenu_mp_gate.scar:572)
Network dispatch table. All handlers run inside `GE_BroadcastMessage` callback — lockstep-safe.
`pid` = PlayerID of pressing peer (same value on all peers). `args` = space-split message tokens.

KEY | ARG_SIG | SIM_WRITE | HANDLER SUMMARY
ECONOMY | pid | Y | CheatEconomy(pid) → +1000 all resources
RESOURCES_FOOD | pid | Y | Player_AddResource(pid, RT_Food, 999999)
RESOURCES_WOOD | pid | Y | Player_AddResource(pid, RT_Wood, 999999)
RESOURCES_GOLD | pid | Y | Player_AddResource(pid, RT_Gold, 999999)
RESOURCES_STONE | pid | Y | Player_AddResource(pid, RT_Stone, 999999)
RESOURCES_OIL | pid | Y | Player_AddResource(pid, RT_Merc_Byz, 999999)
RESOURCES_ALL | pid | Y | Add 1000 each of all 5 resource types
POP_CAP_MAX | pid | Y | Player_SetPopCapOverride(pid, max)
EXPLORE_ALL | pid | Y | Game_SetMapExplored(pid)
INVULNERABLE | pid | Y | ChatCheatInvulnerable(pid) — toggles gInvulnerableCheat[pid]
INSTANT_BUILD | pid | Y | ChatCheatInstantBuildAndGather(pid) — toggles gInstantBuildCheat[pid]
FOW_TOGGLE | pid | Y | ChatCheatFOW(pid) — toggles gFoWCheat[pid]
AGE_UP | pid | Y | CBA_Auto_Age_AgeUp(player) + Player_CompleteUpgrade(pid, age_bp)
SIM_RATE | pid rate | Y | Misc_SetSimRate(rate) — rate is decimal string
KILL_GAIA | pid | Y | CheatKillAllGaia(pid)
SHEEP_WOLVES | pid | Y | CheatReplaceSheepWithWolves(pid)
LOSE_INSTANTLY | pid | Y | CheatLoseInstantly(pid)
DEVMENU_DESTROY | pid eid... | Y | Entity_Kill per eid
DEVMENU_TELEPORT | pid x y z sqid... | Y | Squad_SetPosition(sq, World_Pos(x,y,z)) per squad
DEVMENU_CONVERT | pid target_pid nsquads sqid... eid... | Y | Squad/Entity_SetPlayerOwner to target_pid
DEVMENU_BURN | pid eid... | Y | Entity_SetOnFire + on-fire-threshold modifier per entity
DEVMENU_UNBURN | pid eid... | Y | Modifier_Remove + Entity_StopFire per entity
DEVMENU_INVULN_SEL | pid dir nsquads sqid... eid... | Y | Squad/Entity_SetInvulnerableMinCap; dir=1 apply, 0 remove
DEVMENU_SPAWN_ARMY | pid | Y | SpawnCheatArmy at keep position (deterministic sim state)
DEVMENU_SPAWN_ARMY_CAM | pid x y z | Y | CheatSpawnCoreUnits at serialized camera position
DEVMENU_SPAWN_PHOTON | pid | Y | SpawnCheatPhotonMan

Note: BATTLE_LAG_START / BATTLE_LAG_STOP route through separate `GE_BroadcastMessage` channel in cba_debug_battle_lag.scar, not through `DevMenu_NetworkDispatch`.

## _DEVMENU_DEV_MP_SAFE (UI/devmenu_dev_actions.scar:22)
Allowlist for `_devmenu_dev_safe_call`. Keys outside this list are hard-blocked in MP (modes: warn, block).
Only "allow" mode bypasses. Add a key ONLY after: audit shows no sim writes + network-route any that do have them.

KEY | TYPE
Debug_FactionMapDiagnostic | probe
Debug_VerifyDynastiesData | probe
Debug_VerifyJinRuntime | probe
Debug_BlueprintAudit_Civ | probe
Debug_GetLimitsUIState | probe
Debug_ClassifyTest_All | probe
Debug_EventProbes | probe
Debug_InteractiveChecks | probe
Debug_Determinism | probe
DevMenu_RunMPSafetyAudit | probe
DevMenu_DiagReplInvuln | probe
DevMenu_DiagReplFoW | probe
DevMenu_DiagReplInstBuild | probe
DevMenu_DiagModifierAccount | probe
DevMenu_DiagRunAll | runner
Debug_StressUI | runner
Debug_StressGamemode_Automated | runner (sub-suites network-routed)
Debug_BattleLagTest | runner (network-routed via BATTLE_LAG_START)
Debug_BattleLagStop | runner (network-routed via BATTLE_LAG_STOP)
Debug_BattleLagStatus | probe
Debug_BattleLagConfig | probe

## _DEVMENU_MP_RISK (UI/devmenu_mp_gate.scar:85)
Risk classification for CHEAT actions. Used by `_devmenu_mp_gate(action_name)`.

LEVEL | GATE OUTCOME | ASSIGNED TO
LOW | log-only, proceed | teleport_camera (presentation-only)
MED | log-only, proceed | all 30+ CHEAT sim actions (all routed via lockstep dispatch)
HIGH | blocked (warn+block modes) | (none currently assigned; catch-all for unclassified)
CRIT | blocked (warn+block modes) | (none currently assigned)
UNKNOWN | blocked (warn+block modes) | any action_name not in _DEVMENU_MP_RISK table

Gate modes: `warn` (default) = log + block HIGH/CRIT/UNKNOWN, pass LOW/MED. `block` = same. `allow` = pass everything (SP-soak only).

## _devmenu.* State Fields (UI/devmenu.scar)

FIELD | TYPE | PURPOSE
is_ui_created | bool | UI fully built; prevents duplicate init
is_ui_creation_scheduled | bool | Deferred-creation guard
cheats_enabled | bool | CHEAT panel visibility gate (lobby option)
dev_menu_visible | bool | DEV panel show/hide state
dev_active_submenu_key | string | Currently open DEV category key (e.g. "testing_debug")
dev_active_section_by_cat[key] | string | Active section within a category
dev_section_expanded_by_cat[key] | bool | Section expand/collapse state
dev_pill_scroll_by_cat[key] | number | Scroll position by category
dev_submenu_sections[key] | table | Sections for category
dev_submenu_data_contexts[key] | table | XAML data context per category
cheat_panel_data_context | table | CHEAT panel XAML data context
quick_panel_data_context | table | Quick panel XAML context
quick_panel_enabled | bool | Quick panel visibility toggle
teleport_last_pos | World_Pos | Last warped position (x/y/z fields)
spawn_group_count | number 1–8 | Army spawn group count multiplier
spawn_at_camera | bool | Spawn at camera vs keep toggle
toast_visible | bool | Toast display flag
toast_message | string | Toast message text
toast_state_on | bool | Toast on/off visual state
_devmenu_modifier_apply_count | number | Modifier apply counter (global, not field)
_devmenu_modifier_remove_count | number | Modifier remove counter (global, not field)
_devmenu_burn_modifier_table | table | Per-entity burn modifier IDs for DEVMENU_UNBURN
