# Onslaught Globals Index

Auto-generated on 2026-04-02 05:31. Total top-level assignments: **647**

- **conditions**: 69 globals
- **debug**: 45 globals
- **gameplay**: 100 globals
- **helpers**: 135 globals
- **observerui**: 50 globals
- **playerui**: 137 globals
- **rewards**: 4 globals
- **root**: 92 globals
- **specials**: 5 globals
- **startconditions**: 10 globals

## conditions

### conditions/ags_annihilation.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 14 | `AGS_ANNIHILATION_MODULE` | `"AGS_Annihilation"` |
| 15 | `AGS_ANNIHILATION_OBJECTIVE` | `nil` |
| 16 | `AGS_ANNIHILATION_ACTIVE` | `true` |
| 17 | `AGS_ANNIHILATION_PLAYERS_WITH_MARKETS` | `{ }` |
| 19 | `AGS_ANNIHILATION_PRODUCTIONS_MAP` | `{` |

### conditions/ags_elimination.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 13 | `AGS_ELIMINATION_MODULE` | `"AGS_Elimination"` |
| 14 | `AGS_ELIMINATION_OBJECTIVE` | `nil` |
| 15 | `AGS_ELIMINATION_ACTIVE` | `true` |

### conditions/ags_surrender.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 13 | `AGS_SURRENDER_MODULE` | `"AGS_Surrender"` |
| 14 | `AGS_SURRENDER_OBJECTIVE` | `nil` |
| 15 | `AGS_SURRENDER_ACTIVE` | `true` |

### conditions/ags_wonder.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 12 | `AGS_WONDER_MODULE` | `"AGS_Wonder"` |
| 13 | `AGS_WONDER_OBJECTIVE` | `nil` |
| 14 | `AGS_WONDER_ACTIVE` | `true` |
| 15 | `AGS_WONDER_FOW_REVEAL_RADIUS` | `12` |
| 16 | `AGS_WONDER_VICTORY_TIME` | `15 * 60` |
| 17 | `AGS_WONDER_CHECK_FREQUENCY` | `1.0` |
| 18 | `AGS_WONDER_RUSH` | `false` |
| 20 | `AGS_WONDER_WINNER` | `{` |

### conditions/conditiondata/ags_annihilation_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_ANNIHILATION` | `{` |
| 24 | `AGS_NOTIFICATIONS_ANNIHILATION` | `{` |

### conditions/conditiondata/ags_conquest_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_CONQUEST` | `{` |
| 28 | `AGS_NOTIFICATIONS_CONQUEST` | `{` |
| 34 | `AGS_NOTIFICATIONS_CONQUEST_ATTACKED` | `{` |
| 42 | `AGS_NOTIFICATIONS_CONQUEST_DESTROYED` | `{` |

### conditions/conditiondata/ags_culture_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_CULTURE_SECONDARY` | `{` |
| 19 | `AGS_OBJECTIVES_CULTURE` | `{` |
| 33 | `AGS_NOTIFICATIONS_CULTURE` | `{` |
| 39 | `AGS_NOTIFICATIONS_CULTURE_APPROACH` | `{` |
| 54 | `AGS_NOTIFICATIONS_CULTURE_CAPTURING` | `{` |
| 69 | `AGS_NOTIFICATIONS_CULTURE_CAPTURED` | `{` |
| 84 | `AGS_NOTIFICATIONS_CULTURE_CONTESTING` | `{` |
| 99 | `AGS_NOTIFICATIONS_CULTURE_NEUTRALIZING` | `{` |
| 114 | `AGS_NOTIFICATIONS_CULTURE_NEUTRALIZED` | `{` |

### conditions/conditiondata/ags_elimination_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_ELIMINATION` | `{` |
| 24 | `AGS_NOTIFICATIONS_ELIMINATION` | `{` |

### conditions/conditiondata/ags_regicide_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_REGICIDE` | `{` |
| 28 | `AGS_NOTIFICATIONS_REGICIDE` | `{` |
| 34 | `AGS_NOTIFICATIONS_REGICIDE_ATTACKED` | `{` |

### conditions/conditiondata/ags_religious_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_RELIGIOUS_SECONDARY` | `{` |
| 19 | `AGS_OBJECTIVES_RELIGIOUS` | `{` |
| 38 | `AGS_NOTIFICATIONS_RELIGIOUS` | `{` |
| 44 | `AGS_NOTIFICATIONS_RELIGIOUS_COUNTDOWN` | `{` |
| 55 | `AGS_NOTIFICATIONS_RELIGIOUS_STARTED` | `{` |
| 61 | `AGS_NOTIFICATIONS_RELIGIOUS_INTERRUPTED` | `{` |
| 67 | `AGS_NOTIFICATIONS_RELIGIOUS_APPROACH` | `{` |
| 82 | `AGS_NOTIFICATIONS_RELIGIOUS_CAPTURING` | `{` |
| 97 | `AGS_NOTIFICATIONS_RELIGIOUS_CAPTURED` | `{` |
| 112 | `AGS_NOTIFICATIONS_RELIGIOUS_CONTESTING` | `{` |
| 127 | `AGS_NOTIFICATIONS_RELIGIOUS_NEUTRALIZING` | `{` |
| 142 | `AGS_NOTIFICATIONS_RELIGIOUS_NEUTRALIZED` | `{` |

### conditions/conditiondata/ags_score_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_SCORE` | `{` |
| 30 | `AGS_NOTIFICATIONS_SCORE` | `{` |
| 36 | `AGS_NOTIFICATIONS_SCORE_COUNTDOWN` | `{` |

### conditions/conditiondata/ags_surrender_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_SURRENDER` | `{` |
| 24 | `AGS_NOTIFICATIONS_SURRENDER` | `{` |

### conditions/conditiondata/ags_team_solidarity_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_TEAMSOLIDARITY` | `{` |
| 28 | `AGS_NOTIFICATIONS_TEAM_SOLIDARITY` | `{` |

### conditions/conditiondata/ags_treaty_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_TREATY` | `{` |
| 30 | `AGS_NOTIFICATIONS_TREATY_COUNTDOWN` | `{` |

### conditions/conditiondata/ags_wonder_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_OBJECTIVES_WONDER_SELF` | `{` |
| 18 | `AGS_OBJECTIVES_WONDER_ALLY` | `{` |
| 26 | `AGS_OBJECTIVES_WONDER_ENEMY` | `{` |
| 34 | `AGS_OBJECTIVES_WONDER` | `{` |
| 50 | `AGS_NOTIFICATIONS_WONDER` | `{` |
| 56 | `AGS_NOTIFICATIONS_WONDER_ATTACKED` | `{` |
| 64 | `AGS_NOTIFICATIONS_WONDER_CONSTRUCTION` | `{` |
| 78 | `AGS_NOTIFICATIONS_WONDER_DESTROYED` | `{` |
| 105 | `AGS_NOTIFICATIONS_WONDER_COUNTDOWN` | `{` |

## debug

### debug/cba_debug_autopop.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `_AUTOPOP_DEBUG_VERBOSE` | `false` |
| 10 | `_AUTOPOP_TEST_RESULTS` | `{}  -- [playerIndex] = { civ, tracked, effective, delta, status }` |

### debug/cba_debug_blueprint_audit.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 293 | `_ENUMERATE_UNIT_STEMS` | `{` |

### debug/cba_debug_civ_overview.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 13 | `_CBA_DEBUG_CIV_OVERVIEW` | `nil` |

### debug/cba_debug_core.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 17 | `CBA_DEBUG_MODULE` | `"CBA_Debug"` |
| 19 | `_cba_debug` | `{` |
| 643 | `debug` | `{` |

### debug/cba_debug_coverage.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 12 | `_cba_coverage` | `{` |

### debug/cba_debug_helpers.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1271 | `_Debug_PlayerUI_PhaseBSuiteState` | `nil` |

