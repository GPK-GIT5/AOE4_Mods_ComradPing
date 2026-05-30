# Onslaught Event Handler Map

Auto-generated on 2026-04-02 05:31. Maps game events, intervals, and one-shot rules to handler functions.

- **53** global event registrations (13 unique events)
- **24** interval rules
- **81** one-shot rules
- **125** unique handler functions
- **42** removal operations

## Game Event → Handler Matrix

| Event | Handlers | Files |
|-------|----------|-------|
| `GE_ConstructionComplete` | `Annihilation_OnConstructionComplete`, `AGS_Annihilation_OnConstructionComplete`, `AGS_Wonder_OnConstructionComplete`, `_ST_Interceptor_ConstructionComplete`, `AGS_AutoPop_OnConstructionComplete`, `AGS_LimitsUI_OnConstructionComplete`, `AGS_DockHouse_OnConstructionComplete`, `AGS_SpecialPopulationUI_OnConstructionComplete`, `CBA_AutoAge_ConstructionComplete`, `CBA_Options_AddScuttle_ConstructionComplete`, `CBA_Options_SiegeLimit_ConstructionComplete`, `Nomad_OnConstructionComplete`, `Wonder_OnConstructionComplete` | cba_annihilation.scar, conditions/ags_annihilation.scar, conditions/ags_wonder.scar, debug/cba_debug_siege_test.scar, gameplay/ags_auto_population.scar, gameplay/ags_limits_ui.scar, gameplay/ags_siege_house.scar, gameplay/ags_special_population_ui.scar, gameplay/cba_auto_age.scar, gameplay/cba_options.scar, startconditions/nomad_start.scar, wonder.scar |
| `GE_EntityKilled` | `Annihilation_OnEntityKilled`, `Mod_OnEntityKilled`, `AGS_Annihilation_OnEntityKilled`, `AGS_Wonder_OnEntityKilled`, `AGS_AutoPop_OnEntityKilled`, `AGS_LimitsUI_OnEntityKilled`, `AGS_DockHouse_OnEntityKilled`, `AGS_SpecialPopulationUI_OnEntityKilled`, `CBA_Options_BuildingLimit_OnEntityKilled`, `CBA_Options_SiegeLimit_EntityKilled`, `CBA_Rewards_OnEntityKilled`, `Wonder_OnEntityKilled` | cba_annihilation.scar, cba.scar, conditions/ags_annihilation.scar, conditions/ags_wonder.scar, gameplay/ags_auto_population.scar, gameplay/ags_limits_ui.scar, gameplay/ags_siege_house.scar, gameplay/ags_special_population_ui.scar, gameplay/cba_options.scar, rewards.scar, rewards/cba_rewards.scar, wonder.scar |
| `GE_ConstructionStart` | `AGS_Wonder_OnConstructionStart`, `_ST_Interceptor_ConstructionStart`, `CBA_Options_BuildingLimit_ConstructionStart`, `CBA_Options_SiegeLimit_ConstructionStart`, `Wonder_OnConstructionStart` | conditions/ags_wonder.scar, debug/cba_debug_siege_test.scar, gameplay/cba_options.scar, wonder.scar |
| `GE_SquadKilled` | `AGS_LimitsUI_OnSquadKilled`, `AGS_SpecialPopulationUI_OnSquadKilled`, `CBA_Options_SiegeLimit_SquadKilled`, `_OnSquadKilledRule` | gameplay/ags_limits_ui.scar, gameplay/ags_special_population_ui.scar, gameplay/cba_options.scar, observerui/tracking_squadlosses.scar |
| `GE_BuildItemComplete` | `AGS_LimitsUI_OnBuildItemComplete`, `AGS_SpecialPopulationUI_OnBuildItemComplete`, `CBA_Options_SiegeLimit_BuildItemComplete` | gameplay/ags_limits_ui.scar, gameplay/ags_special_population_ui.scar, gameplay/cba_options.scar |
| `GE_ConstructionCancelled` | `_ST_Interceptor_ConstructionCancelled`, `CBA_Options_BuildingLimit_ConstructionCancelled`, `CBA_Options_SiegeLimit_ConstructionCancelled` | debug/cba_debug_siege_test.scar, gameplay/cba_options.scar |
| `GE_DamageReceived` | `AGS_Annihilation_OnDamageReceived`, `AGS_Wonder_OnDamageReceived`, `Wonder_OnDamageReceived` | conditions/ags_annihilation.scar, conditions/ags_wonder.scar, wonder.scar |
| `GE_LocalPlayerChanged` | `AGS_GlobalSettings_OnLocalPlayerChanged`, `Religious_OnLocalPlayerChanged`, `Wonder_OnLocalPlayerChanged` | ags_global_settings.scar, cba_religious.scar, wonder.scar |
| `GE_EntityLandmarkDestroyed` | `Annihilation_OnLandmarkDestroyed`, `AGS_Annihilation_OnLandmarkDestroyed` | cba_annihilation.scar, conditions/ags_annihilation.scar |
| `GE_ProjectileFired` | `AGS_TreeBombardment_OnProjectileFired` | gameplay/ags_tree_bombardment.scar |
| `GE_ProjectileLanded` | `AGS_TreeBombardment_OnProjectileLanded` | gameplay/ags_tree_bombardment.scar |
| `GE_StrategicPointChanged` | `Religious_OnHolySiteChange` | cba_religious.scar |
| `GE_UpgradeComplete` | `CBA_AutoAge_UpgradeComplete` | gameplay/cba_auto_age.scar |