### debug/cba_debug_leaver.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 31 | `_LEAVER_DEBUG_FULL_PENDING` | `nil` |
| 32 | `_LEAVER_DEBUG_FULL_RUN_COUNTER` | `0` |
| 33 | `_LEAVER_DEBUG_MIL_COVERAGE_RUN_COUNTER` | `0` |
| 34 | `_LEAVER_MIL_TEST_PENDING` | `nil` |
| 35 | `_LEAVER_DEBUG_MILTEST_RUN_COUNTER` | `0` |
| 36 | `_LEAVER_MIL_TEST_CLASS_PROOF_STREAK` | `0` |
| 37 | `_LEAVER_MIL_ONESHOT_PENDING` | `nil` |
| 38 | `_LEAVER_MIL_ONESHOT_RUN_COUNTER` | `0` |
| 1417 | `_VISUAL_TEST_BUILDINGS_MILITARY` | `{ "barracks", "archery_range", "stable", "siege_workshop" }` |
| 1418 | `_VISUAL_TEST_BUILDINGS_ECONOMY` | `{ "house", "market", "blacksmith", "scar_dock" }` |
| 1419 | `_VISUAL_TEST_BUILDINGS_ADVANCED` | `{ "monastery", "castle" }` |
| 1420 | `_VISUAL_TEST_BUILDINGS_WALLS` | `{ "stone_wall", "palisade_wall", "palisade_gate" }` |
| 1421 | `_VISUAL_TEST_BUILDINGS_LANDMARKS` | `{ "town_center" }` |
| 1429 | `_VISUAL_TEST_CLEANUP_EIDS` | `{}` |
| 1430 | `_VISUAL_TEST_CLEANUP_SQS` | `{}` |
| 1431 | `_VISUAL_TEST_DEFERRED_CLEANUP` | `nil` |
| 1432 | `_VISUAL_TEST_CLEANUP_TRACE` | `true` |
| 1437 | `_VISUAL_TEST_UNITS` | `{` |
| 1480 | `_VISUAL_TEST_STATE` | `nil` |
| 1481 | `_VISUAL_TEST_CIV_OVERRIDE` | `nil` |
| 2556 | `_MIL_COVERAGE_PATTERNS` | `{` |
| 3042 | `_LEAVER_DEBUG_FULLSYS_PENDING` | `nil` |
| 3527 | `_LEAVER_PERF_CASCADE` | `nil` |

### debug/cba_debug_playerui_anim.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 48 | `_cba_debug_anim_monitor` | `{` |
| 56 | `_cba_debug_reward_capture` | `{` |
| 196 | `_cba_debug_anim_staged` | `{` |
| 209 | `_cba_debug_elim_validate` | `{` |

### debug/cba_debug_rules.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 22 | `RULE_HARD_FAIL` | `"hard_fail"   -- Pipeline-stopping: must pass for system to be valid` |
| 23 | `RULE_WARNING` | `"warning"     -- Logged concern: does not block but should be investigated` |
| 24 | `RULE_INFO` | `"info"        -- Advisory: informational metric, never blocks` |

### debug/cba_debug_settings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 91 | `_DEBUG_SETTINGS` | `{}` |

### debug/cba_debug_siege_test.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1426 | `Debug_SiegeLimits` | `Debug_SiegeTest` |

### debug/cba_debug_stress.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `STRESS_ALL_CIVS` | `{` |
| 17 | `_cba_stress` | `{` |

### debug/cba_debug_ui_prompts.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 15 | `_cba_debug_prompts` | `{` |

### debug/cba_verify_military_pipeline.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 27 | `_LEAVER_VERIFY_STATE` | `{` |

## gameplay

### gameplay/ags_auto_population.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `AGS_POPULATION_AUTOMATIC_MODULE` | `"AGS_PopulationAutomatic"` |
| 12 | `_AGS_AutoPop_Caps` | `{}` |
| 13 | `_AGS_AutoPop_InnateCorrected` | `{}` |
| 14 | `_AGS_AutoPop_Corrections` | `{}  -- Soft-correction tracking per player for reconciler` |
| 15 | `_AGS_AutoPop_ForbiddenBPSet` | `{}   -- Init-time EBP lookup set for event-driven pop-source detection` |
| 16 | `_AGS_AutoPop_DeferredPending` | `false  -- Deferred reconcile one-shot guard` |
| 17 | `_AGS_AutoPop_RewardSuppressCount` | `0  -- Counter for reward-path unlock suppressions` |
| 21 | `_AGS_POP_LOCK_KEYS` | `{` |

### gameplay/ags_auto_resources.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `AGS_AUTO_RESOURCES_MODULE` | `"AGS_AutoResources"` |

### gameplay/ags_game_rates.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_GAME_RATES_MODULE` | `"AGS_GameRates"` |
| 11 | `AGS_GAME_RATES_MODIFIERS` | `{ }` |

### gameplay/ags_gather_rates.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_GATHER_RATES_MODULE` | `"AGS_GatherRates"` |
| 11 | `AGS_GATHER_RATES_MODIFIERS` | `{ }` |

### gameplay/ags_handicaps.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_HANDICAPS_MODULE` | `"AGS_Handicaps"` |
| 12 | `AGS_HANDICAPS_TABLE` | `{` |
| 22 | `AGS_HANDICAPS_ECO_MODIFIERS` | `{ }` |
| 23 | `AGS_HANDICAPS_MIL_MODIFIERS` | `{ }` |

### gameplay/ags_limits_ui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 31 | `AGS_LIMITS_UI_MODULE` | `"AGS_LimitsUI"` |
| 34 | `AGS_LIMITS_UI_BAR_MAX` | `160` |
| 35 | `AGS_LIMITS_UI_YELLOW_START_RATIO` | `(8 / 15)` |
| 38 | `AGS_LIMITS_UI_ANIM` | `{` |
| 51 | `AGS_LIMITS_UI_TRACE_UPDATE_FLOW` | `false` |
| 57 | `AGS_LIMITS_UI_CONTEXT` | `{` |
| 140 | `AGS_LIMITS_UI_ROW_DEFS` | `{` |

### gameplay/ags_no_dock.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 14 | `AGS_NO_DOCK_MODULE` | `"AGS_NoDock"` |
| 15 | `AGS_NO_WALL_MODULE` | `"AGS_NoWall"` |
| 16 | `AGS_NO_SIEGE_MODULE` | `"AGS_NoSiege"` |
| 17 | `AGS_NO_ARSENAL_MODULE` | `"AGS_NoArsenal"` |

### gameplay/ags_population_capacity.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 12 | `AGS_POPULATION_CAPACITY_MODULE` | `"AGS_PopulationCapacity"` |
| 13 | `AGS_MedicPopulation_CAPACITY_MODULE` | `"AGS_MedicPopulationCapacity"` |

### gameplay/ags_reveal_fow_on_elimination.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_REVEAL_FOW_ON_ELIMINATION_MODULE` | `"AGS_RevealFowOnElimination"` |

### gameplay/ags_siege_house.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_DOCKHOUSE_POPULATION` | `10` |
| 11 | `AGS_DOCKHOUSE_MODULE` | `"AGS_DockHouse"` |

### gameplay/ags_special_population_ui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_SPECIALPOPULATION_UI_MODULE` | `"AGS_SpecialPopulationUI"` |
| 11 | `AGS_SPECIALPOPULATION_UI_CONTEXT` | `{` |

### gameplay/ags_starting_age.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_STARTING_AGE_MODULE` | `"AGS_StartingAge"` |

### gameplay/ags_team_balance.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `AGS_TEAM_BALANCE_MODULE` | `"AGS_TeamBalance"` |
| 12 | `AGS_TEAM_BALANCE_TEAM_BONUS` | `{}` |
| 13 | `AGS_TEAM_BALANCE_MEDIC_BONUS` | `{}` |

### gameplay/ags_tree_bombardment.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `AGS_TREE_BOMBARDMENT_MODULE` | `"AGS_TreeBombardment"` |
| 12 | `AGS_TREE_BOMBARDMENT` | `{` |

### gameplay/ags_unit_rates.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_UNIT_RATES_MODULE` | `"AGS_UnitRates"` |
| 11 | `AGS_UNIT_RATES_MODIFIERS` | `{ }` |

### gameplay/cba_auto_age.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 6 | `_autoage` | `{` |
| 17 | `CBA_AUTO_AGE_AUTOAGE_MODULE` | `"CBA_AutoAge"` |
| 19 | `_AUTOAGE_SPECIAL_UPGRADES` | `{` |

### gameplay/cba_economy.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `CBA_ECONOMY_RESOURCES` | `{` |

### gameplay/cba_hre_balance.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `CBA_HRE_BALANCE_MODULE` | `"CBA_HREBalance"` |
| 12 | `CBA_HRE_BALANCE_MODIFIERS` | `{ }` |

### gameplay/cba_options.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 5 | `CBA_OPTIONS_MODULE` | `"CBA_Options"` |
| 132 | `_BLUEPRINT_REVERSE_MAP` | `{}` |
| 1052 | `_CBA_SiegeLimit_DeferredRecheckPending` | `_CBA_SiegeLimit_DeferredRecheckPending or {}` |
| 1053 | `_CBA_SiegeLimit_DeferredRecheckScheduled` | `_CBA_SiegeLimit_DeferredRecheckScheduled or false` |
| 1345 | `_CBA_PERF` | `_CBA_PERF or { sg_allocs = 0, eg_allocs = 0, recount_calls = 0, queue_scans = 0, disable_skipped = 0, reconcile_ticks = ...` |
| 1875 | `_CBA_ENFORCE_IN_PROGRESS` | `false` |
| 2509 | `_CBA_SiegeWeaponBPMapCache` | `_CBA_SiegeWeaponBPMapCache or {}` |

### gameplay/cba_siege_data.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `BP_SIEGE_WORKSHOP` | `"scar_siegeworkshop" -- Duplicate / not used` |
| 11 | `BP_SIEGE_RAM` | `"ram"` |
| 12 | `BP_SIEGE_WORKSHOP_RAM` | `"workshop_ram"` |
| 13 | `BP_SIEGE_SPRINGALD` | `"springald"` |
| 14 | `BP_SIEGE_MANGONEL` | `"mangonel"` |
| 15 | `BP_SIEGE_RIBAULDEQUIN` | `"ribauldequin"` |
| 16 | `BP_SIEGE_CULVERIN` | `"culverin"` |
| 17 | `BP_SIEGE_CANNON` | `"cannon"` |
| 18 | `BP_SIEGE_BOMBARD` | `"bombard"` |
| 19 | `BP_SIEGE_TREBUCHET_CW` | `"trebuchet_cw"` |
| 20 | `BP_SIEGE_TREBUCHET_TR` | `"trebuchet_tr"  -- Used by Tuning Pack for all factions` |
| 21 | `BP_SIEGE_TOWER` | `"siege_tower"` |
| 23 | `RAM_LIMIT_MAX` | `5` |
| 24 | `SIEGE_TOWER_LIMIT_MAX` | `5` |
| 26 | `BP_SIEGE_SPRINGALD_ABB` | `"unit_springald_3_buildable_abb"` |
| 27 | `BP_SIEGE_MANGONEL_ABB` | `"unit_mangonel_3_buildable_abb"` |
| 29 | `BP_SIEGE_SPRINGALD_ABB_HA_01` | `"unit_springald_3_buildable_abb_ha_01"` |
| 30 | `BP_SIEGE_MANGONEL_ABB_HA_01` | `"unit_mangonel_3_buildable_abb_ha_01"` |
| 32 | `BP_SIEGE_TREBUCHET_TR_BUILDALBE` | `"unit_trebuchet_4_tr_field_construct_mon"` |
| 33 | `BP_SIEGE_TREBUCHET_CW_BUILDALBE` | `"unit_trebuchet_4_cw_field_construct_mon"` |
| 34 | `BP_SIEGE_SPRINGALD_MON` | `"unit_springald_3_field_construct_mon"` |
| 35 | `BP_SIEGE_MANGONEL_MON` | `"unit_mangonel_3_field_construct_mon"` |
| 37 | `BP_SIEGE_TREBUCHET_CW_DOUBLE` | `"trebuchet_cw_double"` |
| 38 | `BP_SIEGE_TREBUCHET_TR_DOUBLE` | `"trebuchet_tr_double"` |
| 39 | `BP_SIEGE_SPRINGALD_DOUBLE` | `"springald_double"` |
| 40 | `BP_SIEGE_MANGONEL_DOUBLE` | `"mangonel_double"` |
| 41 | `BP_SIEGE_RIBAULDEQUIN_DOUBLE` | `"ribauldequin_double"` |
| 42 | `BP_SIEGE_CULVERIN_DOUBLE` | `"culverin_double"` |
| 43 | `BP_SIEGE_CANNON_DOUBLE` | `"cannon_double"` |
| 44 | `BP_SIEGE_BOMBARD_DOUBLE` | `"bombard_double"` |
| 46 | `BP_SIEGE_FRENCH_ROYAL` | `"siege_royal_fre"` |
| 47 | `BP_SIEGE_ROYAL_CANNON` | `"royal_cannon"` |
| 48 | `BP_SIEGE_ROYAL_CULVERIN` | `"royal_culverin"` |
| 49 | `BP_SIEGE_ROYAL_RIBAULDEQUIN` | `"royal_ribauldequin"` |
| 51 | `BP_SIEGE_NESTOFBEES` | `"nest_of_bees"` |
| 52 | `BP_SIEGE_NESTOFBEES_CLOCKTOWER_CHI` | `"nestofbees_clocktower_chi"` |
| 53 | `BP_SIEGE_MANGONEL_CLOCKTOWER_CHI` | `"mangonel_clocktower_chi"` |
| 54 | `BP_SIEGE_SPRINGALD_CLOCKTOWER_CHI` | `"springald_clocktower_chi"` |
| 55 | `BP_SIEGE_TREBUCHET_CLOCKTOWER_CHI` | `"trebuchet_clocktower_chi"` |
| 56 | `BP_SIEGE_BOMBARD_CLOCKTOWER_CHI` | `"bombard_clocktower_chi"` |
| 61 | `CBA_SIEGE_UNITS` | `{` |
| 128 | `CBA_SIEGE_TAG_REGISTRY` | `{` |
| 256 | `CBA_SIEGE_TABLE` | `{` |
| 609 | `CBA_CIV_BP_SUFFIX` | `{` |

## helpers