## Handler Lifecycle (Register / Remove Pairs)

| Handler | Registered | Removed | Balance |
|---------|------------|---------|---------|
| `_Debug_RewardCapture_Tick` | 1 | 2 | -1 |
| `_DebugIC_WaitForIdle` | 3 | 0 | +3 |
| `_DebugPrompt_PollTimeout` | 2 | 0 | +2 |
| `_OneRuleToRingThemAll_OnlyTrackWhenUpdatingUi` | 1 | 1 | balanced |
| `_OnSquadKilledRule` | 1 | 1 | balanced |
| `_PlayerUI_Animate_Tick` | 1 | 1 | balanced |
| `_PlayerUI_RingRule` | 1 | 1 | balanced |
| `_QA_WaitForPrompt` | 1 | 0 | +1 |
| `_ST_Interceptor_ConstructionCancelled` | 1 | 0 | +1 |
| `_ST_Interceptor_ConstructionComplete` | 1 | 0 | +1 |
| `_ST_Interceptor_ConstructionStart` | 1 | 0 | +1 |
| `_Visual_PollResolution` | 1 | 0 | +1 |
| `AGS_Annihilation_OnConstructionComplete` | 1 | 1 | balanced |
| `AGS_Annihilation_OnDamageReceived` | 1 | 1 | balanced |
| `AGS_Annihilation_OnEntityKilled` | 1 | 1 | balanced |
| `AGS_Annihilation_OnLandmarkDestroyed` | 1 | 1 | balanced |
| `AGS_AutoPop_OnConstructionComplete` | 1 | 0 | +1 |
| `AGS_AutoPop_OnEntityKilled` | 1 | 0 | +1 |
| `AGS_AutoResources` | 1 | 0 | +1 |
| `AGS_DockHouse_OnConstructionComplete` | 1 | 1 | balanced |
| `AGS_DockHouse_OnEntityKilled` | 1 | 1 | balanced |
| `AGS_GlobalSettings_OnLocalPlayerChanged` | 1 | 1 | balanced |
| `AGS_LimitsUI_OnBuildItemComplete` | 1 | 1 | balanced |
| `AGS_LimitsUI_OnConstructionComplete` | 1 | 1 | balanced |
| `AGS_LimitsUI_OnEntityKilled` | 1 | 1 | balanced |
| `AGS_LimitsUI_OnSquadKilled` | 1 | 1 | balanced |
| `AGS_PopulationAutomatic_ReconcileCapDrift` | 1 | 0 | +1 |
| `AGS_SpecialPopulationUI_OnBuildItemComplete` | 1 | 1 | balanced |
| `AGS_SpecialPopulationUI_OnConstructionComplete` | 1 | 1 | balanced |
| `AGS_SpecialPopulationUI_OnEntityKilled` | 1 | 1 | balanced |
| `AGS_SpecialPopulationUI_OnSquadKilled` | 1 | 1 | balanced |
| `AGS_TreeBombardment_OnProjectileFired` | 1 | 1 | balanced |
| `AGS_TreeBombardment_OnProjectileLanded` | 1 | 1 | balanced |
| `AGS_Wonder_OnConstructionComplete` | 1 | 1 | balanced |
| `AGS_Wonder_OnConstructionStart` | 1 | 1 | balanced |
| `AGS_Wonder_OnDamageReceived` | 1 | 1 | balanced |
| `AGS_Wonder_OnEntityKilled` | 1 | 1 | balanced |
| `Annihilation_OnConstructionComplete` | 1 | 2 | -1 |
| `Annihilation_OnEntityKilled` | 1 | 1 | balanced |
| `Annihilation_OnLandmarkDestroyed` | 1 | 1 | balanced |
| `CBA_AutoAge_ConstructionComplete` | 1 | 0 | +1 |
| `CBA_AutoAge_UpdateTimer` | 1 | 0 | +1 |
| `CBA_AutoAge_UpgradeComplete` | 1 | 0 | +1 |
| `CBA_Options_AddScuttle_ConstructionComplete` | 1 | 0 | +1 |
| `CBA_Options_BuildingLimit_ConstructionCancelled` | 1 | 0 | +1 |
| `CBA_Options_BuildingLimit_ConstructionStart` | 1 | 0 | +1 |
| `CBA_Options_BuildingLimit_OnEntityKilled` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_BuildItemComplete` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_ConstructionCancelled` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_ConstructionComplete` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_ConstructionStart` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_EntityKilled` | 1 | 0 | +1 |
| `CBA_Options_SiegeLimit_SquadKilled` | 1 | 0 | +1 |
| `CBA_Options_VillagerSpawner` | 1 | 0 | +1 |
| `CBA_Rewards_OnEntityKilled` | 2 | 0 | +2 |
| `Mod_OnEntityKilled` | 1 | 0 | +1 |
| `Nomad_OnConstructionComplete` | 1 | 0 | +1 |
| `Onslaught_CrashProbeTick` | 1 | 0 | +1 |
| `Onslaught_SyncScoreToEngine` | 1 | 0 | +1 |
| `Religious_FlashAllHolySites` | 1 | 0 | +1 |
| `Religious_HolySiteMinimapBlips` | 1 | 0 | +1 |
| `Religious_OnHolySiteChange` | 1 | 0 | +1 |
| `Religious_OnLocalPlayerChanged` | 1 | 0 | +1 |
| `statechange` | 3 | 0 | +3 |
| `Wonder_CheckVictory` | 1 | 0 | +1 |
| `Wonder_OnConstructionComplete` | 1 | 1 | balanced |
| `Wonder_OnConstructionStart` | 1 | 1 | balanced |
| `Wonder_OnDamageReceived` | 1 | 1 | balanced |
| `Wonder_OnEntityKilled` | 1 | 1 | balanced |
| `Wonder_OnLocalPlayerChanged` | 1 | 1 | balanced |
| `Wonder_Update` | 1 | 1 | balanced |

## Interval Rules

| Handler | Interval | File | Line |
|---------|----------|------|------|
| `_Debug_RewardCapture_Tick` | 0.10s | debug/cba_debug_playerui_anim.scar | 2759 |
| `_DebugIC_WaitForIdle` | 1.0s | debug/cba_debug_ui_prompts.scar | 824 |
| `_DebugIC_WaitForIdle` | 1.0s | debug/cba_debug_ui_prompts.scar | 853 |
| `_DebugIC_WaitForIdle` | 1.0s | debug/cba_debug_ui_prompts.scar | 848 |
| `_DebugPrompt_PollTimeout` | 1.0s | debug/cba_debug_ui_prompts.scar | 420 |
| `_DebugPrompt_PollTimeout` | 1.0s | debug/cba_debug_ui_prompts.scar | 335 |
| `_OneRuleToRingThemAll_OnlyTrackWhenUpdatingUi` | 0.5s | observerui/observeruirulesystem.scar | 15 |
| `_PlayerUI_Animate_Tick` | 0.1s | playerui/playerui_animate.scar | 329 |
| `_PlayerUI_RingRule` | 1.0s | playerui/playerui_rulesystem.scar | 29 |
| `_QA_WaitForPrompt` | 1.0s | debug/cba_debug_qa_runner.scar | 523 |
| `_Visual_PollResolution` | 0.5s | debug/cba_debug_helpers.scar | 427 |
| `AGS_AutoResources` | 60s | gameplay/ags_auto_resources.scar | 25 |
| `AGS_PopulationAutomatic_ReconcileCapDrift` | 5s | gameplay/ags_auto_population.scar | 156 |
| `CBA_AutoAge_UpdateTimer` | 1s | gameplay/cba_auto_age.scar | 74 |
| `CBA_Options_VillagerSpawner` | 20s | gameplay/cba_options.scar | 110 |
| `Onslaught_CrashProbeTick` | 1s | cba.scar | 469 |
| `Onslaught_SyncScoreToEngine` | 2s | cba.scar | 463 |
| `Religious_FlashAllHolySites` | 1s | cba_religious.scar | 347 |
| `Religious_HolySiteMinimapBlips` | 5s | cba_religious.scar | 345 |
| `statechange` | 600s | onslaught.scar | 199 |
| `statechange` | 1800s | day night cycle.scar | 57 |
| `statechange` | 600s | cba.scar | 448 |
| `Wonder_CheckVictory` | 1.0s | wonder.scar | 138 |
| `Wonder_Update` | 1.0s | wonder.scar | 137 |

## OneShot Rules (Top 30 by Frequency)

| Handler | Delay | Count | Example File |
|---------|-------|-------|-------------|
| `Wonder_CreateEventCue` | 0s | 8 | wonder.scar |
| `_Leaver_ContinueTransfer` | 0s | 5 | cba.scar |
| `_VisualTest_NextPhase` | 0.1s | 5 | debug/cba_debug_leaver.scar |
| `_LeaverPerf_CascadeNext` | 0s | 3 | debug/cba_debug_leaver.scar |
| `_Debug_Run_PlayerUI_PhaseBSuite_Step` | 0.1s | 3 | debug/cba_debug_helpers.scar |
| `_Ranking_CheckTransitionConverged` | 0.5s | 2 | playerui/playerui_ranking.scar |
| `_LeaverMilTest_Finalize` | 0s | 2 | debug/cba_debug_leaver.scar |
| `_LeaverDebug_FullSystemFinalize` | 0s | 2 | debug/cba_debug_leaver.scar |
| `Religious_StopMusic` | 1s | 2 | cba_religious.scar |
| `Religious_DelayedNewObjective` | 0s | 2 | cba_religious.scar |
| `_LeaverDebug_FullFinalize` | 0s | 2 | debug/cba_debug_leaver.scar |
| `CBA_Rewards_InitialSpawnWhenReady` | 1s | 2 | rewards/cba_rewards.scar |
| `_VisualTest_DeferredCleanupStep` | 0.05s | 2 | debug/cba_debug_leaver.scar |
| `_VisualKeepDestroy_Execute` | 1.0s | 1 | debug/cba_debug_helpers.scar |
| `_VisualTest_DeferredCleanup` | 0.5s | 1 | debug/cba_debug_leaver.scar |
| `AddLandmarkHintpoint` | 2s | 1 | gameplay/cba_training.scar |
| `AGS_AutoPop_RunDeferredReconcile` | 0.25s | 1 | gameplay/ags_auto_population.scar |
| `AGS_LimitsUI_Update` | 0.5s | 1 | gameplay/ags_limits_ui.scar |
| `AGS_PopulationAutomatic_CompensateInnate` | 1s | 1 | gameplay/ags_auto_population.scar |
| `CBA_Options_SiegeLimit_RunDeferredRecheck` | 0.25s | 1 | gameplay/cba_options.scar |
| `CBA_Rewards_SpawnUnits` | 1s | 1 | rewards.scar |
| `CBA_Rewards_StartingUnits` | 1s | 1 | rewards.scar |
| `toDawn` | 1200s | 1 | day night cycle.scar |
| `toDay` | 1500s | 1 | day night cycle.scar |
| `toDusk` | 0s | 1 | day night cycle.scar |
| `toDusk2` | 300s | 1 | day night cycle.scar |
| `toNight` | 600s | 1 | day night cycle.scar |
| `_QA_T6_AskQ2` | 1.0s | 1 | debug/cba_debug_qa_runner.scar |
| `_QA_T6_AskQ1` | 1.0s | 1 | debug/cba_debug_qa_runner.scar |
| `_QA_T2_Ask` | 1.5s | 1 | debug/cba_debug_qa_runner.scar |