### helpers/ags_blueprints.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 15 | `AGS_BP_KEEP` | `"castle" --scar_keep or castle` |
| 16 | `AGS_BP_TC_CAPITAL` | `"town_center_capital"` |
| 17 | `AGS_BP_TC_CAPITAL_UNIT` | `"town_center_capital_moving"` |
| 18 | `AGS_BP_TC` | `"town_center"` |
| 19 | `AGS_BP_TC_LANDMARK` | `"town_center_landmark"` |
| 20 | `AGS_BP_VILLAGER` | `"villager"` |
| 21 | `AGS_BP_SPEARMAN` | `"spearman"` |
| 22 | `AGS_BP_ARCHER` | `"archer"` |
| 23 | `AGS_BP_HORSEMAN` | `"horseman"` |
| 24 | `AGS_BP_SPRINGALD` | `"springald"` |
| 25 | `AGS_BP_MONK` | `"monk"` |
| 26 | `AGS_BP_SCOUT` | `"scout"` |
| 27 | `AGS_BP_KING` | `"king"` |
| 28 | `AGS_BP_SHEEP` | `"sheep"` |
| 29 | `AGS_BP_TREE` | `"tree"` |
| 30 | `AGS_BP_LANDMARK` | `"wonder"` |
| 31 | `AGS_BP_WONDER` | `"wonder_imperial_age"` |
| 32 | `AGS_BP_SACRED_SITE` | `"special_beacon"` |
| 34 | `AGS_BP_BUILDING` | `"building"` |
| 36 | `AGS_BP_UNIT_CLASS` | `"annihilation_condition"` |
| 37 | `AGS_BP_GAIA` | `"gaia"` |
| 38 | `AGS_BP_MOVING_BUILDINGS` | `"mongol_moving_structure"` |
| 39 | `AGS_BP_HOUSE_UNIT` | `"house_moving"` |
| 40 | `AGS_BP_HOW` | `"house_of_wisdom"` |
| 41 | `AGS_BP_PALISADE` | `"palisade_wall"` |
| 42 | `AGS_BP_PALISADE_GATE` | `"palisade_gate"` |
| 43 | `AGS_BP_ANY_WALL` | `"wall"` |
| 44 | `AGS_BP_ANY_GATE` | `"gate"` |
| 45 | `AGS_BP_MOBILE` | `"mobile_building"` |
| 46 | `AGS_BP_SIEGE` | `"siege"` |
| 47 | `AGS_BP_WORKER` | `"worker"` |
| 48 | `AGS_BP_MILITARY` | `"military"` |
| 49 | `AGS_BP_MONASTERY` | `"monastery"` |
| 50 | `AGS_BP_BARRACKS` | `"barracks"` |
| 51 | `AGS_BP_ARCHERY_RANGE` | `"archery_range"` |
| 52 | `AGS_BP_STABLE` | `"stable"` |
| 53 | `AGS_BP_MARKET` | `"market"` |
| 54 | `AGS_BP_DOCK` | `"scar_dock"` |
| 55 | `AGS_BP_HOUSE` | `"house"` |
| 56 | `AGS_BP_BLACKSMITH` | `"blacksmith"` |
| 57 | `AGS_BP_UNIVERSITY` | `"university"` |
| 58 | `AGS_BP_ARSENAL` | `"arsenal"` |
| 59 | `AGS_BP_RELIC` | `"relic"` |
| 60 | `AGS_BP_TREASURE` | `"resource_pickup"` |
| 61 | `AGS_BP_TREASURE_FOOD` | `"resource_pickup_food"` |
| 62 | `AGS_BP_TREASURE_WOOD` | `"resource_pickup_wood"` |
| 63 | `AGS_BP_TREASURE_GOLD` | `"resource_pickup_gold"` |
| 64 | `AGS_BP_TREASURE_STONE` | `"resource_pickup_stone"` |
| 65 | `AGS_BP_DEPOSIT_GOLD` | `"gold"` |
| 66 | `AGS_BP_DEPOSIT_STONE` | `"stone"` |
| 67 | `AGS_BP_DEPOSIT_FOOD` | `"forage_bush"` |
| 68 | `AGS_BP_DEPOSIT_MARKET` | `"settlement"` |
| 69 | `AGS_BP_DEPOSIT_ANIMAL` | `"animal"` |
| 70 | `AGS_BP_WORKSHOP` | `"siege_workshop"` |
| 71 | `AGS_BP_CROSSBOW` | `"crossbow" -- Not used` |
| 72 | `AGS_BP_STONEWALL` | `"stone_wall"` |
| 73 | `AGS_BP_MINING_CAMP` | `"mining_camp"` |
| 74 | `AGS_BP_LUMBER_CAMP` | `"lumber_camp"` |
| 75 | `AGS_BP_MILL` | `"mill"` |
| 77 | `AGS_UP_ANY` | `"common"` |
| 78 | `AGS_UP_SPECIAL` | `"special"` |
| 79 | `AGS_UP_A_MELEE_I` | `"melee1_attack" -- CBA Reward list upgrades` |
| 80 | `AGS_UP_D_MELEE_I` | `"melee1_defense"` |
| 81 | `AGS_UP_A_MELEE_II` | `"melee2_attack"` |
| 82 | `AGS_UP_D_MELEE_II` | `"melee2_defense"` |
| 83 | `AGS_UP_A_MELEE_III` | `"melee3_attack"` |
| 84 | `AGS_UP_D_MELEE_III` | `"melee3_defense"` |
| 85 | `AGS_UP_A_RANGED_I` | `"ranged1_attack"` |
| 86 | `AGS_UP_D_RANGED_I` | `"ranged1_defense"` |
| 87 | `AGS_UP_A_RANGED_II` | `"ranged2_attack"` |
| 88 | `AGS_UP_D_RANGED_II` | `"ranged2_defense"` |
| 89 | `AGS_UP_A_RANGED_III` | `"ranged3_attack"` |
| 90 | `AGS_UP_D_RANGED_III` | `"ranged3_defense"` |
| 91 | `AGS_UP_MANATARMS_ELITE` | `"maa_elite_tactics"` |
| 92 | `AGS_UP_SPEARMAN_ELITE` | `"spear_elite_tactics"` |
| 93 | `AGS_UP_BIOLOGY` | `"biology"` |
| 94 | `AGS_UP_BARDING` | `"barding"` |
| 95 | `AGS_UP_GRAPERED_LANCE` | `"grapered_lance"` |
| 96 | `AGS_UP_MILITARY_ACADEMY` | `"military_academy"` |
| 97 | `AGS_UP_RANGED_INCENDIARY` | `"ranged_incendiary"` |
| 98 | `AGS_UP_ARCHITECTURE` | `"university_architecture"` |
| 99 | `AGS_UP_CHEMISTRY` | `"university_chemistry"` |
| 100 | `AGS_UP_SIEGE_WORKS` | `"siege_works"` |
| 101 | `AGS_UP_SIEGE_SPEED` | `"siege_speed"` |
| 102 | `AGS_UP_SIEGE_ROLLER_TRIGGER` | `"roller_trigger"` |
| 103 | `AGS_UP_SIEGE_ADJUSTABLE_CROSSBAR` | `"adjustable_crossbar"` |
| 104 | `AGS_UP_SIEGE_ENGINEERS` | `"siege_engineers"` |
| 106 | `AGS_UP_LONGBOW_CAMP` | `"longbow_make_camp"` |
| 107 | `AGS_UP_LONBOW_PALINGS` | `"ranged_palings"` |
| 108 | `AGS_UP_LONGBOW_VOLLEY` | `"arrow_volley"` |
| 109 | `AGS_UP_LONGBOW_DMGPEN` | `"longbow_armor_penetration"` |
| 110 | `AGS_UP_LONGBOW_DAMAGE` | `"longbow_damage"` |
| 111 | `AGS_UP_ARMOR_CLAD` | `"armor_clad"` |
| 112 | `AGS_UP_TREBUCHET_AOE` | `"trebuchet_aoe"]]` |
| 114 | `AGS_CIV_SULTANATE` | `"sultanate"` |
| 115 | `AGS_CIV_ENGLISH` | `"english"` |
| 116 | `AGS_CIV_HRE` | `"hre"` |
| 117 | `AGS_CIV_MONGOL` | `"mongol"` |
| 118 | `AGS_CIV_ABBASID` | `"abbasid"` |
| 119 | `AGS_CIV_CHINESE` | `"chinese"` |
| 120 | `AGS_CIV_RUS` | `"rus"` |
| 121 | `AGS_CIV_FRENCH` | `"french"` |
| 122 | `AGS_CIV_MALIAN` | `"malian"` |
| 123 | `AGS_CIV_OTTOMAN` | `"ottoman"` |
| 124 | `AGS_CIV_ABBASID_HA_01` | `"abbasid_ha_01"` |
| 125 | `AGS_CIV_CHINESE_HA_01` | `"chinese_ha_01"` |
| 126 | `AGS_CIV_FRENCH_HA_01` | `"french_ha_01"` |
| 127 | `AGS_CIV_HRE_HA_01` | `"hre_ha_01"` |
| 128 | `AGS_CIV_JAPANESE` | `"japanese"` |
| 129 | `AGS_CIV_BYZANTINE` | `"byzantine"` |
| 130 | `AGS_CIV_MONGOL_HA_GOL` | `"mongol_ha_gol"` |
| 131 | `AGS_CIV_LANCASTER` | `"lancaster"` |
| 132 | `AGS_CIV_TEMPLAR` | `"templar"` |
| 133 | `AGS_CIV_BYZANTINE_HA_MAC` | `"byzantine_ha_mac"` |
| 134 | `AGS_CIV_JAPANESE_HA_SEN` | `"japanese_ha_sen"` |
| 135 | `AGS_CIV_SULTANATE_HA_TUG` | `"sultanate_ha_tug"` |
| 141 | `AGS_CIV_PARENT_MAP` | `{` |
| 153 | `AGS_CIV_FACTION_MAP` | `{` |
| 178 | `AGS_UNIT_BP_OVERRIDES` | `{` |
| 190 | `AGS_UP_DARK` | `"AGE_DARK"` |
| 191 | `AGS_UP_FEUDAL` | `"AGE_FEUDAL"` |
| 192 | `AGS_UP_CASTLE` | `"AGE_CASTLE"` |
| 193 | `AGS_UP_IMPERIAL` | `"AGE_IMPERIAL"` |
| 198 | `AGS_BUILDING_FALLBACK_MAP` | `{` |
| 212 | `AGS_ENTITY_TABLE` | `{` |
| 929 | `AGS_CIV_PREFIXES` | `{` |
| 956 | `AGS_UPGRADE_AGES` | `{` |
| 963 | `AGS_UPGRADE_CORRECTION_TABLE` | `{` |
| 1061 | `AGS_UPGRADE_TABLE` | `{` |
| 2574 | `AGS_NIL_BP_WARNINGS` | `AGS_NIL_BP_WARNINGS or {}` |
| 2693 | `AGS_SAE_SELF` | `0` |
| 2694 | `AGS_SAE_ALLY` | `1` |
| 2695 | `AGS_SAE_ENEMY` | `2` |

### helpers/ags_teams.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_TEAMS_MODULE` | `"AGS_Teams"` |
| 11 | `AGS_TEAMS_TABLE` | `{` |

## observerui

### observerui/gamestatetracking/ontributesent.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 3 | `TRIBUTE_RESOURCES` | `{` |

### observerui/observerui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 73 | `_SwapPlayers1v1ButtonDataContext` | `{` |
| 77 | `_SymmetryButtonDataContext` | `{` |
| 81 | `_ToggleUIButtonDataContext` | `{` |
| 85 | `_HideMessagesButtonDataContext` | `{` |
| 89 | `_HideArmyButtonDataContext` | `{` |
| 93 | `_SwapResourceWithIncomePerMinuteButtonDataContext` | `{` |
| 97 | `_IsImprovedUIVisible` | `true` |

### observerui/observeruiconstants.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUiConstants` | `{` |

### observerui/observeruiinitialization.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUiInitialization` | `{` |

### observerui/observeruimessagesystem.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUiMessageSystem` | `{` |

### observerui/observeruirulesystem.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUiRuleSystem` | `{` |
| 76 | `_DefaultFuncTable` | `{ Func = _NoOp }` |
| 77 | `_DefaultFuncMt` | `{ __index = function () return _DefaultFuncTable end}` |

### observerui/observeruiupdateui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_ObserverUIDataContext` | `ObserverUiDataContext` |
| 4 | `ObserverUi_ResourceMapping` | `{` |
| 15 | `_AgeIconsForAnimation` | `{` |
| 26 | `_AgeIcons` | `{` |
| 37 | `_RaceImage` | `{` |

### observerui/settings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUI_Settings` | `{` |

### observerui/tracking_agingupprogress.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `AgingUpProgress` | `{}` |

### observerui/tracking_aginguptimings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `AgingUpTimings` | `{` |

### observerui/tracking_gameobjectrepository.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `GameObjectRepository` | `{` |

### observerui/tracking_ownedsquads.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `OwnedSquads` | `{}` |

### observerui/tracking_populationcapped.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `PopulationCapped` | `{}` |

### observerui/tracking_populationcomposition.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `PopulationComposition` | `{}` |

### observerui/tracking_queuedstuff.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `QueuedStuff` | `{}` |

### observerui/tracking_reliclocations.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `RelicLocations` | `{}` |

### observerui/tracking_squadlosses.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `SquadLosses` | `{}` |

### observerui/tracking_towncenteridling.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `TownCenterIdling` | `{}` |

### observerui/tracking_workeridling.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `WorkerIdling` | `{}` |

### observerui/uidatacontext/initialize_numberofplayers.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiNumberOfPlayers` | `{}` |

### observerui/uidatacontext/initialize_observeruidatacontextmappings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUIDataContextMappings` | `{` |

### observerui/uidatacontext/observeruidatacontext.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `ObserverUiDataContext` | `{}` |

### observerui/uidatacontext/updateui_landmarkvictory.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiLandmarkVictory` | `{}` |

### observerui/uidatacontext/updateui_messages.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiMessages` | `{` |

### observerui/uidatacontext/updateui_populationcapped.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiPopulationCapped` | `{}` |

### observerui/uidatacontext/updateui_squadlosses.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiSquadLosses` | `{}` |

### observerui/uidatacontext/updateui_teamsummary.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiTeamSummary` | `{}` |

### observerui/uidatacontext/updateui_victorycountdowns.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `UiVictoryCountdowns` | `{}` |

### observerui/xaml/hidearmybutton.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `XamlHideArmyButton` | `` |

### observerui/xaml/hidemessagesbutton.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `XamlHideMessagesButton` | `` |

### observerui/xaml/observe2players.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_Observe2PlayersXaml` | `` |

### observerui/xaml/observenplayers.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_ObserveNPlayersXaml` | `` |
| 3 | `xmlns` | `"http://schemas.microsoft.com/winfx/2006/xaml/presentation"` |

### observerui/xaml/swapplayers1v1button.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_SwapPlayers1v1ButtonXaml` | `` |

### observerui/xaml/swapresourcewithincomeperminutebutton.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_SwapResourceWithIncomePerMinuteButtonXaml` | `` |

### observerui/xaml/symmetrybutton.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_SymmetryButtonXaml` | `` |

### observerui/xaml/teamvteam.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `XamlTeamVTeam` | `` |

### observerui/xaml/toggleuibutton.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 1 | `_ToggleUIButtonXaml` | `` |

## playerui

### playerui/playerui_animate.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 15 | `_PlayerUI_Anim` | `{}           -- keyed by string id → { target = N, display = N }` |
| 16 | `_PlayerUI_AnimDirty` | `false   -- true while any display ≠ target` |
| 17 | `_PlayerUI_AnimMaxStepTicks` | `15   -- ticks to converge (15 × 0.1s = 1.5s)` |
| 20 | `_PLAYERUI_ANIM_EASE_BASE_DURATION` | `1.0   -- seconds at delta=1` |
| 21 | `_PLAYERUI_ANIM_EASE_MIN_DURATION` | `0.5    -- minimum seconds` |
| 22 | `_PLAYERUI_ANIM_EASE_MAX_DURATION` | `3.0    -- maximum seconds` |
| 23 | `_PLAYERUI_ANIM_TICK_INTERVAL` | `0.1        -- seconds per tick` |
| 27 | `_PlayerUI_AnimPositions` | `{}` |
| 28 | `_PlayerUI_AnimPositionsDirty` | `false` |
| 29 | `_PLAYERUI_ANIM_EASEOUT_FACTOR` | `0.25   -- lerp factor per 0.1s tick (~400ms convergence)` |
| 30 | `_PLAYERUI_ANIM_POSITION_EPSILON` | `0.5  -- px threshold to snap to target` |
| 33 | `_PlayerUI_AnimDecay` | `{}` |
| 36 | `_PlayerUI_ScorePulse` | `{}` |
| 37 | `_PLAYERUI_PULSE_DECAY` | `0.30` |
| 38 | `_PLAYERUI_PULSE_SCALE_PEAK` | `0.12` |
| 39 | `_PLAYERUI_PULSE_EPSILON` | `0.01` |
| 40 | `_PLAYERUI_HIGHLIGHT_DECAY_RATE` | `0.12` |
| 41 | `_PLAYERUI_SCALE_POP_PEAK` | `0.08` |
| 42 | `_PLAYERUI_SCALE_POP_DECAY_RATE` | `0.20` |
| 45 | `_PlayerUI_ElimDiag` | `{` |
| 63 | `_PlayerUI_RewardIconSlotState` | `{}      -- array of { threshold, opacity, borderColor, targetBorderColor, offsetX, targetOffsetX, scale, targetScale }` |
| 64 | `_PlayerUI_RewardIconSmoothingActive` | `false` |
| 65 | `_PlayerUI_RewardIconSmoothingInitialized` | `false` |
| 68 | `_PlayerUI_RewardStripOffsetX` | `0` |
| 69 | `_PlayerUI_RewardStripTargetOffsetX` | `0` |
| 72 | `_PlayerUI_MotionGuards` | `{` |
| 1548 | `_PlayerUI_EliminationAnims` | `{}` |
| 1681 | `_PlayerUI_EliminationRevealAnims` | `{}` |
| 1766 | `_PlayerUI_EliminationGlowAnims` | `{}` |

### playerui/playerui_constants.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 5 | `PlayerUiConstants` | `{` |
| 18 | `_PLAYERUI_ELIM_ANIM_DURATION` | `0.5         -- animation duration in seconds` |
| 19 | `_PLAYERUI_ELIM_ANIM_FADE_TARGET` | `0.4      -- final opacity multiplier (0.4 = standard dim)` |
| 20 | `_PLAYERUI_ELIM_ANIM_SCALE_MIN` | `0.95       -- scale floor (animates from 0.95 back to 1.0)` |
| 21 | `_PLAYERUI_ELIM_ANIM_SEED_PROGRESS` | `0.08   -- immediate first-frame progress so fade is visible on trigger pass` |
| 22 | `_PLAYERUI_ELIM_ANIM_MAX_PROGRESS_STEP` | `0.35 -- clamp per tick to avoid skip-to-complete on delayed frames` |
| 23 | `_PLAYERUI_ELIM_ANIM_DEBUG` | `false          -- debug output toggle` |
| 31 | `_PLAYERUI_ELIM_REVEAL_DURATION` | `0.25       -- reveal fade-in duration in seconds` |
| 32 | `_PLAYERUI_ELIM_REVEAL_SEED_PROGRESS` | `0.10  -- immediate first-frame progress so reveal is visible on trigger` |
| 33 | `_PLAYERUI_ELIM_REVEAL_MAX_PROGRESS_STEP` | `0.40 -- clamp per tick to avoid skip-to-complete` |
| 40 | `_PLAYERUI_ELIM_GLOW_DURATION` | `0.30         -- glow pulse duration in seconds` |
| 41 | `_PLAYERUI_ELIM_GLOW_PEAK_OPACITY` | `0.30     -- starting opacity of glow overlay` |
| 42 | `_PLAYERUI_ELIM_GLOW_SEED_PROGRESS` | `0.10    -- immediate first-frame progress` |
| 43 | `_PLAYERUI_ELIM_GLOW_MAX_PROGRESS_STEP` | `0.40 -- clamp per tick to avoid skip-to-complete` |
| 49 | `_PLAYERUI_ELIM_MARGIN_SLIDE_PX` | `3              -- vertical slide distance in px` |
| 50 | `_PLAYERUI_ELIM_SCORE_COLOR_ALIVE` | `"#FFFFFFFF"  -- white (alive score colour)` |
| 51 | `_PLAYERUI_ELIM_SCORE_COLOR_FINAL` | `"#FF888888"  -- grey (eliminated score colour)` |
| 52 | `_PLAYERUI_ELIM_STATUS_COLOR_START` | `"#FF888888"  -- grey (status label start colour for lerp)` |
| 59 | `_PLAYERUI_REWARD_ICON_FADE_IN_RATE` | `0.15       -- opacity increase per 0.1s tick (~0.7s full fade)` |
| 60 | `_PLAYERUI_REWARD_ICON_FADE_SEED` | `0.25          -- starting opacity when slot content changes` |
| 61 | `_PLAYERUI_REWARD_ICON_BORDER_LERP` | `0.20        -- border colour lerp factor per 0.1s tick` |
| 70 | `_PLAYERUI_REWARD_HIGHLIGHT_DURATION` | `1.0       -- seconds to hold completed icon with glow + de-emphasis` |
| 71 | `_PLAYERUI_REWARD_FADEOUT_DURATION` | `0.55         -- seconds for completed icon to fade out (was 0.4)` |
| 72 | `_PLAYERUI_REWARD_RESHUFFLE_DURATION` | `0.6        -- seconds for remaining icons to restore and reposition (was 0.4)` |
| 73 | `_PLAYERUI_REWARD_DEEMPHASIS_OPACITY` | `0.30       -- queued icon opacity during highlight/fadeout` |
| 74 | `_PLAYERUI_REWARD_GLOW_PEAK_OPACITY` | `0.35        -- peak gold overlay opacity on completed icon` |
| 75 | `_PLAYERUI_REWARD_GLOW_HOLD_RATIO` | `0.30          -- fraction of highlight duration to hold peak before decay` |
| 76 | `_PLAYERUI_REWARD_DEEMPH_RAMP_RATIO` | `0.50        -- fraction of highlight to ramp de-emphasis (was hard-coded 0.3)` |
| 77 | `_PLAYERUI_REWARD_ADVANCE_DWELL` | `0.15            -- seconds to pause between reshuffle and next milestone` |
| 78 | `_PLAYERUI_REWARD_RESHUFFLE_STAGGER` | `0.08        -- seconds per slot of staggered reshuffle entry` |
| 86 | `_PLAYERUI_REWARD_ICON_OFFSET_LERP` | `0.25         -- lerp factor per 0.1s tick for offsetX convergence` |
| 87 | `_PLAYERUI_REWARD_ICON_OFFSET_EPSILON` | `0.5        -- px threshold to snap offsetX to target` |
| 88 | `_PLAYERUI_REWARD_ICON_SCALE_LERP` | `0.25           -- lerp factor per 0.1s tick for scale convergence` |
| 89 | `_PLAYERUI_REWARD_ICON_SCALE_EPSILON` | `0.01        -- threshold to snap scale to target` |
| 90 | `_PLAYERUI_REWARD_ICON_SCALE_HIGHLIGHT` | `1.20      -- completed icon scale during highlight (expressive)` |
| 91 | `_PLAYERUI_REWARD_ICON_SCALE_DEEMPH` | `0.80         -- queued icon scale during highlight/fadeout` |
| 92 | `_PLAYERUI_REWARD_ICON_OFFSET_SLIDE` | `20           -- px: new lead icon slides left during reshuffle` |
| 93 | `_PLAYERUI_REWARD_CENTER_DURATION` | `0.35           -- seconds: completion_center convergence phase` |
| 94 | `_PLAYERUI_REWARD_CENTER_TIMEOUT` | `0.6             -- seconds: max time before force-advancing past center` |
| 95 | `_PLAYERUI_REWARD_FADEOUT_SCALE_END` | `0.60          -- completed icon scale at end of fadeout (shrink)` |
| 96 | `_PLAYERUI_REWARD_STRIP_OFFSET_LERP` | `0.20         -- strip-level pan lerp factor per tick` |
| 97 | `_PLAYERUI_REWARD_ICON_SLOT_WIDTH` | `36              -- px: icon natural width in StackPanel (30 icon + 6 margin)` |
| 98 | `_PLAYERUI_REWARD_FILL_BASE_DURATION` | `1.35         -- seconds for bar to smoothly fill 0→100% (center + highlight)` |
| 99 | `_PLAYERUI_REWARD_FILL_QUEUE_ACCEL` | `0.25           -- extra speed multiplier per queued item (more queue = faster fill)` |

### playerui/playerui_datacontext.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 6 | `PlayerUiDataContext` | `{}` |
| 69 | `_PlayerUI_RewardPlayback` | `{` |

### playerui/playerui_initialization.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUiInitialization` | `{` |

### playerui/playerui_ranking.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 21 | `_RANKING_STABILITY_THRESHOLD` | `15       -- score margin required to swap adjacent ranks` |
| 22 | `_RANKING_STABILITY_COOLDOWN` | `3.0       -- seconds between rank changes for same player` |
| 23 | `_RANKING_GLOBAL_REORDER_COOLDOWN` | `2.0  -- seconds between batch reorders` |
| 24 | `_RANKING_ROW_HEIGHT` | `34                -- pixels per player row` |
| 25 | `_RANKING_STAGGER_DELAY` | `0.05           -- seconds between staggered animations (50ms)` |
| 26 | `_RANKING_TRANSITION_CONVERGE` | `0.5      -- px threshold to consider animation converged` |
| 27 | `_RANKING_TRANSITION_TIMEOUT` | `2.0       -- seconds before force-releasing transition lock` |
| 28 | `_RANKING_EASEOUT_FACTOR` | `0.25          -- lerp factor per 0.1s tick (ease-out)` |
| 29 | `_RANKING_ELIMINATED_SENTINEL` | `-100000  -- ranking-only score for eliminated players (always below active)` |
| 30 | `_RANKING_CONTESTED_PULSE_PERIOD` | `0.6   -- seconds per full contested glow cycle` |
| 31 | `_RANKING_CONTESTED_PULSE_MIN` | `0.3      -- minimum glow opacity during pulse` |
| 32 | `_RANKING_CONTESTED_PULSE_PEAK` | `0.6     -- maximum glow opacity during pulse` |
| 33 | `_RANKING_CONTESTED_RESOLVE_FLASH_PEAK` | `0.5    -- highlight flash peak on contested→resolved transition` |
| 34 | `_RANKING_CONTESTED_RESOLVE_FLASH_DECAY` | `0.15  -- decay rate for contested→resolved flash` |
| 35 | `_RANKING_DIRECTIONAL_PULSE_PERIOD` | `0.8  -- seconds per full up/down glow cycle (calmer than contested)` |
| 36 | `_RANKING_DIRECTIONAL_PULSE_MIN` | `0.5     -- minimum directional glow opacity` |
| 37 | `_RANKING_DIRECTIONAL_PULSE_PEAK` | `0.9    -- maximum directional glow opacity` |
| 38 | `_RANKING_DIRECTIONAL_RESOLVE_FLASH_PEAK` | `0.4   -- flash peak on directional arrow clear/change` |
| 39 | `_RANKING_DIRECTIONAL_RESOLVE_FLASH_DECAY` | `0.18  -- decay rate for directional resolution flash` |
| 40 | `_RANKING_SHUFFLE_PULSE_PERIOD` | `0.4    -- seconds per shuffle-imminent pulse cycle (faster than directional)` |
| 41 | `_RANKING_SHUFFLE_PULSE_MIN` | `0.35      -- minimum shuffle-arrow opacity` |
| 42 | `_RANKING_SHUFFLE_PULSE_PEAK` | `0.85     -- maximum shuffle-arrow opacity` |
| 43 | `_RANKING_PULSE_LOOPS_PER_UPDATE` | `2       -- number of pulse cycles to run after each ranking update` |
| 44 | `_RANKING_DEBUG_FORCE_WINDOW` | `5.0         -- seconds debug-forced prediction state persists against recompute` |
| 47 | `RANK_CHANGE_NONE` | `"none"` |
| 48 | `RANK_CHANGE_MINOR` | `"minor"   -- moved 1 position` |
| 49 | `RANK_CHANGE_MAJOR` | `"major"   -- moved 2+ positions` |
| 52 | `_PlayerUI_RankState` | `nil  -- { teamLeft = {}, teamRight = {} }` |
| 53 | `_PlayerUI_RankTransitionLock` | `false` |
| 54 | `_PlayerUI_RankTransitionLockTime` | `0` |
| 55 | `_PlayerUI_RankLastGlobalReorder` | `0` |
| 56 | `_PlayerUI_RankPendingReorder` | `false` |
| 59 | `_RANKING_STATS_COLLAPSE_HITS` | `0              -- times contested collapse suppressed multi-arrows` |
| 60 | `_RANKING_STATS_COLLAPSE_BYPASSED_FORCE` | `0    -- times collapse skipped due to debug-force active` |
| 64 | `_RANKING_DEBUG_SCORE_INJECTION` | `nil` |
| 722 | `_RANKING_DEFERRED_TARGETS` | `{}` |
| 1786 | `_PLAYERUI_DEBUG_FWA_PENDING` | `nil` |

### playerui/playerui_rulesystem.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUiRuleSystem` | `{` |
| 97 | `_PlayerUI_DefaultFuncTable` | `{ Func = _PlayerUI_NoOp }` |
| 98 | `_PlayerUI_DefaultFuncMt` | `{ __index = function() return _PlayerUI_DefaultFuncTable end }` |

### playerui/playerui_settings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PLAYERUI_ENABLED` | `true` |
| 9 | `PlayerUI_Settings` | `{` |

### playerui/playerui_updateui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `_PlayerUI_DataContext` | `PlayerUiDataContext` |
| 13 | `_PLAYERUI_ELIM_TRANSFER_SUPPRESS_WARN_SEC` | `15.0` |
| 16 | `_PlayerUI_EliminationAnimTriggered` | `{}   -- keyed by playerIndex, true once animation triggered` |
| 436 | `PlayerUI_ResourceMapping` | `{` |
| 447 | `_PlayerUI_AgeIcons` | `{` |
| 458 | `_PlayerUI_RaceImage` | `{` |
| 476 | `_PLAYERUI_COLOR_WHITE` | `{ r = 255, g = 255, b = 255 }  -- score 0` |
| 477 | `_PLAYERUI_COLOR_YELLOW` | `{ r = 255, g = 255, b = 0   }  -- score 5000` |
| 478 | `_PLAYERUI_COLOR_ORANGE` | `{ r = 255, g = 165, b = 0   }  -- score 7500` |
| 479 | `_PLAYERUI_COLOR_RED` | `{ r = 255, g = 50,  b = 50  }  -- score 10000` |
| 1221 | `_PlayerUI_LimitsYellowRatio` | `(8 / 15)` |
| 1308 | `_PlayerUI_RewardIconFallback` | `"pack://application:,,,/WPFGUI;component/icons/races/common/buildings/keep.png"` |

### playerui/tracking/tracking_agingupprogress.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 8 | `PlayerUI_AgingUpProgress` | `{}` |

### playerui/tracking/tracking_gameobjectrepository.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUI_GameObjectRepository` | `{` |

### playerui/tracking/tracking_ownedsquads.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUI_OwnedSquads` | `{}` |

### playerui/tracking/tracking_populationcomposition.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUI_PopulationComposition` | `{}` |

### playerui/tracking/tracking_queuedstuff.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUI_QueuedStuff` | `{}` |

### playerui/tracking/tracking_reliclocations.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 7 | `PlayerUI_RelicLocations` | `{}` |

### playerui/uidatacontext/initialize_datacontext.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `PlayerUIDataContextMappings` | `{` |

## rewards

### rewards/cba_kill_scoring.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 12 | `CBA_KILL_POINTS` | `{` |

### rewards/cba_rewards.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 13 | `CBA_REWARDS_CBAULE` | `"CBA_Rewards"` |
| 14 | `_CBA` | `{` |
| 25 | `_reward_queue` | `{}` |

## root

### ags_global_settings.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 19 | `AGS_GS_TEAM_VICTORY_FFA` | `0` |
| 20 | `AGS_GS_TEAM_VICTORY_STANDARD` | `1` |
| 21 | `AGS_GS_TEAM_VICTORY_DYNAMIC` | `2` |
| 23 | `AGS_GS_SETTLEMENT_SCATTERED` | `0` |
| 24 | `AGS_GS_SETTLEMENT_NOMADIC` | `1` |
| 25 | `AGS_GS_SETTLEMENT_SETTLED` | `2` |
| 26 | `AGS_GS_SETTLEMENT_FORTIFIED` | `3` |
| 27 | `AGS_GS_SETTLEMENT_PILGRIMS` | `4` |
| 29 | `AGS_GS_TEAM_BALANCE_NONE` | `0` |
| 30 | `AGS_GS_TEAM_BALANCE_POPULATION` | `1` |
| 31 | `AGS_GS_TEAM_BALANCE_RESOURCES` | `2` |
| 32 | `AGS_GS_TEAM_BALANCE_FULL` | `3` |
| 34 | `AGS_TEAM_BALANCE_MAX_POP` | `400` |
| 36 | `AGS_GS_WONDER_SCALE_COST_DISABLED` | `-1` |
| 38 | `AGS_GS_TEAM_VISION_NONE` | `0` |
| 39 | `AGS_GS_TEAM_VISION_REQUIRES_MARKET` | `1` |
| 40 | `AGS_GS_TEAM_VISION_ALWAYS` | `2` |
| 42 | `AGS_GS_MAP_VISION_CONCEALED` | `0` |
| 43 | `AGS_GS_MAP_VISION_EXPLORED` | `1` |
| 44 | `AGS_GS_MAP_VISION_REVEALED` | `2` |
| 46 | `AGS_GS_AGE_NONE` | `0` |
| 47 | `AGS_GS_AGE_DARK` | `1` |
| 48 | `AGS_GS_AGE_FEUDAL` | `2` |
| 49 | `AGS_GS_AGE_CASTLE` | `3` |
| 50 | `AGS_GS_AGE_IMPERIAL` | `4` |
| 51 | `AGS_GS_AGE_LATE_IMPERIAL` | `5` |
| 53 | `AGS_GS_RESOURCES_NONE` | `0` |
| 54 | `AGS_GS_RESOURCES_LOW` | `1` |
| 55 | `AGS_GS_RESOURCES_NORMAL` | `2` |
| 56 | `AGS_GS_RESOURCES_MEDIUM` | `3` |
| 57 | `AGS_GS_RESOURCES_HIGH` | `4` |
| 58 | `AGS_GS_RESOURCES_VERY_HIGH` | `5` |
| 59 | `AGS_GS_RESOURCES_MAXIMUM` | `6` |
| 61 | `AGS_GS_TC_RESTRICTIONS_NONE` | `0` |
| 62 | `AGS_GS_TC_RESTRICTIONS_NORMAL` | `1` |
| 63 | `AGS_GS_TC_RESTRICTIONS_LANDMARKS` | `2` |
| 65 | `AGS_GS_HANDICAP_TYPE_DISABLED` | `0` |
| 66 | `AGS_GS_HANDICAP_TYPE_ECONOMIC` | `1` |
| 67 | `AGS_GS_HANDICAP_TYPE_MILITARY` | `2` |
| 68 | `AGS_GS_HANDICAP_TYPE_BOTH` | `3` |
| 70 | `AGS_GS_COLOR_BLUE` | `1 -- Azure Blue` |
| 71 | `AGS_GS_COLOR_RED` | `2 -- Red Orange` |
| 72 | `AGS_GS_COLOR_YELLOW` | `3 -- Citrine Yellow` |
| 73 | `AGS_GS_COLOR_GREEN` | `4 -- Vibrant Green` |
| 74 | `AGS_GS_COLOR_TURQUOISE` | `5 -- Bright Turquoise` |
| 75 | `AGS_GS_COLOR_PURPLE` | `6 -- Purple Mimosa` |
| 76 | `AGS_GS_COLOR_ORANGE` | `7 -- Blaze Orange` |
| 77 | `AGS_GS_COLOR_PINK` | `8 -- Hot Pink` |
| 78 | `AGS_GS_COLOR_GREY` | `9 -- Monsoon/Natural Grey` |
| 80 | `AGS_CBA_FIXED_MAX_PRODUCTION_BUILDINGS` | `15` |
| 81 | `AGS_CBA_FIXED_MAX_SIEGE_WORKSHOP` | `2` |
| 86 | `AGS_GS_LOCAL_PLAYER` | `nil` |
| 87 | `AGS_GLOBAL_SETTINGS_BUILD` | `"3.3"` |
| 88 | `AGS_GLOBAL_SETTINGS_MODULE` | `"AGS_GlobalSettings"` |
| 89 | `AGS_GLOBAL_SETTINGS` | `{` |

### cba_annihilation.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 18 | `_annihilation` | `{` |

### cba_religious.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 19 | `_religious` | `{` |

### cba.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 147 | `_onslaught_gameover_queued` | `false` |
| 150 | `_onslaught_teardown_detected` | `false` |
| 151 | `_onslaught_core_gameover_executed` | `false` |
| 152 | `_onslaught_trace_seq` | `0` |
| 153 | `_onslaught_probe_last_bucket` | `-1` |
| 154 | `_onslaught_enable_heartbeat_probe` | `false` |
| 277 | `_mod` | `{` |
| 1657 | `_PRECACHE_MANIFEST` | `nil` |
| 1661 | `_LEAVER_PRECACHE_ALWAYS_REQUIRED_BP` | `{` |
| 1709 | `_LEAVER_PRECACHE_TARGET_CIVS` | `{` |
| 1721 | `_LEAVER_PRECACHE_SELECTED_CIVS_BUILDINGS` | `{` |
| 1743 | `_LEAVER_LEGACY_PRECACHE_ENABLED` | `false` |
| 2115 | `_LEAVER_RESOURCE_TYPES` | `{ RT_Food, RT_Wood, RT_Gold, RT_Stone }` |
| 2120 | `_LEAVER_MILITARY_SUFFIX_OVERRIDE` | `{` |
| 2135 | `_LEAVER_DEBUG_BYPASS_GATES` | `false` |
| 2140 | `_LEAVER_DEBUG_BYPASS_CAPABILITY_GATES` | `false` |
| 2146 | `_LEAVER_DEBUG_VERBOSE` | `true` |
| 2150 | `_LEAVER_AUDIT_LOG` | `{}` |
| 2219 | `_LEAVER_AGE_REQUIREMENTS` | `{` |
| 2230 | `_LEAVER_CAPABILITY_REQUIREMENTS` | `{` |
| 2238 | `_LEAVER_SPAWNER_EXEMPT_PREFIXES` | `{` |
| 2255 | `_LEAVER_CAP_CACHE` | `{}` |
| 2351 | `_LEAVER_CIV_UNIQUE_FALLBACK` | `{` |
| 2482 | `_LEAVER_UNIT_ROLE_MAP` | `{` |
| 2511 | `_LEAVER_RECEIVER_CLASS_MAP` | `{` |
| 2704 | `_LEAVER_CANONICAL_ROLE` | `{` |
| 3713 | `_LEAVER_BATCH_BUILDINGS` | `10` |
| 3714 | `_LEAVER_BATCH_SQUADS` | `20` |
| 3717 | `_leaver_last_transfer_stats` | `nil` |
| 4247 | `_LEAVER_PERF_ANNIHILATION_CHECKS` | `0` |
| 4254 | `_LEAVER_RULES_PAUSED` | `false` |

### onslaught.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 77 | `_mod` | `{` |

### rewards.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `CBA_REWARDS_CBAULE` | `"CBA_Rewards"` |
| 10 | `_CBA` | `{` |

### wonder.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 18 | `_wonder` | `{` |

## specials

### specials/ags_match_ui.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_MATCH_UI_MODULE` | `"AGS_MatchUI"` |
| 11 | `AGS_MATCH_UI_OBJECTIVE_VISIBILITY` | `true` |
| 12 | `AGS_MATCH_UI_CONTEXT` | `{` |

### specials/ags_testing.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 10 | `AGS_TESTING_MODULE` | `"AGS_Testing"` |

### specials/ags_utilities.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 58 | `AGS_UTILITIES_MODULE` | `"AGS_Utilities"` |

## startconditions

### startconditions/ags_start_scattered.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 11 | `AGS_SCATTERED_MODULE` | `"AGS_Scattered"` |
| 12 | `AGS_SCATTERED_RADIUS` | `1` |
| 13 | `AGS_SCATTERED_TUNING` | `1.9` |
| 14 | `AGS_SCATTERED_WOOD` | `400` |
| 15 | `AGS_SCATTERED_STONE` | `300` |

### startconditions/nomad_start.scar

| Line | Variable | Value (truncated) |
|------|----------|--------------------|
| 9 | `_num_vils` | `3 -- number of vils to be spawned at the start of the game` |
| 10 | `_timer_one` | `180 -- Duration of treaty timer option one` |
| 11 | `_timer_two` | `300 -- Duration of treaty timer option two` |
| 12 | `_tcSpawned` | `{} -- Holds bools for if player has built a TC` |
| 13 | `options` | `{}` |

