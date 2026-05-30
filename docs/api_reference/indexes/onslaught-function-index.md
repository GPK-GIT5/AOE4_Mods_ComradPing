# Onslaught Function Index

Auto-generated on 2026-04-02 05:31. Total functions: **1746**

- **conditions**: 68 functions across 4 files
- **debug**: 678 functions across 28 files
- **gameplay**: 291 functions across 21 files
- **helpers**: 52 functions across 3 files
- **observerui**: 156 functions across 25 files
- **playerui**: 216 functions across 13 files
- **rewards**: 18 functions across 4 files
- **root**: 220 functions across 8 files
- **specials**: 29 functions across 3 files
- **startconditions**: 18 functions across 2 files

Visibility: **1178** public, **419** private (_ prefix), **149** local

## conditions

### conditions/ags_annihilation.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 34 | `AGS_Annihilation_UpdateModuleSettings` | — | public |
| 41 | `AGS_Annihilation_PresetFinalize` | — | public |
| 46 | `AGS_Annihilation_OnPlay` | — | public |
| 55 | `AGS_Annihilation_TreatyStarted` | — | public |
| 60 | `AGS_Annihilation_TreatyEnded` | — | public |
| 65 | `AGS_Annihilation_OnPlayerDefeated` | player, reason | public |
| 77 | `AGS_Annihilation_OnObjectiveToggle` | toggle | public |
| 84 | `AGS_Annihilation_OnGameOver` | — | public |
| 97 | `AGS_Annihilation_OnDamageReceived` | context | public |
| 104 | `AGS_Annihilation_OnEntityKilled` | context | public |
| 110 | `AGS_Annihilation_OnLandmarkDestroyed` | context | public |
| 116 | `AGS_Annihilation_OnConstructionComplete` | context | public |
| 133 | `AGS_Annihilation_CreateObjective` | — | public |
| 138 | `AGS_Annihilation_RemoveObjective` | — | public |
| 142 | `AGS_Annihilation_Eliminate` | player | public |
| 153 | `AGS_Annihilation_CheckAnnihilation` | player_id | public |
| 173 | `AGS_Annihilation_AreOnlyValidSquads` | player, squad_count | public |
| 199 | `AGS_Annihilation_DefineCheapestSquads` | — | public |
| 213 | `AGS_Annihilation_IsAbleToProduce` | player | public |
| 287 | `AGS_Annihilation_PlayerCanReceiveTribute` | player_id | public |
| 289 | `PlayerCanSendTribute` | player_id | local |

### conditions/ags_elimination.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 23 | `AGS_Elimination_UpdateModuleSettings` | — | public |
| 30 | `AGS_Elimination_OnPlayerAITakeover` | context | public |
| 60 | `AGS_Elimination_OnPlayerDefeated` | player, reason | public |

### conditions/ags_surrender.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 23 | `AGS_Surrender_UpdateModuleSettings` | — | public |
| 30 | `AGS_Surrender_OnPlay` | — | public |
| 47 | `AGS_Surrender_OnSurrenderMatchRequested` | — | public |
| 53 | `AGS_Surrender_OnPlayerDefeated` | player, reason | public |
| 84 | `AGS_Surrender_Notify` | player_id | public |
| 94 | `AGS_Surrender_CheckAI` | — | public |

### conditions/ags_wonder.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 35 | `AGS_Wonder_UpdateModuleSettings` | — | public |
| 46 | `AGS_Wonder_OnPlay` | — | public |
| 59 | `AGS_Wonder_TreatyStarted` | — | public |
| 66 | `AGS_Wonder_TreatyEnded` | — | public |
| 72 | `AGS_Wonder_OnPlayerDefeated` | player, reason | public |
| 82 | `AGS_Wonder_OnRelationshipChanged` | observer_id, target_id | public |
| 109 | `AGS_Wonder_OnObjectiveToggle` | toggle | public |
| 116 | `AGS_Wonder_OnGameOver` | — | public |
| 132 | `AGS_Wonder_OnDamageReceived` | context | public |
| 168 | `AGS_Wonder_OnConstructionStart` | context | public |
| 172 | `AGS_Wonder_OnConstructionComplete` | context | public |
| 176 | `AGS_Wonder_Construction` | context, construction_callback | public |
| 201 | `AGS_Wonder_ConstructionStarted` | player, entity_id | public |
| 209 | `AGS_Wonder_ConstructionCompleted` | player, entity_id | public |
| 215 | `AGS_Wonder_OnEntityKilled` | context | public |
| 251 | `AGS_Wonder_OnTimerTick` | — | public |
| 270 | `AGS_Wonder_InitializeWonders` | — | public |
| 284 | `AGS_Wonder_EnableConstruction` | is_enabled | public |
| 290 | `AGS_Wonder_DeactivateTimers` | — | public |
| 298 | `AGS_Wonder_RemoveAllObjectives` | — | public |
| 303 | `AGS_Wonder_CreateTimerObjective` | owner | public |
| 325 | `AGS_Wonder_UpdateTimerObjectives` | — | public |
| 334 | `AGS_Wonder_UpdateWonderTimer` | player | public |
| 341 | `AGS_Wonder_RemoveTimerObjectives` | — | public |
| 349 | `AGS_Wonder_CreateBuildObjective` | — | public |
| 354 | `AGS_Wonder_RemoveBuildObjective` | — | public |
| 358 | `AGS_Wonder_FailTimerObjective` | owner | public |
| 367 | `AGS_Wonder_WarnEveryone` | owner, objective, relation, objective_template | public |
| 376 | `AGS_Wonder_StartCountdown` | owner | public |
| 390 | `AGS_Wonder_CreateTimerNotifications` | player | public |
| 398 | `AGS_Wonder_ResetTimerObjective` | player | public |
| 412 | `AGS_Wonder_CleanWonder` | player | public |
| 434 | `AGS_Wonder_VictoryTriggered` | winner | public |
| 457 | `AGS_Wonder_TryDeclareWinners` | — | public |
| 467 | `AGS_Wonder_InformNegativeProgressChange` | owner | public |
| 488 | `AGS_Wonder_Destroyed` | owner | public |
| 503 | `AGS_Wonder_TimerUpdate` | — | public |
| 516 | `AGS_Wonder_TimerProgressNotification` | player | public |

## debug

### debug/cba_debug_advanced_stress.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 21 | `Debug_AdvStress_SiegeCascade` | — | public |
| 43 | `validate_fn` | p, c, bp | public |
| 48 | `validate_fn` | p, c, bp | public |
| 53 | `validate_fn` | p, c, bp | public |
| 58 | `validate_fn` | p, c, bp | public |
| 67 | `_AdvStress_Hook_SiegeState` | — | private |
| 70 | `_AdvStress_Hook_LimitsUI` | — | private |
| 84 | `Debug_AdvStress_RapidElimination` | — | public |
| 110 | `_AdvStress_Hook_Balance` | — | private |
| 113 | `_AdvStress_Hook_PostDefeat` | — | private |
| 117 | `_RapidElim_DestroyP2` | — | private |
| 131 | `_RapidElim_DestroyP3` | — | private |
| 145 | `_RapidElim_DestroyP4` | — | private |
| 154 | `_RapidElim_FinalReport` | — | private |
| 177 | `Debug_AdvStress_BuildingLimitOscillation` | — | public |
| 248 | `Debug_AdvStress_MaxPopPressure` | — | public |
| 324 | `Debug_AdvStress_BlueprintStorm` | — | public |
| 410 | `Debug_AdvStress_ConcurrentThrash` | — | public |
| 510 | `Debug_AdvancedStressAll` | — | public |
| 527 | `_AdvStressAll_Phase2` | — | private |
| 532 | `_AdvStressAll_Phase3` | — | private |
| 537 | `_AdvStressAll_Phase4` | — | private |
| 542 | `_AdvStressAll_Phase5` | — | private |
| 549 | `_AdvStressAll_Phase6` | — | private |
| 556 | `_AdvStressAll_FinalReport` | — | private |

### debug/cba_debug_ai_behavior.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 54 | `_AI_ScenarioHeader` | num | local |
| 61 | `_AI_ScenarioFooter` | num | local |
| 80 | `_AI_Scenario1_TargetPriority` | — | private |
| 120 | `_AI_S1_Ask` | — | private |
| 127 | `_AI_S1_OnAnswer` | choice | private |
| 142 | `_AI_Scenario2_ResourceBehavior` | — | private |
| 170 | `_AI_S2_Ask` | — | private |
| 177 | `_AI_S2_OnAnswer` | choice | private |
| 192 | `_AI_Scenario3_PopulationCap` | — | private |
| 226 | `_AI_S3_Ask` | — | private |
| 233 | `_AI_S3_OnAnswer` | choice | private |
| 248 | `_AI_Scenario4_MultiThreat` | — | private |
| 278 | `_AI_S4_Ask` | — | private |
| 285 | `_AI_S4_OnAnswer` | choice | private |
| 300 | `_AI_Scenario5_SiegeResponse` | — | private |
| 326 | `_AI_S5_Ask` | — | private |
| 333 | `_AI_S5_OnAnswer` | choice | private |
| 348 | `_AI_Scenario6_Recovery` | — | private |
| 383 | `_AI_S6_Ask` | — | private |
| 390 | `_AI_S6_OnAnswer` | choice | private |
| 405 | `_AI_Scenario7_HolySiteContest` | — | private |
| 427 | `_AI_S7_Ask` | — | private |
| 434 | `_AI_S7_AskTheoretical` | — | private |
| 441 | `_AI_S7_OnAnswer` | choice | private |
| 456 | `_AI_Scenario8_StateAudit` | — | private |
| 508 | `_AI_S8_AskQ1` | — | private |
| 515 | `_AI_S8_OnAnswer` | choice | private |
| 545 | `Debug_AIBehavior_Scenario` | n | public |
| 567 | `Debug_AIBehavior` | — | public |
| 588 | `_AI_RunNextScenario` | — | private |
| 612 | `_AI_OnScenarioComplete` | — | private |
| 621 | `_AI_FinalReport` | — | private |
| 652 | `Debug_AIBehaviorStatus` | — | public |

### debug/cba_debug_autopop.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 17 | `Debug_AutoPop_FullValidation` | — | public |
| 54 | `Debug_AutoPop_CheckBuildingLocks` | — | public |
| 114 | `Debug_AutoPop_CheckUpgradeLocks` | — | public |
| 126 | `Debug_AutoPop_CheckCapAlignment` | — | public |
| 174 | `Debug_AutoPop_CheckReconcilerState` | — | public |
| 211 | `Debug_AutoPop_PrintSummary` | — | public |
| 249 | `Debug_AutoPop_CheckEventDriven` | — | public |
| 279 | `Debug_AutoPop_CheckRewardSuppression` | — | public |
| 309 | `Debug_ValidateAutoPopulation` | — | public |
| 314 | `debug_autopop` | — | public |

### debug/cba_debug_blueprint_audit.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 14 | `Debug_BlueprintAudit` | — | public |
| 121 | `Debug_BlueprintAudit_Civ` | civ_name | public |
| 180 | `Debug_DumpBlueprintsForSuffix` | suffix | public |
| 226 | `Debug_BlueprintAudit_LeaverFallback` | — | public |
| 337 | `Debug_EnumerateAllCivUnits` | opt_civ | public |
| 419 | `debug.data.run` | — | public |

### debug/cba_debug_civ_overview.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 37 | `_CivOverview_SortedKeys` | tbl | private |
| 44 | `_CivOverview_BPExists` | bp_name | private |
| 67 | `_CivOverview_GetSource` | table_ref, civ, parent_map | private |
| 78 | `_CivOverview_BuildCivSet` | — | private |
| 87 | `Debug_CivOverview_Build` | — | public |
| 250 | `_CivOverview_RequireBuild` | — | private |
| 257 | `Debug_CivOverview_Summary` | — | public |
| 271 | `Debug_CivOverview_Civ` | civ | public |
| 294 | `Debug_CivOverview_Audit` | — | public |
| 311 | `Debug_CivOverview_DumpStructured` | include_entries | public |

### debug/cba_debug_comprehensive_stress.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 55 | `_CS_CatHeader` | num | local |
| 62 | `_CS_CatFooter` | num | local |
| 82 | `_CS_Cat1_BootIntegrity` | — | private |
| 160 | `_CS_Cat2_EconomyStress` | — | private |
| 260 | `_CS_Cat3_BuildingLimitGauntlet` | — | private |
| 340 | `_CS_Cat4_SiegeLimitCascade` | — | private |
| 432 | `_CS_Cat5_WinConditionMatrix` | — | private |
| 509 | `_CS_Cat6_AutoAgePipeline` | — | private |
| 574 | `_CS_Cat7_RewardIntegrity` | — | private |
| 649 | `_CS_Cat8_LeaverResilience` | — | private |
| 728 | `_CS_Cat9_EventPipelineFuzz` | — | private |
| 803 | `_CS_Cat10_VisualStateVerification` | — | private |
| 813 | `_CS_Visual_Phase1` | — | private |
| 822 | `_CS_Visual_Phase1_Answer` | choice | private |
| 831 | `_CS_Visual_Phase2_Start` | — | private |
| 849 | `_CS_Visual_Phase2_Answer` | choice | private |
| 858 | `_CS_Visual_Phase3_Start` | — | private |
| 879 | `_CS_Visual_Phase3_Ask` | — | private |
| 886 | `_CS_Visual_Phase3_Answer` | choice | private |
| 895 | `_CS_Visual_Phase4_Start` | — | private |
| 923 | `_CS_Visual_Phase4_Answer` | choice | private |
| 932 | `_CS_Visual_Finish` | — | private |
| 957 | `_CS_Cat11_ExtremeEdgeCases` | — | private |
| 1083 | `_CS_Cat12_RuntimeStability` | — | private |
| 1113 | `nest` | n | local |
| 1221 | `Debug_ComprehensiveStress_Cat` | n | public |
| 1251 | `Debug_ComprehensiveStress` | — | public |
| 1270 | `_CS_RunNextCategory` | — | private |
| 1298 | `_CS_OnCat10Complete` | — | private |
| 1307 | `_CS_FinalReport` | — | private |
| 1357 | `Debug_ComprehensiveStressStatus` | — | public |
| 1369 | `Debug_ComprehensiveStressStop` | — | public |

### debug/cba_debug_core.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 65 | `CBA_Debug_UpdateModuleSettings` | options | public |
| 73 | `CBA_Debug_EarlyInitializations` | — | public |
| 81 | `DebugLog` | area, msg | public |
| 96 | `DebugLog_SetFilter` | ... | public |
| 111 | `_Debug_RunTest` | name, test_fn | private |
| 136 | `_Debug_ResetPhaseTracking` | — | private |
| 146 | `_Debug_SetPhaseCounterGetter` | getter | private |
| 154 | `_Debug_PhaseHeader` | phase_num, phase_name | private |
| 180 | `_Debug_PhaseFooter` | phase_num, phase_name | private |
| 220 | `_Debug_TableExists` | name, ref | private |
| 225 | `_Debug_FunctionExists` | fn_name | private |
| 230 | `_Debug_CountKeys` | tbl | private |
| 236 | `_Debug_GetPlayerCiv` | player | private |
| 245 | `_Debug_EndMarker` | suite_name, passed, total, elapsed_seconds | private |
| 299 | `Debug_StepMode` | enabled | public |
| 308 | `Debug_Continue` | — | public |
| 321 | `Debug_Skip` | — | public |
| 331 | `Debug_StepStatus` | — | public |
| 345 | `_Debug_ScheduleNextPhase` | next_fn, delay, phase_name, suite_name | private |
| 364 | `Debug_RegisterHook` | name, fn | public |
| 373 | `Debug_FireHook` | name | public |
| 386 | `Debug_ListHooks` | — | public |
| 397 | `Debug_ClearHooks` | — | public |
| 409 | `Debug_RunAll` | step | public |
| 451 | `Debug_RunFullValidation` | — | public |
| 477 | `_Debug_MasterEnqueue` | fn, end_marker | private |
| 481 | `_Debug_MasterRunSmoke` | — | private |
| 486 | `_Debug_MasterAdvance` | — | private |
| 507 | `_Debug_MasterFinalReport` | — | private |
| 545 | `_Debug_SubStart` | name | private |
| 558 | `_Debug_SubEnqueue` | fn, end_marker | private |
| 563 | `_Debug_SubLaunch` | — | private |
| 572 | `_Debug_SubAdvance` | — | private |
| 593 | `_Debug_SubFinalReport` | — | private |
| 625 | `_Debug_LogCommandFailure` | command_name, reason | private |
| 671 | `debug._register` | tag, handler, desc, tier | public |
| 692 | `debug.run` | tag | public |
| 724 | `debug.unlock` | — | public |
| 736 | `debug.list` | filter | public |
| 759 | `debug.status` | — | public |
| 806 | `debug._safety.include_human` | — | public |
| 813 | `debug._safety.exclude_human_reset` | — | public |
| 822 | `debug._safety.validate_target` | player_index | public |
| 847 | `debug._safety.is_test_lobby` | — | public |

### debug/cba_debug_coverage.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 19 | `_Cov_RunTest` | name, test_fn | private |
| 34 | `_Cov_BatchHeader` | num, name | private |
| 43 | `_Cov_Batch1_EngineAPI` | — | private |
| 68 | `_Cov_Batch2_BlueprintResolution` | — | private |
| 97 | `_Cov_Batch3_Economy` | — | private |
| 130 | `_Cov_Batch4_TeamPlayer` | — | private |
| 158 | `_Cov_Batch5_Options` | — | private |
| 186 | `_Cov_Batch6_Rewards` | — | private |
| 217 | `_Cov_Batch7_Objectives` | — | private |
| 239 | `_Cov_Batch8_WinConditions` | — | private |
| 275 | `_Cov_Batch9_AutoSystems` | — | private |
| 300 | `_Cov_Batch10_DebugSelfTest` | — | private |
| 337 | `_Cov_FinalReport` | — | private |
| 363 | `Debug_CoverageTest` | — | public |
| 382 | `_Cov_Run2` | — | private |
| 386 | `_Cov_Run3` | — | private |
| 390 | `_Cov_Run4` | — | private |
| 394 | `_Cov_Run5` | — | private |
| 398 | `_Cov_Run6` | — | private |
| 402 | `_Cov_Run7` | — | private |
| 406 | `_Cov_Run8` | — | private |
| 410 | `_Cov_Run9` | — | private |
| 414 | `_Cov_Run10` | — | private |
| 419 | `Debug_CoverageBatch` | n | public |

### debug/cba_debug_data_extract.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 23 | `_DataExtract_SafeCall` | fn, ... | private |
| 29 | `_DataExtract_CostToString` | cost_table | private |
| 45 | `_DataExtract_GetAllRaces` | — | private |
| 66 | `Debug_DataExtract_AllBlueprints` | — | public |
| 127 | `Debug_DataExtract_RaceSquads` | — | public |
| 166 | `Debug_DataExtract_BuildingData` | — | public |
| 210 | `Debug_DataExtract_UnitCosts` | — | public |
| 283 | `Debug_DataExtract_Summary` | — | public |

### debug/cba_debug_destructive.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 15 | `_Debug_Destructive_IsLocalPlayerIndex` | player_idx | local |
| 30 | `_Debug_Destructive_RejectLocalTarget` | commandName, player_idx | local |
| 38 | `Debug_ForceKeepDestroy` | player_idx | public |
| 85 | `Debug_ForceEliminatePlayer` | player_idx | public |
| 125 | `Debug_ForceSurrender` | player_idx | public |
| 158 | `Debug_ForceTransferTest` | src_idx, dst_idx | public |
| 214 | `Debug_ValidateSpawnAnchors` | — | public |
| 241 | `debug.players.forceKeepDestroy` | idx | public |
| 245 | `debug.players.forceEliminate` | idx | public |
| 249 | `debug.players.forceSurrender` | idx | public |
| 253 | `debug.players.forceTransfer` | src, dst | public |

### debug/cba_debug_event_probes.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 15 | `_EP_MockContext_EntityKilled` | victim_eid, victim_owner, killer_owner | private |
| 23 | `_EP_MockContext_ConstructionStart` | entity, player | private |
| 30 | `_EP_MockContext_UpgradeComplete` | player, upgrade | private |
| 37 | `_EP_MockContext_BuildItemComplete` | player, entity | private |
| 44 | `_EP_MockContext_StrategicPointChanged` | entity | private |
| 54 | `_EP_Group_EntityKilled` | results | private |
| 87 | `_EP_Group_Construction` | results | private |
| 125 | `_EP_Group_WinConditions` | results | private |
| 151 | `_EP_Group_SiegeLimits` | results | private |
| 180 | `Debug_EventProbes` | — | public |

### debug/cba_debug_helpers.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 13 | `Debug_SetBaseline` | amount | public |
| 28 | `Debug_GetKillScore` | player_idx | public |
| 46 | `Debug_GetAutoAgeStatus` | — | public |
| 67 | `Debug_GetPopCap` | player_idx | public |
| 92 | `Debug_PopAudit` | — | public |
| 123 | `Debug_KeepDiagnostic` | — | public |
| 153 | `Debug_PrecacheStatus` | — | public |
| 181 | `Debug_Spawn` | bp_name, player_idx, count | public |
| 212 | `_Debug_GetPlayerSpawnAnchor` | player | private |
| 220 | `_Debug_ClampToPlayableBounds` | base_pos, dx, dz, margin | private |
| 248 | `_Debug_GetSafePosFromAnchor` | anchor, offsets, margin, ref_entity, ref_ebp | private |
| 288 | `_Debug_GetRamBaselineTotals` | player | private |
| 301 | `_Debug_LogRamBaseline` | player, label | private |
| 312 | `Debug_RunSmokeTests` | — | public |
| 405 | `Debug_WaitForVisual` | description, timeout_seconds | public |
| 430 | `_Visual_PollResolution` | — | private |
| 463 | `_Visual_Resume` | — | private |
| 471 | `Debug_Confirm` | — | public |
| 479 | `Debug_Reject` | reason | public |
| 492 | `Debug_FocusPlayer` | player_idx | public |
| 509 | `Debug_FocusPosition` | x, y, z | public |
| 520 | `Debug_SlowMotion` | enabled | public |
| 530 | `Debug_PauseAI` | — | public |
| 537 | `Debug_ResumeAI` | — | public |
| 544 | `Debug_ToggleOverlays` | — | public |
| 554 | `Debug_VisualValidation_KeepDestroy` | player_idx | public |
| 571 | `_VisualKeepDestroy_Execute` | — | private |
| 595 | `_VisualKeepDestroy_Finish` | — | private |
| 600 | `Debug_VisualValidation_SiegeSpawn` | player_idx | public |
| 633 | `_Debug_GetAgeUnlockMode` | civ | private |
| 652 | `Debug_ValidateAgeGateCoverage` | silent | public |
| 715 | `_Debug_GetDefaultPlayerIndex` | player_idx | private |
| 753 | `Debug_ListPlayerSlots` | — | public |
| 796 | `Debug_Demo_RewardPlayback` | player_idx, kill_grant | public |
| 865 | `Debug_Get_RewardPlaybackState` | player_idx | public |
| 933 | `Debug_Get_RewardHealthSummary` | player_idx | public |
| 1060 | `Debug_Get_EliminationSettleState` | — | public |
| 1140 | `_Debug_PlayerUI_ReadableName` | slot | local |
| 1163 | `Debug_Get_RankingAnimKeyAudit` | — | public |
| 1206 | `Debug_Get_RankingOverview` | — | public |
| 1273 | `_Debug_Run_PlayerUI_PhaseBSuite_Step` | — | private |
| 1316 | `Debug_Run_PlayerUI_PhaseBSuite` | player_idx, kill_grant | public |
| 1345 | `Debug_PlayerUI_RegressionCheck` | player_idx | public |

### debug/cba_debug_inspectors.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 14 | `Debug_GetBuildingLimitState` | — | public |
| 57 | `Debug_GetSiegeLimitState` | — | public |
| 95 | `Debug_RamSiegeTowerLimitState` | — | public |
| 130 | `Debug_TeamBalanceCapState` | — | public |
| 165 | `Debug_GetKeepOwnershipMap` | — | public |
| 191 | `Debug_GetVillagerState` | — | public |
| 214 | `Debug_GetOptionParseResults` | — | public |
| 241 | `Debug_GetPostDefeatState` | — | public |
| 262 | `Debug_GetReligiousState` | — | public |
| 286 | `Debug_GetWonderState` | — | public |
| 308 | `Debug_GetAutoAgeState` | — | public |
| 326 | `Debug_CheckUpgradeBlueprint` | upgrade_name | public |
| 349 | `Debug_AutoAge_CheckSpecialUpgradeIds` | — | public |
| 381 | `Debug_KeepCap_CheckSpecialAgeAbilityResolution` | — | public |
| 488 | `Debug_GetStarterKeepState` | — | public |
| 564 | `Debug_SiegeLimitFullDump` | — | public |
| 767 | `Debug_RamLimitFullTrace` | — | public |
| 1093 | `Debug_SiegeLimitCrossValidation` | — | public |
| 1161 | `_SiegeAudit_CheckTag` | bp, tag, is_entity | local |
| 1172 | `_SiegeAudit_AddIssue` | issues, severity, kind, civ, key, detail | local |
| 1178 | `_SiegeAudit_CheckPaths` | civ, key, bp_name, bp, cls, is_entity, issues | local |
| 1179 | `chk` | tag | local |
| 1344 | `Debug_ValidateSiegeClassifications` | — | public |
| 1526 | `Debug_TeamBalancePerLimit` | — | public |
| 1575 | `Debug_LeaverSummary` | — | public |
| 1705 | `Debug_AutoPopHouseGuard` | — | public |

### debug/cba_debug_leaver.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 40 | `_LeaverDebug_FullFinalize` | — | private |
| 118 | `_LeaverMilTest_Finalize` | — | private |
| 210 | `_LeaverMilTest_GetActualRecipientIndex` | src_idx | private |
| 223 | `_LeaverMilTest_IsAlivePlayerIndex` | player_idx | private |
| 230 | `_LeaverMilTest_GetCivSuffix` | civ_name | private |
| 239 | `_LeaverMilTest_GetRoleSourceCandidates` | role_key, src_suffix | private |
| 257 | `_LeaverMilTest_FindReceiverClassCandidate` | role_key, src_civ, dst_civ | private |
| 277 | `_LeaverMilTest_SelectAutoPair` | — | private |
| 314 | `_LeaverMilTest_SelectFullValidationTarget` | excluded_idx | private |
| 331 | `_LeaverDebug_Stage1_Snapshot` | — | private |
| 410 | `_LeaverDebug_Stage2_ReverseMap` | — | private |
| 486 | `_LeaverDebug_Stage3_Disconnect` | player_idx | private |
| 526 | `_LeaverDebug_Stage4_Validate` | pre_snapshot, disconnected_idx | private |
| 627 | `_LeaverDebug_Stage5_BlueprintAudit` | — | private |
| 708 | `_LeaverDebug_Stage6_Summary` | stage_issues | private |
| 921 | `Debug_LeaverConversion_Full` | disconnect_player_idx, opt_mode | public |
| 985 | `Debug_LeaverMilTest` | src_idx, dst_idx, verbose | public |
| 1201 | `Debug_LeaverMilProof_OneShot` | verbose | public |
| 1263 | `Debug_LeaverConversion_Inspect` | — | public |
| 1348 | `Debug_LeaverConversion_Stress` | num_disconnects | public |
| 1484 | `_VisualTest_SafeWorldPos` | raw_x, raw_z | local |
| 1499 | `_VisualTest_SafeGridBase` | raw_x, raw_z, cols, spacing_x, total_slots, spacing_z | local |
| 1519 | `_VisualTest_BuildingGroup` | category_name, keys | private |
| 1567 | `_VisualTest_DeferredCleanup` | — | private |
| 1592 | `_VisualTest_DeferredCleanupStep` | — | private |
| 1645 | `_VisualTest_ProcessUnitBatch` | — | private |
| 1749 | `_VisualTest_NextPhase` | — | private |
| 1815 | `Debug_LeaverConversion_VisualByCiv` | src_civ, dst_civ, mode | public |
| 1929 | `Debug_LeaverConversion_Visual` | src_idx, dst_idx, mode | public |
| 1947 | `_ResolveVisualPlayerSelector` | selector, default_idx, role | local |
| 2051 | `Debug_LeaverConversion_VisualCleanup` | — | public |
| 2077 | `_LeaverDebug_SimulateGates` | bp_name, ags_key, player_id | private |
| 2126 | `Debug_LeaverConversion_MilResolve` | src_idx, dst_idx | public |
| 2270 | `Debug_LeaverCrossCivMatrix` | opt_mode | public |
| 2623 | `Debug_LeaverMilCoverage_Pair` | src_civ, rcv_civ | public |
| 2710 | `Debug_LeaverMilCoverage_AllPairs` | opt_mode | public |
| 2857 | `Debug_ForceDisconnect` | player_idx | public |
| 2865 | `Debug_LeaverValidation` | — | public |
| 2913 | `Debug_TransferValidation` | src_idx, dst_idx | public |
| 2941 | `Debug_ForceAnnihilation` | player_idx | public |
| 2965 | `Debug_GetLeaverBalanceState` | — | public |
| 2993 | `Debug_GetBestAllyInfo` | — | public |
| 3044 | `_LeaverDebug_FullSystemValidateLimitsUI` | — | private |
| 3110 | `_LeaverDebug_Stage4b_WallOwnershipAudit` | victim_id | private |
| 3173 | `_LeaverDebug_FullSystemFinalize` | — | private |
| 3389 | `Debug_FullSystemValidation` | player_idx | public |
| 3467 | `Debug_FullValidation_All` | player_idx, mode | public |
| 3486 | `Debug_LeaverPerformance` | — | public |
| 3529 | `_LeaverPerf_CascadeNext` | — | private |
| 3578 | `_LeaverPerf_CascadeSummary` | — | private |
| 3611 | `Debug_LeaverPerformance_6Player` | count | public |
| 3657 | `Debug_LeaverPipelineStatus` | — | public |
| 3692 | `Debug_LeaverCoverage_AllCivPairs` | opt_mode | public |
| 3827 | `Debug_LeaverCoverage_Civ` | src_civ_name | public |
| 3912 | `Debug_LeaverCoverage_Pair` | src_civ, rcv_civ | public |
| 4014 | `_LeaverCoverage_TryResolve` | civ_name, ags_key | private |
| 4030 | `Debug_LeaverResolve_ForcedBP` | — | public |
| 4179 | `_ClassifyWeaponPath` | weapon_bp_name | local |
| 4242 | `Debug_LeaverWeaponAudit` | — | public |
| 4436 | `Debug_LeaverTransferInspector` | rcv_civ, src_civ | public |
| 4550 | `Debug_LeaverWeaponAudit_ReceiverClass` | filter_civ | public |
| 4700 | `Debug_PrecacheManifest_ForcedCoverage` | — | public |
| 4807 | `Debug_LeaverTransferInspector_AllPairs` | src_civ | public |
| 4845 | `Debug_PrecacheManifest_Summary` | — | public |
| 4904 | `Debug_PrecacheManifest_Gaps` | — | public |
| 4940 | `Debug_PrecacheManifest_Confirmed` | — | public |
| 4964 | `Debug_PrecacheManifest_Report` | — | public |
| 5100 | `Debug_LeaverSpawnerExemptProof` | src_idx, dst_idx | public |
| 5327 | `leaver_matrix_all_pairs` | opt_mode | public |
| 5386 | `debug.players.full_validation_all` | idx, mode | public |
| 5391 | `debug.players.forceDisconnect` | idx | public |
| 5395 | `debug.players.forceAnnihilation` | idx | public |
| 5404 | `debug.players.run` | player_idx | public |

### debug/cba_debug_limits_ui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 21 | `Debug_GetLimitsUIState` | — | public |
| 53 | `Debug_ConstructionTrace` | player_idx | public |
| 116 | `Debug_LimitsUIStress` | — | public |
| 187 | `Debug_LimitsUI_TraceUpdateFlow` | enable | public |

### debug/cba_debug_playerui_anim.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 77 | `Debug_PlayerUI_Anim_FeatureStatus` | — | public |
| 94 | `Debug_PlayerUI_Anim_PresetSafe` | — | public |
| 100 | `Debug_PlayerUI_Anim_PresetAll` | — | public |
| 106 | `Debug_PlayerUI_Anim_TogglePresetHudOnly` | — | public |
| 112 | `Debug_PlayerUI_Anim_TogglePresetFull` | — | public |
| 118 | `Debug_PlayerUI_Anim_ApplyWhenVisible` | enabled | public |
| 125 | `Debug_PlayerUI_Anim_ToggleProbe` | path | public |
| 141 | `PlayerUI_Debug_FeatureStatus` | — | public |
| 145 | `PlayerUI_Debug_TogglePresetFull` | — | public |
| 149 | `Debug_PlayerUI_Anim_SetMinimalHud` | enabled | public |
| 157 | `Debug_PlayerUI_Anim_RestoreStage1` | — | public |
| 165 | `Debug_PlayerUI_Anim_RestoreStage2` | — | public |
| 171 | `Debug_PlayerUI_Anim_RestoreStage3` | — | public |
| 177 | `Debug_PlayerUI_Anim_RestoreStage4` | — | public |
| 183 | `Debug_PlayerUI_Anim_RestoreStage5` | — | public |
| 189 | `Debug_PlayerUI_Anim_RestoreStage6` | — | public |
| 225 | `_Debug_ElimValidate_Log` | message | local |
| 229 | `_Debug_ElimValidate_IsTrue` | value | local |
| 246 | `_Debug_ElimValidate_GetLocalPlayerIndex` | — | local |
| 258 | `_Debug_ElimValidate_IsSafeTarget` | player_idx, local_idx | local |
| 276 | `_Debug_ElimValidate_GetSafeCandidates` | local_idx | local |
| 289 | `_Debug_ElimValidate_GetNextCandidateCyclic` | candidates, local_idx, skip_idx | local |
| 302 | `_Debug_ElimValidate_SelectTargets` | candidates | local |
| 361 | `_Debug_ElimValidate_ReadDiagSnapshot` | — | local |
| 375 | `_Debug_ElimValidate_GetWorldPlayerId` | worldIndex | local |
| 386 | `_Debug_ElimValidate_ResolveUIIndexByPlayerId` | worldIndex | local |
| 403 | `_Debug_ElimValidate_ResolveObservationIndex` | worldIndex | local |
| 417 | `_Debug_ElimValidate_ReadPlayerData` | worldIndex | local |
| 428 | `_Debug_ElimValidate_ReadAnimationEntry` | worldIndex | local |
| 440 | `_Debug_ElimValidate_IsAnimActive` | worldIndex | local |
| 451 | `_Debug_ElimValidate_GetProgress` | worldIndex | local |
| 462 | `_Debug_ElimValidate_IsWorldPlayerEliminated` | worldIndex | local |
| 474 | `_Debug_ElimValidate_FormatFailures` | failures | local |
| 481 | `_Debug_ElimValidate_TriggerEliminate` | player_idx | local |
| 492 | `_Debug_ElimValidate_TriggerEliminateStrict` | player_idx | local |
| 510 | `_Debug_ElimValidate_TriggerSurrender` | player_idx | local |
| 521 | `_Debug_ElimValidate_TriggerDisconnect` | player_idx | local |
| 542 | `Debug_PlayerUI_Elim_ValidateFull` | verbose | public |
| 619 | `_Debug_ElimValidate_RunNextStage` | — | private |
| 708 | `_Debug_ElimValidate_PollStageEarly` | — | private |
| 754 | `_Debug_ElimValidate_PollStageMain` | — | private |
| 835 | `_Debug_ElimValidate_FinalizeStage` | — | private |
| 1025 | `_Debug_ElimValidate_FinalizeRun` | — | private |
| 1081 | `Debug_PlayerUI_Anim_RunStaged` | delay | public |
| 1104 | `_Debug_PlayerUI_Anim_RunStaged_Step` | — | private |
| 1166 | `_Debug_PlayerUI_Anim_RunStaged_Finalize` | — | private |
| 1174 | `Debug_PlayerUI_Anim_TogglePaths` | hud_enabled, scores_enabled, objectives_enabled | public |
| 1190 | `Debug_PlayerUI_Anim_Features` | move_enabled, scale_enabled, pulse_enabled, dim_enabled | public |
| 1252 | `_Debug_Anim_Phase0_Engine` | — | private |
| 1348 | `_Debug_Anim_Phase1_RankState` | — | private |
| 1469 | `_Debug_Anim_Phase2_BindingCoverage` | — | private |
| 1567 | `_Debug_Anim_Phase3_FlipStress` | — | private |
| 1684 | `_Debug_Anim_Phase4_ScorePulse` | — | private |
| 1782 | `_Debug_Anim_Phase5_CrashProbes` | — | private |
| 1901 | `_Debug_Anim_Phase6_MonitorDryRun` | — | private |
| 1920 | `Debug_PlayerUI_Anim` | — | public |
| 1941 | `_Debug_Anim_Chain1` | — | private |
| 1946 | `_Debug_Anim_Chain2` | — | private |
| 1951 | `_Debug_Anim_Chain3` | — | private |
| 1956 | `_Debug_Anim_Chain4` | — | private |
| 1961 | `_Debug_Anim_Chain5` | — | private |
| 1966 | `_Debug_Anim_Chain6` | — | private |
| 1971 | `_Debug_Anim_Finish` | — | private |
| 1996 | `Debug_PlayerUI_Anim_Monitor` | — | public |
| 2015 | `Debug_PlayerUI_Anim_MonitorStop` | — | public |
| 2047 | `_Debug_Anim_MonitorTick` | — | private |
| 2056 | `_Debug_Anim_MonitorCheck` | — | private |
| 2149 | `Debug_PlayerUI_Anim_Stress` | rounds | public |
| 2230 | `Debug_PlayerUI_Anim_Pulse` | player_idx | public |
| 2260 | `Debug_PlayerUI_Anim_ValidateDataContext` | — | public |
| 2269 | `Debug_PlayerUI_Anim_Snapshot` | — | public |
| 2365 | `Debug_PlayerUI_RewardPlayback_Snapshot` | — | public |
| 2452 | `_Debug_RewardCapture_GuardSnapshot` | — | local |
| 2463 | `_Debug_RewardCapture_Stop` | status | local |
| 2506 | `_Debug_RewardValidate_QueuedInvariants` | phase | local |
| 2540 | `_Debug_RewardCapture_Tick` | — | private |
| 2722 | `Debug_PlayerUI_RewardPlayback_CaptureFull` | threshold, count, timeout | public |
| 2766 | `Debug_PlayerUI_RewardPlayback_Inject` | threshold, count | public |
| 2812 | `Debug_PlayerUI_RewardPlayback_InjectReal` | score_delta | public |
| 2912 | `Debug_PlayerUI_RewardPlayback_SkipPhase` | — | public |
| 2925 | `Debug_PlayerUI_RewardPlayback_Reset` | — | public |
| 2959 | `Debug_PlayerUI_RewardPlayback_ValidateCycle` | threshold, count, timeout | public |

### debug/cba_debug_playerui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 20 | `_Debug_PlayerUI_Phase0_Init` | — | private |
| 185 | `_Debug_PlayerUI_Phase1_Data` | — | private |
| 330 | `_Debug_PlayerUI_Phase2_UI` | — | private |
| 417 | `_Debug_PlayerUI_Finish` | — | private |
| 442 | `Debug_PlayerUI` | — | public |
| 458 | `_Debug_PlayerUI_Chain1` | — | private |
| 463 | `_Debug_PlayerUI_Chain2` | — | private |
| 468 | `_Debug_PlayerUI_Chain3` | — | private |
| 477 | `Debug_PlayerUI_Data` | — | public |
| 506 | `Debug_PlayerUI_UI` | — | public |
| 535 | `_Debug_PlayerUI_Phase3_Ranking` | — | private |
| 657 | `Debug_PlayerUI_Ranking` | — | public |
| 693 | `debug.playerUI.run` | — | public |

### debug/cba_debug_qa_runner.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 52 | `_QA_Topic1_ResourceDelivery` | — | private |
| 69 | `_QA_T1_Ask` | — | private |
| 76 | `_QA_T1_OnAnswer` | choice | private |
| 91 | `_QA_Topic2_PopulationGrowth` | — | private |
| 123 | `_QA_T2_Ask` | — | private |
| 130 | `_QA_T2_OnAnswer` | choice | private |
| 146 | `_QA_Topic3_RewardSpawn` | — | private |
| 169 | `_QA_T3_Ask` | — | private |
| 176 | `_QA_T3_OnAnswer` | choice | private |
| 192 | `_QA_Topic4_BuildingLimitLock` | — | private |
| 215 | `_QA_T4_Ask` | — | private |
| 222 | `_QA_T4_OnAnswer` | choice | private |
| 237 | `_QA_Topic5_SiegeLimitEnforcement` | — | private |
| 270 | `_QA_T5_Ask` | — | private |
| 277 | `_QA_T5_OnAnswer` | choice | private |
| 293 | `_QA_Topic6_LeaverTransfer` | — | private |
| 328 | `_QA_T6_AskQ1` | — | private |
| 335 | `_QA_T6_OnQ1` | choice | private |
| 345 | `_QA_T6_AskQ2` | — | private |
| 352 | `_QA_T6_OnQ2` | choice | private |
| 367 | `_QA_Topic7_PlayerStatusHUD` | — | private |
| 387 | `_QA_T7_OnAnswer` | choice | private |
| 402 | `_QA_Topic8_OverallScreenCheck` | — | private |
| 424 | `_QA_T8_OnAnswer` | choice | private |
| 453 | `Debug_QADiagnostic_Topic` | n | public |
| 475 | `Debug_QADiagnostic` | — | public |
| 495 | `_QA_RunNextTopic` | — | private |
| 519 | `_QA_OnTopicComplete` | — | private |
| 530 | `_QA_WaitForPrompt` | — | private |
| 543 | `_QA_FinalReport` | — | private |
| 582 | `Debug_QADiagnosticStatus` | — | public |
| 620 | `_QA_Transfer_Record` | name, pass, detail | private |
| 630 | `_QA_Transfer_ComputePrecache` | — | private |
| 659 | `_QA_Transfer_FindAliveCandidate` | excluded | private |
| 675 | `_QA_Transfer_AutoAgeAllPlayers` | — | private |
| 686 | `_QA_Transfer_SpawnRelevantForPlayer` | player_idx | private |
| 748 | `_QA_Transfer_PrepareSetup` | — | private |
| 758 | `_QA_Transfer_AskPrecacheYesNo` | player_idx, scenario_label, next_fn_name | private |
| 775 | `_QA_Transfer_OnPrecacheAnswer` | choice | private |
| 789 | `Debug_QADiagnostic_TransferScenarios` | surrender_idx, elimination_idx, disconnect_idx | public |
| 826 | `_QA_Transfer_RunSurrenderPrecheck` | — | private |
| 831 | `_QA_Transfer_DoSurrender` | — | private |
| 844 | `_QA_Transfer_PromptSurrenderOutcome` | — | private |
| 857 | `_QA_Transfer_OnSurrenderOutcome` | choice | private |
| 862 | `_QA_Transfer_RunEliminationPrecheck` | — | private |
| 867 | `_QA_Transfer_DoElimination` | — | private |
| 880 | `_QA_Transfer_PromptEliminationOutcome` | — | private |
| 893 | `_QA_Transfer_OnEliminationOutcome` | choice | private |
| 898 | `_QA_Transfer_RunDisconnectPrecheck` | — | private |
| 903 | `_QA_Transfer_DoDisconnect` | — | private |
| 914 | `_QA_Transfer_PromptDisconnectOutcome` | — | private |
| 927 | `_QA_Transfer_OnDisconnectOutcome` | choice | private |
| 932 | `_QA_Transfer_Finalize` | — | private |

### debug/cba_debug_registry.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 61 | `Debug_RegisterModule` | meta, handlers | public |
| 128 | `Debug_ListModules` | filter | public |
| 158 | `Debug_ModuleInfo` | name | public |
| 177 | `Debug_DependencyGraph` | — | public |
| 206 | `Debug_ValidateModules` | — | public |
| 259 | `Debug_SealModuleRegistry` | — | public |
| 272 | `Debug_IsRegistrySealed` | — | public |
| 282 | `Debug_GetAllModuleManifests` | — | public |
| 288 | `Debug_GetTagModuleMap` | — | public |
| 294 | `Debug_GetModuleCount` | — | public |

### debug/cba_debug_rules.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 59 | `Debug_RegisterRule` | rule | public |
| 102 | `Debug_CheckRules` | domain_filter, ctx | public |
| 204 | `Debug_ListRules` | domain_filter | public |
| 231 | `Debug_RuleInfo` | name | public |
| 255 | `Debug_RuleReport` | — | public |
| 289 | `Debug_GetAllRules` | — | public |
| 295 | `Debug_GetRuleCount` | — | public |
| 311 | `check` | ctx | public |
| 331 | `check` | ctx | public |
| 349 | `check` | ctx | public |
| 374 | `check` | ctx | public |
| 403 | `check` | ctx | public |

### debug/cba_debug_scenario.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 36 | `_Scenario_Stage1` | — | private |
| 51 | `_Scenario_Stage2` | — | private |
| 66 | `_Scenario_Stage3` | — | private |
| 81 | `_Scenario_Stage4` | — | private |
| 97 | `_Scenario_Stage5` | — | private |
| 140 | `_Scenario_Stage6` | — | private |
| 206 | `_Scenario_Stage7` | — | private |
| 248 | `_Scenario_RunNextStage` | — | private |
| 271 | `Debug_Scenario` | — | public |
| 294 | `Debug_ScenarioStatus` | — | public |
| 311 | `Debug_ScenarioStop` | — | public |

### debug/cba_debug_settings.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 116 | `Debug_GetSetting` | key | public |
| 128 | `Debug_SetSetting` | key, value | public |
| 146 | `Debug_ListSettings` | domain_filter | public |
| 179 | `Debug_ResetSettings` | — | public |
| 195 | `Debug_GetSettingSchema` | key | public |
| 201 | `Debug_GetAllSettingSchemas` | — | public |

### debug/cba_debug_siege_test.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 51 | `_ST_Assert` | test_name, condition, detail | local |
| 61 | `_ST_ResolvePlayer` | — | local |
| 71 | `_ST_GrantResources` | player | local |
| 78 | `_ST_KillAllSiege` | player | local |
| 99 | `_ST_ResetCounters` | player | local |
| 116 | `_ST_FullRecount` | player | local |
| 126 | `_ST_SpawnSquad` | player, sbp_name, pos | local |
| 136 | `_ST_ResolveBlueprint` | bp_name, prefer_entity | local |
| 151 | `_ST_LogCounters` | player, label | local |
| 162 | `_ST_CreateScaffold` | player, ebp, pos, label | local |
| 189 | `_ST_FindWorkshop` | player | local |
| 203 | `_ST_DestroyAllWorkshops` | player | local |
| 218 | `_ST_KillNRams` | player, n | local |
| 235 | `_ST_LogEnforcement` | player, label, transient | local |
| 262 | `_ST_Interceptor_ConstructionStart` | context | private |
| 282 | `_ST_Interceptor_ConstructionComplete` | context | private |
| 302 | `_ST_Interceptor_ConstructionCancelled` | context | private |
| 336 | `Debug_SiegeTest` | — | public |
| 506 | `_ST_Phase1_RamLimits` | — | private |
| 576 | `_ST_Phase1b_RamRecheck` | — | private |
| 593 | `_ST_Phase2_STLifecycle` | — | private |
| 626 | `_ST_Phase2b_STVerify` | — | private |
| 654 | `_ST_Phase2c_CancelVerify` | — | private |
| 691 | `_ST_Phase3_GenericSiege` | — | private |
| 800 | `_ST_Phase4_SEGate` | — | private |
| 847 | `_ST_Phase5_FieldEdgeCases` | — | private |
| 947 | `_ST_Phase5b_CapHotfixVerify` | — | private |
| 976 | `_ST_Phase5c_BuildableSiege` | — | private |
| 1035 | `_ST_Phase5d_BuildableVerify` | — | private |
| 1060 | `_ST_Phase6_Workshop` | — | private |
| 1109 | `_ST_Phase6b_Baseline` | — | private |
| 1136 | `_ST_Phase6c_OverQueue` | — | private |
| 1173 | `_ST_Phase6d_VerifyProduction` | — | private |
| 1200 | `_ST_Phase6e_VerifyKill` | — | private |
| 1239 | `_ST_Phase6f_VerifyResume` | — | private |
| 1267 | `_ST_Phase7_EventHandlers` | — | private |
| 1298 | `_ST_Phase7b_VerifyKill` | — | private |
| 1323 | `_ST_Phase7c_TypeTags` | — | private |
| 1351 | `_ST_Phase8_Summary` | — | private |
| 1437 | `debug.siege.run` | — | public |

### debug/cba_debug_spawn_sequences.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 17 | `Debug_RunSpawnPlan` | plan | public |
| 41 | `_SpawnPlan_RunNextStep` | — | private |
| 113 | `_SpawnPlan_AdvanceOrPause` | step | private |
| 120 | `_SpawnPlan_FinalReport` | — | private |
| 152 | `Debug_SpawnAndValidate` | bp_name, player_idx, count, validate_fn | public |
| 164 | `Debug_SpawnPlan_SiegeStress` | — | public |
| 171 | `validate_fn` | p, c, bp | public |
| 173 | `validate_fn` | p, c, bp | public |
| 175 | `validate_fn` | p, c, bp | public |
| 177 | `validate_fn` | p, c, bp | public |
| 179 | `validate_fn` | p, c, bp | public |
| 185 | `Debug_SpawnPlan_MixedArmy` | player_idx | public |

### debug/cba_debug_stress.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 27 | `_Stress_RunTest` | name, test_fn | private |
| 42 | `_Stress_StageHeader` | num, name | private |
| 51 | `_Stress_Stage1_CoreSystem` | — | private |
| 79 | `_Stress_Stage2_Blueprints` | — | private |
| 156 | `_Stress_Stage3_Rewards` | — | private |
| 185 | `_Stress_Stage4_Economy` | — | private |
| 226 | `_Stress_Stage5_PopAge` | — | private |
| 258 | `_Stress_Stage6_WinConditions` | — | private |
| 283 | `_Stress_Stage7_Restrictions` | — | private |
| 458 | `_Stress_Stage8_PlayerState` | — | private |
| 509 | `_Stress_FinalReport` | — | private |
| 535 | `Debug_StressTest` | — | public |
| 553 | `_Stress_Run2` | — | private |
| 557 | `_Stress_Run3` | — | private |
| 561 | `_Stress_Run4` | — | private |
| 565 | `_Stress_Run5` | — | private |
| 569 | `_Stress_Run6` | — | private |
| 573 | `_Stress_Run7` | — | private |
| 577 | `_Stress_Run8` | — | private |
| 582 | `Debug_StressStage` | n | public |
| 608 | `Debug_SiegeLimitStressTest` | — | public |

### debug/cba_debug_ui_prompts.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 36 | `_DebugPrompt_BuildXaml` | — | local |
| 122 | `_DebugPrompt_EnsurePanel` | — | local |
| 153 | `_DebugPrompt_UpdateDC` | — | local |
| 159 | `_DebugPrompt_Show` | — | local |
| 166 | `_DebugPrompt_Hide` | — | local |
| 177 | `_DebugPrompt_ClickA` | — | private |
| 181 | `_DebugPrompt_ClickB` | — | private |
| 185 | `_DebugPrompt_ClickC` | — | private |
| 189 | `_DebugPrompt_ClickD` | — | private |
| 197 | `_DebugPrompt_Resolve` | choice_index | private |
| 242 | `_DebugPrompt_PollTimeout` | — | private |
| 275 | `Debug_AskYesNo` | question, on_answer, timeout, default_answer, detail | public |
| 350 | `Debug_AskChoice` | question, choices, on_answer, timeout, default_choice, detail | public |
| 429 | `Debug_Answer` | value | public |
| 466 | `Debug_DismissPrompt` | — | public |
| 484 | `_DebugPrompt_Cleanup` | — | private |
| 511 | `Debug_InteractiveCheck_Precache` | — | public |
| 588 | `_DebugPC_OnConfirm` | choice | private |
| 600 | `_DebugPC_OnChoice` | choice | private |
| 626 | `Debug_InteractiveCheck_KeepState` | — | public |
| 643 | `_DebugKS_NextPlayer` | — | private |
| 701 | `_DebugKS_OnAnswer` | choice | private |
| 714 | `_DebugKS_NextPlayer_Scheduled` | — | private |
| 724 | `Debug_InteractiveCheck_SiegeLimitUI` | — | public |
| 768 | `_DebugSLUI_AskConfirm` | — | private |
| 778 | `_DebugSLUI_OnAnswer` | choice | private |
| 796 | `Debug_InteractiveChecks` | — | public |
| 813 | `_DebugIC_RunPrecache` | — | private |
| 828 | `_DebugIC_WaitForIdle` | — | private |
| 846 | `_DebugIC_RunKeepState` | — | private |
| 851 | `_DebugIC_RunSiegeUI` | — | private |
| 856 | `_DebugIC_Finish` | — | private |

### debug/cba_debug_validation.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 16 | `_Debug_Phase0_Boot` | — | private |
| 65 | `_Debug_Phase1_Config` | — | private |
| 129 | `_Debug_Phase2_Runtime` | — | private |
| 265 | `_Debug_Phase3_Data` | — | private |
| 667 | `_Debug_Phase4_Endstate` | — | private |
| 716 | `_Debug_Phase5_Limits` | — | private |
| 761 | `_Debug_FinalReport` | — | private |
| 806 | `Debug_FullValidation` | — | public |
| 822 | `_Debug_FullValidation_Phase1` | — | private |
| 826 | `_Debug_FullValidation_Phase2` | — | private |
| 830 | `_Debug_FullValidation_Phase3` | — | private |
| 834 | `_Debug_FullValidation_Phase4` | — | private |
| 838 | `_Debug_FullValidation_Phase5` | — | private |
| 847 | `Debug_LimitEnforcementValidator` | — | public |
| 865 | `Debug_LimitEnforcementValidator` | — | public |
| 892 | `Debug_FactionMapDiagnostic` | — | public |
| 903 | `_fmd_test` | name, pass, detail | local |
| 1073 | `_fmd_try_resolve` | civ, key | local |
| 1266 | `Debug_VerifyDynastiesData` | — | public |
| 1277 | `_test` | name, pass, detail | local |
| 1414 | `_reward_has_thresholds` | civ, third_threshold | local |

### debug/cba_verify_military_pipeline.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 37 | `LeaverVerify_HeroBehavior` | — | public |
| 90 | `LeaverVerify_ElephantMapping` | — | public |
| 146 | `LeaverVerify_MilitaryRoutes` | — | public |
| 187 | `LeaverVerify_StatsConsistency` | — | public |
| 261 | `LeaverVerify_NoHiddenTransfers` | — | public |
| 299 | `LeaverVerify_AutoRunAll` | — | public |

## gameplay

### gameplay/ags_auto_population.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 38 | `AGS_PopulationAutomatic_UpdateModuleSettings` | — | public |
| 46 | `AGS_PopulationAutomatic_EarlyInitializations` | — | public |
| 52 | `AGS_PopulationAutomatic_PresetFinalize` | — | public |
| 65 | `AGS_PopulationAutomatic_CompensateInnate` | — | public |
| 82 | `AGS_PopulationAutomatic_NormalizeStartCap` | player | public |
| 96 | `AGS_PopulationAutomatic_ApplyStartCaps` | — | public |
| 104 | `AGS_IncreasePopulation` | — | public |
| 129 | `AGS_AutoPopulationStart` | — | public |
| 171 | `AGS_PopulationAutomatic_ReconcileCapDrift` | — | public |
| 215 | `AGS_AutoPop_BuildForbiddenBPSet` | — | public |
| 234 | `AGS_AutoPop_ScheduleDeferredReconcile` | reason | public |
| 242 | `AGS_AutoPop_RunDeferredReconcile` | — | public |
| 250 | `AGS_AutoPop_OnConstructionComplete` | context | public |
| 265 | `AGS_AutoPop_OnEntityKilled` | context | public |

### gameplay/ags_auto_resources.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 18 | `AGS_AutoResources_UpdateModuleSettings` | — | public |
| 24 | `AGS_AutoResources_PresetFinalize` | — | public |
| 35 | `AGS_AutoResources` | — | public |
| 75 | `AGS_Toggle_EconBuildings` | — | public |

### gameplay/ags_game_rates.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 20 | `AGS_GameRates_UpdateModuleSettings` | — | public |
| 27 | `AGS_GameRates_PresetFinalize` | — | public |
| 38 | `AGS_GameRates_ApplyBonus` | bps | public |
| 51 | `AGS_GameRates_ApplyModifier` | player_id, modifier_ebp, modifier_type, modifier_value | public |

### gameplay/ags_gather_rates.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 19 | `AGS_GatherRates_UpdateModuleSettings` | — | public |
| 26 | `AGS_GatherRates_PresetFinalize` | — | public |
| 36 | `AGS_GatherRates_ApplyBonus` | bps | public |
| 51 | `AGS_GatherRates_ApplyModifier` | player_id, modifier_ebp, modifier_type, modifier_value | public |

### gameplay/ags_handicaps.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 30 | `AGS_Handicaps_UpdateModuleSettings` | — | public |
| 37 | `AGS_Handicaps_PresetFinalize` | — | public |
| 46 | `AGS_Handicaps_ApplyPerPlayer` | — | public |
| 62 | `AGS_Handicaps_ApplyWorkerBonus` | bps | public |
| 85 | `AGS_Handicaps_ApplyMilitaryBonus` | bps | public |
| 105 | `AGS_Handicaps_ApplyModifier` | player_id, modifier_ebp, modifier_type, modifier_value | public |
| 108 | `AGS_Handicaps_AddModifier` | player_id, modifier_ebp, modifier_type, modifier_value | public |
| 113 | `AGS_Handicaps_CreateListFrom` | slots | public |
| 126 | `AGS_Handicaps_ToRaw` | perc_value | public |

### gameplay/ags_limits_ui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 53 | `AGS_LimitsUI_ShouldTraceUpdateFlow` | — | local |
| 147 | `get_current` | p | public |
| 148 | `get_max` | p | public |
| 149 | `is_active` | — | public |
| 160 | `get_current` | p | public |
| 161 | `get_max` | p | public |
| 162 | `is_active` | — | public |
| 173 | `get_current` | p | public |
| 174 | `get_max` | p | public |
| 175 | `is_active` | — | public |
| 187 | `get_current` | p | public |
| 188 | `get_max` | p | public |
| 189 | `is_active` | — | public |
| 202 | `AGS_LimitsUI_UpdateModuleSettings` | — | public |
| 215 | `AGS_LimitsUI_EarlyInitializations` | — | public |
| 219 | `AGS_LimitsUI_OnPlay` | — | public |
| 243 | `AGS_LimitsUI_OnGameRestore` | — | public |
| 249 | `AGS_LimitsUI_OnGameOver` | — | public |
| 262 | `AGS_LimitsUI_OnPlayerDefeated` | player, reason | public |
| 274 | `AGS_LimitsUI_DeferUpdate` | reason | public |
| 290 | `AGS_LimitsUI_OnConstructionComplete` | context | public |
| 294 | `AGS_LimitsUI_OnBuildItemComplete` | context | public |
| 298 | `AGS_LimitsUI_OnEntityKilled` | context | public |
| 302 | `AGS_LimitsUI_OnSquadKilled` | context | public |
| 312 | `AGS_LimitsUI_GetColors` | current, max | public |
| 331 | `AGS_LimitsUI_HexToByte` | two | local |
| 335 | `AGS_LimitsUI_ClampByte` | v | local |
| 341 | `AGS_LimitsUI_Lerp` | a, b, t | local |
| 345 | `AGS_LimitsUI_Clamp01` | v | local |
| 351 | `AGS_LimitsUI_AnimProgress` | left, total, min_start | local |
| 373 | `AGS_LimitsUI_BlendRGB` | base_rgb, target_rgb, t | public |
| 389 | `AGS_LimitsUI_BlendARGB` | base_argb, target_argb, t | public |
| 408 | `AGS_LimitsUI_BuildSnapshot` | dc | local |
| 420 | `AGS_LimitsUI_LogRecreate` | reason, detail | local |
| 441 | `AGS_LimitsUI_Update` | — | public |
| 574 | `AGS_LimitsUI_AnimTick` | — | public |
| 654 | `AGS_LimitsUI_BoostRGB` | base_rgb, factor | public |
| 673 | `AGS_LimitsUI_BoostARGB` | base_argb, factor | public |
| 692 | `AGS_LimitsUI_ApplyMargin` | — | public |
| 712 | `AGS_LimitsUI_Show` | show_ui | public |
| 727 | `AGS_LimitsUI_RecreateUI` | reason, detail | public |
| 740 | `AGS_LimitsUI_CreateAndUpdateUI` | — | public |
| 748 | `AGS_LimitsUI_CreateUI` | reason | public |

### gameplay/ags_no_dock.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 26 | `AGS_NoDock_UpdateModuleSettings` | — | public |
| 33 | `AGS_NoDock_PresetFinalize` | — | public |
| 41 | `AGS_NoWall_UpdateModuleSettings` | — | public |
| 48 | `AGS_NoWall_PresetFinalize` | — | public |
| 56 | `AGS_NoSiege_UpdateModuleSettings` | — | public |
| 63 | `AGS_NoSiege_PresetFinalize` | — | public |
| 70 | `AGS_NoArsenal_UpdateModuleSettings` | — | public |
| 77 | `AGS_NoArsenal_PresetFinalize` | — | public |
| 86 | `AGS_NoDock_Lock` | — | public |
| 93 | `AGS_NoWall_Lock` | — | public |
| 106 | `AGS_NoSiege_Lock` | — | public |
| 160 | `AGS_NoArsenal_Lock` | — | public |

### gameplay/ags_population_capacity.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 21 | `AGS_PopulationCapacity_UpdateModuleSettings` | — | public |
| 28 | `AGS_PopulationCapacity_AdjustSettings` | — | public |
| 35 | `AGS_PopulationCapacity_PresetFinalize` | — | public |
| 43 | `AGS_MedicPopulationCapacity_UpdateModuleSettings` | — | public |
| 50 | `AGS_MedicPopulationCapacity_PresetFinalize` | — | public |
| 60 | `AGS_PopulationCapacity_Change` | — | public |
| 67 | `AGS_PopulationCapacity_SetMinPopulation` | player, pop_size | public |
| 80 | `AGS_PopulationCapacity_ApplyMinPopulation` | player, pop_size | public |
| 84 | `AGS_PopulationCapacity_ApplyMaxCapPopulation` | player, pop_size | public |
| 90 | `AGS_MedicPopulationCapacity_Change` | — | public |
| 97 | `AGS_MedicPopulationCapacity_SetMinMedicPopulation` | player, pop_size | public |
| 103 | `AGS_MedicPopulationCapacity_ApplyMinMedicPopulation` | player, pop_size | public |
| 107 | `AGS_MedicPopulationCapacity_ApplyMaxCapMedicPopulation` | player, pop_size | public |

### gameplay/ags_reveal_fow_on_elimination.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 18 | `AGS_RevealFowOnElimination_UpdateModuleSettings` | — | public |
| 25 | `AGS_RevealFowOnElimination_OnPlayerDefeated` | player, reason | public |
| 34 | `AGS_RevealFowOnElimination_Reveal` | player | public |

### gameplay/ags_siege_house.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 16 | `AGS_DockHouse_UpdateModuleSettings` | — | public |
| 23 | `AGS_DockHouse_OnPlay` | — | public |
| 29 | `AGS_DockHouse_GameOver` | — | public |
| 38 | `AGS_DockHouse_IsDock` | entity_id | public |
| 42 | `AGS_DockHouse_OnConstructionComplete` | context | public |
| 62 | `AGS_DockHouse_OnEntityKilled` | context | public |
| 88 | `AGS_DockHouse_AddMaxCapPopulation` | player, value | public |
| 91 | `AGS_DockHouse_AddMinPopulation` | player, value | public |
| 95 | `AGS_DockHouse_RemoveMaxCapPopulation` | player, value | public |
| 98 | `AGS_DockHouse_RemoveMinPopulation` | player, value | public |

### gameplay/ags_special_population_ui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 34 | `AGS_SpecialPopulationUI_UpdateModuleSettings` | — | public |
| 41 | `AGS_SpecialPopulationUI_EarlyInitializations` | — | public |
| 46 | `AGS_SpecialPopulationUI_OnPlay` | — | public |
| 56 | `AGS_SpecialPopulationUI_OnGameRestore` | — | public |
| 62 | `AGS_SpecialPopulationUI_OnGameOver` | — | public |
| 71 | `AGS_SpecialPopulationUI_OnPlayerDefeated` | player, reason | public |
| 82 | `AGS_SpecialPopulationUI_OnConstructionComplete` | context | public |
| 85 | `AGS_SpecialPopulationUI_OnBuildItemComplete` | context | public |
| 88 | `AGS_SpecialPopulationUI_OnEntityKilled` | context | public |
| 91 | `AGS_SpecialPopulationUI_OnSquadKilled` | context | public |
| 99 | `AGS_SpecialPopulationUI_CreateDataContext` | — | public |
| 108 | `AGS_SpecialPopulationUI_Update` | — | public |
| 129 | `AGS_SpecialPopulationUI_MarginError` | — | public |
| 144 | `AGS_SpecialPopulationUI_Show` | show_ui | public |
| 151 | `AGS_SpecialPopulationUI_CreateAndUpdateUI` | — | public |
| 156 | `AGS_SpecialPopulationUI_CreateUI` | — | public |

### gameplay/ags_starting_age.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 18 | `AGS_StartingAge_UpdateModuleSettings` | — | public |
| 25 | `AGS_StartingAge_LateInitializations` | — | public |
| 34 | `AGS_StartingAge_UpgradeAllPlayers` | — | public |
| 40 | `AGS_StartingAge_UpgradePlayer` | player_id | public |

### gameplay/ags_team_balance.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 16 | `_CeilTo5` | n | private |
| 25 | `AGS_TeamBalance_UpdateModuleSettings` | — | public |
| 32 | `AGS_TeamBalance_OnPlayerDefeated` | player, reason | public |
| 41 | `AGS_TeamBalance_UpdateTeam` | player | public |
| 99 | `AGS_TeamBalance_UpdateTeamPopulation` | player, allies, allies_count | public |
| 125 | `AGS_TeamBalance_UpdateTeamMedicPopulation` | player, allies, allies_count | public |
| 147 | `AGS_TeamBalance_UpdateTeamResources` | player, allies, allies_count | public |
| 165 | `AGS_TeamBalance_UpdateAllLimits` | player, allies, allies_count | public |
| 191 | `AGS_TeamBalance_UpdateAutoRates` | current_alive_count | public |
| 213 | `AGS_TeamBalance_IncreaseCapPopulation` | player, pop_size | public |
| 217 | `AGS_TeamBalance_IncreaseMaxCapPopulation` | player, pop_size | public |

### gameplay/ags_tree_bombardment.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 37 | `AGS_TreeBombardment_UpdateModuleSettings` | — | public |
| 44 | `AGS_TreeBombardment_PrepareStart` | — | public |
| 50 | `AGS_TreeBombardment_OnGameOver` | — | public |
| 60 | `AGS_TreeBombardment_OnProjectileFired` | projectile | public |
| 72 | `AGS_TreeBombardment_OnProjectileLanded` | projectile | public |
| 88 | `AGS_TreeBombardment_OnExpectedLanding` | context, data | public |
| 103 | `AGS_TreeBombardment_DestroyTreeGroup` | projectile_target | public |
| 111 | `_AGS_DestroyAnyTree` | gid, idx, eid | local |

### gameplay/ags_unit_rates.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 19 | `AGS_UnitRates_UpdateModuleSettings` | — | public |
| 26 | `AGS_UnitRates_PresetFinalize` | — | public |
| 36 | `AGS_UnitRates_ApplyBonus` | bps | public |
| 47 | `AGS_UnitRates_ApplyModifier` | player_id, modifier_ebp, modifier_type, modifier_value | public |

### gameplay/cba_auto_age.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 59 | `CBA_AutoAge_UpdateModuleSettings` | — | public |
| 66 | `CBA_AutoAge_PresetFinalize` | — | public |
| 80 | `CBA_AutoAge_PlayerHasAnyUpgrade` | player_id, upgrades | public |
| 93 | `CBA_AutoAge_SetUpgradeAvailabilitySafe` | player_id, upg_name, lock_type, context | public |
| 111 | `CBA_AutoAge_SyncSpecialUpgradeAvailability` | player | public |
| 142 | `CBA_AutoAge_SetBuildCount` | player, new_count | public |
| 163 | `CBA_AutoAge_ReconcileSpecialProgress` | player | public |
| 183 | `CBA_AutoAge_UpgradeComplete` | context | public |
| 198 | `CBA_AutoAge_SetupObjective` | — | public |
| 261 | `CBA_AutoAge_UpdateTimer` | — | public |
| 279 | `CBA_AutoAge_ConstructionComplete` | context | public |
| 356 | `CBA_AutoAge_SetMaxAge` | — | public |
| 393 | `CBA_Auto_Age` | — | public |
| 404 | `CBA_Auto_Age_1` | — | public |
| 445 | `CBA_Auto_Age_2` | — | public |
| 482 | `CBA_Auto_Age_3` | — | public |

### gameplay/cba_economy.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 31 | `CBA_Economy_ParseOptions` | — | public |
| 71 | `CBA_Economy_SetStartingResources` | mode_key | public |
| 90 | `CBA_Economy_RemoveGaia` | — | public |
| 102 | `CBA_Economy_SetFOW` | — | public |

### gameplay/cba_hre_balance.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 20 | `CBA_HREBalance_UpdateModuleSettings` | — | public |
| 28 | `CBA_HREBalance_PresetFinalize` | — | public |
| 44 | `CBA_HREBalance_ApplyPenalty` | squad_blueprints | public |
| 67 | `CBA_HREBalance_ApplyModifier` | player_id, squad_bp, modifier_value | public |

### gameplay/cba_options.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 15 | `DebugLog` | area, msg, opt_data | public |
| 20 | `CBA_Options_ShouldLogSiegeStandard` | — | public |
| 24 | `CBA_Options_ShouldLogSiegeVerbose` | — | public |
| 34 | `CBA_Options_ShouldLogSiegeStateChange` | player, key, state | public |
| 45 | `CBA_Options_UpdateModuleSettings` | — | public |
| 53 | `CBA_Options_PresetFinalize` | — | public |
| 136 | `_BuildBlueprintReverseMap` | — | private |
| 165 | `CBA_Options_GetPlayerProdLimit` | player | public |
| 170 | `CBA_Options_GetWorkshopLimit` | — | public |
| 177 | `CBA_Options_GetPlayerWorkshopLimit` | player | public |
| 182 | `CBA_Options_GetPlayerSiegeLimit` | player | public |
| 187 | `CBA_Options_GetPlayerRamLimit` | player | public |
| 192 | `CBA_Options_GetPlayerSiegeTowerLimit` | player | public |
| 197 | `CBA_Options_GetPlayerOutpostLimit` | player | public |
| 203 | `CBA_Options_WorkshopLimit_ApplyThreshold` | player | public |
| 237 | `CBA_Options_BuildingLimit_SetupObjective` | — | public |
| 338 | `CBA_Options_BuildingLimit_ConstructionStart` | context | public |
| 460 | `CBA_Options_BuildingLimit_ConstructionCancelled` | context | public |
| 573 | `CBA_Options_BuildingLimit_OnEntityKilled` | context | public |
| 736 | `CBA_Options_SiegeLimit_Cancel_1` | gid, index, iid | public |
| 756 | `CBA_Options_SiegeLimit_Cancel_2` | gid, index, iid | public |
| 776 | `CBA_Options_SiegeLimit_Cancel_3` | gid, index, iid | public |
| 797 | `CBA_Options_AddScuttle_ConstructionComplete` | context | public |
| 816 | `CBA_Options_DarkAge_Unlocks` | — | public |
| 831 | `CBA_Options_VillagerSpawner` | — | public |
| 861 | `CBA_Option_KeepModifier` | — | public |
| 894 | `CBA_Options_OutpostRestrictions` | — | public |
| 912 | `CBA_Options_SiegeLimit_ApplyAllThresholds` | player | public |
| 931 | `CBA_Options_SiegeLimit_ConstructionStart` | context | public |
| 1055 | `CBA_Options_SiegeLimit_ScheduleDeferredRecheck` | player, reason | public |
| 1068 | `CBA_Options_SiegeLimit_RunDeferredRecheck` | — | public |
| 1140 | `CBA_Options_SiegeLimit_ConstructionCancelled` | context | public |
| 1200 | `CBA_Options_SiegeLimit_ConstructionComplete` | context | public |
| 1260 | `CBA_Options_SiegeLimit_EntityKilled` | context | public |
| 1349 | `CBA_Options_SiegeLimit_RecountAll` | player | public |
| 1530 | `CBA_Options_SiegeLimit_Recount` | player | public |
| 1617 | `CBA_Options_HasSiegeEngineers` | player | public |
| 1627 | `CBA_Options_SiegeLimit_ApplyThreshold` | player, opt_siege_queued | public |
| 1696 | `CBA_Options_BuildingLimit_RecountPlayer` | player | public |
| 1765 | `CBA_Options_BuildingLimit_EnforceExcess` | player | public |
| 1807 | `_kill_excess` | list, cap, label | local |
| 1824 | `CBA_Options_EnforcePopulationCap` | player | public |
| 1878 | `CBA_Options_EnforcePostTransfer` | player | public |
| 1906 | `CBA_Options_EnforcePostTransfer_Recount` | player | public |
| 1915 | `CBA_Options_EnforcePostTransfer_Enforce` | player | public |
| 1933 | `CBA_Options_EnforcePostTransfer_UI` | player | public |
| 1944 | `CBA_Options_RevalidateAll` | player | public |
| 1960 | `CBA_Options_RevalidateAllPlayers` | — | public |
| 1971 | `CBA_Options_SiegeLimit_Reconcile` | — | public |
| 2048 | `CBA_Options_FieldConstruct_Gate` | player | public |
| 2141 | `CBA_Options_RamLimit_Disable` | player_id, lock_type | public |
| 2170 | `CBA_Options_RamTowerOnly_Disable` | player_id, lock_type | public |
| 2178 | `CBA_Options_SiegeTowerLimit_Disable` | player_id, lock_type | public |
| 2196 | `CBA_Options_RamLimit_ApplyThreshold` | player, opt_ram_queued | public |
| 2236 | `CBA_Options_SiegeTowerLimit_ApplyThreshold` | player, opt_st_queued | public |
| 2268 | `CBA_Options_GetRamLimitMax` | — | public |
| 2272 | `CBA_Options_GetSiegeTowerLimitMax` | — | public |
| 2280 | `CBA_Options_ValidateEnforcement` | player, context_label | public |
| 2321 | `CBA_Options_RamLimit_EnforceSpawnCap` | player, spawned_squad | public |
| 2371 | `CBA_Options_SiegeLimit_EnforceSpawnCap` | player, spawned_squad | public |
| 2419 | `CBA_Options_SiegeLimit_RollbackExcessScaffolds` | player, excess_pts | public |
| 2453 | `CBA_Options_IsRamTowerSBP` | sbp, player_civ | public |
| 2467 | `CBA_Options_IsRamTowerSquad` | squad, player_civ | public |
| 2479 | `CBA_Options_IsRamTowerEBP` | ebp, player_civ | public |
| 2493 | `CBA_Options_IsRamTowerEntity` | entity, player_civ | public |
| 2511 | `CBA_Options_GetSiegeWeaponBPMaps` | player_civ | public |
| 2522 | `add_bp` | key, default_pts, opt_ottoman_pts | local |
| 2589 | `CBA_Options_IsSiegeWeaponBPMatch_EBP` | ebp, player_civ | public |
| 2598 | `CBA_Options_IsSiegeWeaponBPMatch_SBP` | sbp, player_civ | public |
| 2612 | `CBA_Options_GetSiegeWeaponPointsSBP` | sbp, player_civ | public |
| 2648 | `CBA_Options_GetSiegeWeaponPointsEBP` | ebp, player_civ | public |
| 2680 | `CBA_Options_GetSiegeWeaponPointsEntity` | entity, player_civ | public |
| 2715 | `CBA_Options_GetRamWeight` | squad, player_civ | public |
| 2722 | `CBA_Options_GetRamWeightSBP` | sbp, player_civ | public |
| 2729 | `CBA_Options_GetRamWeightEntity` | entity, player_civ | public |
| 2736 | `CBA_Options_RamLimit_RollbackExcessScaffolds` | player, excess_weight | public |
| 2771 | `CBA_Options_RamLimit_Recount` | player | public |
| 2838 | `CBA_Options_SiegeTowerLimit_Recount` | player | public |
| 2894 | `_CBA_Options_ForEachQueueSpawnItem` | player, callback | local |
| 2918 | `_CBA_Options_GetAllQueuedCounts` | player | private |
| 2940 | `CBA_Options_RamLimit_GetQueuedCount` | player | public |
| 2955 | `CBA_Options_SiegeTowerLimit_GetQueuedCount` | player | public |
| 2966 | `CBA_Options_RamLimit_TrimQueue` | player, opt_ram_queued | public |
| 2997 | `CBA_Options_SiegeTowerLimit_TrimQueue` | player, opt_st_queued | public |
| 3022 | `CBA_Options_SiegeLimit_GetQueuedPoints` | player | public |
| 3035 | `CBA_Options_SiegeLimit_TrimQueue` | player, opt_siege_queued | public |
| 3064 | `CBA_Options_SiegeLimit_GetGateTotals` | player | public |
| 3094 | `Debug_SiegePerfReset` | — | public |
| 3099 | `Debug_SiegePerfReport` | — | public |
| 3105 | `Debug_SiegeStatus` | — | public |
| 3124 | `Debug_RecountValidate` | — | public |

### gameplay/cba_siege_data.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 635 | `AGS_GetSiegeEntity` | player_civ, bp_type | public |
| 650 | `AGS_GetSiegeUnit` | player_civ, bp_type | public |

### gameplay/cba_training.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 9 | `Tutorials_MissionZero_HighlightAgeUp` | — | public |
| 65 | `MissionZero_AgeUpFeudalTrigger` | goalSequence | public |
| 75 | `Predicate_FeudalLandmarkBeingPlaced` | goal | public |
| 83 | `Predicate_FeudalLandmarkPlaced` | goal | public |
| 90 | `IgnorePredicate_AgeUpFeudalBuilt` | goalSequence | public |
| 101 | `MissionZero_PickConvenientVillager` | mustBeIdle | public |
| 133 | `AgeUpFeudal_Monitor` | — | public |
| 142 | `AgeUpFeudal_OnComplete` | — | public |
| 148 | `IntroProgressToFeudalAge_OnComplete` | — | public |
| 154 | `AddLandmarkHintpoint` | — | public |
| 159 | `ProgressAgeFeudal_OnConstructionStart` | context | public |
| 184 | `Tutorials_MissionZero_HighlightAgeUpCastle` | — | public |
| 214 | `UserHasSelectedAVillagerAgeUpCastle_MissionZero` | goalSequence | public |
| 224 | `Predicate_AgeUpCastleBuilt` | goal | public |
| 230 | `IgnorePredicate_AgeUpCastleBuilt` | goalSequence | public |

## helpers

### helpers/ags_blueprints.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 171 | `AGS_CivTableHasExplicitFalse` | civ, key | public |
| 2446 | `AGS_GetCivilizationEntity` | player_civ, bp_type | public |
| 2460 | `AGS_GetCivilizationUnit` | player_civ, bp_type | public |
| 2476 | `AGS_GetCivilizationUpgrade` | player_civ, bp_type | public |
| 2488 | `AGS_GetNeutralEntity` | bp_type | public |
| 2492 | `AGS_GetNeutralUnit` | bp_type | public |
| 2496 | `AGS_EGroupName` | player_id, entity_category | public |
| 2500 | `AGS_SGroupName` | player_id, unit_category | public |
| 2504 | `AGS_EGroupNeutralName` | unique_num, egroup_focus_name | public |
| 2509 | `AGS_SpawnEntity` | player_id, egroup_name, bp_entity, position, position_offset, opt_do_rounding | public |
| 2542 | `AGS_SpawnSquad` | player_id, sgroup_name, bp_squad, position, position_offset, count | public |
| 2564 | `AGS_Print` | text, opt_data, opt_level | public |
| 2576 | `AGS_WarnNilBlueprint` | api_name, bp_kind, context | public |
| 2583 | `AGS_SetEntityProductionAvailabilitySafe` | player_id, ebp, lock_type, context | public |
| 2592 | `AGS_SetSquadProductionAvailabilitySafe` | player_id, sbp, lock_type, context | public |
| 2601 | `AGS_CompleteUpgradeSafe` | player_id, ubp, context | public |
| 2610 | `AGS_IsSBPOfTypeSafe` | sbp, sbp_type, context | public |
| 2618 | `AGS_IsMutualRelation` | first_id, second_id, relation | public |
| 2622 | `AGS_CountItems` | table | public |
| 2629 | `AGS_IsACapital` | entity_id | public |
| 2633 | `AGS_IsALandmark` | entity_id | public |
| 2637 | `AGS_IsATownCenter` | entity_id | public |
| 2641 | `AGS_IsAKeep` | entity_id | public |
| 2645 | `AGS_IsAWonder` | entity_id | public |
| 2649 | `AGS_IsThisSpecialMobileBuildingDead` | entity_id | public |
| 2655 | `AGS_IsLocalGame` | — | public |
| 2662 | `AGS_ApplyUpgrade` | player_id, upgrade | public |
| 2669 | `AGS_RemoveUpgrade` | player_id, upgrade | public |
| 2676 | `AGS_CalculateCenterOffset` | start, x_offset, z_offset | public |
| 2699 | `AGS_GetRelation` | player | public |
| 2713 | `AGS_Contains` | table, value | public |
| 2722 | `AGS_GetFreeItems` | all, used | public |

### helpers/ags_starts.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 15 | `AGS_Starts_GetStartPosition` | player_id | public |

### helpers/ags_teams.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 19 | `AGS_Teams_EarlyInitializations` | — | public |
| 25 | `AGS_Teams_OnPlayerDefeated` | player, reason | public |
| 47 | `AGS_Teams_CreateInitialTeams` | — | public |
| 66 | `AGS_Teams_CreateFFA` | — | public |
| 78 | `AGS_Teams_CreateStaticTeams` | — | public |
| 106 | `AGS_Teams_DoesWinnerGroupExists` | — | public |
| 120 | `AGS_Teams_IsTeamAlive` | player_id | public |
| 132 | `AGS_Teams_GetSoloTeamWinner` | — | public |
| 146 | `AGS_Teams_GetStaticTeamWinnders` | — | public |
| 158 | `AGS_Teams_GetDynamicTeamWinners` | — | public |
| 181 | `AGS_Teams_GetStaticTeamAliveMembers` | team_mates | public |
| 199 | `AGS_Teams_GetAllMutualFriendshipPlayers` | player | public |
| 212 | `AGS_Teams_GetAllCurrentOpponents` | player, opt_all | public |
| 240 | `AGS_Teams_GetAllCurrentTeammates` | player, opt_all | public |
| 264 | `AGS_Teams_IsTeamVictoryEligible` | player | public |
| 269 | `AGS_Teams_AreTeamVictoryEligible` | player, other_player | public |
| 289 | `AGS_Teams_CountAliveInGroup` | group_table | public |
| 299 | `AGS_Teams_CountAlivePlayers` | — | public |
| 303 | `AGS_Teams_CountAliveAllies` | player | public |

## observerui

### observerui/gamestatetracking/ontributesent.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 10 | `ObserverUI_GameStateTracking_Tribute_OnTributeSent` | tributes | public |

### observerui/observerui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 47 | `ObserverUI_OnInit` | — | public |
| 99 | `SwitchBetween_ReplayStatViewer_And_ImprovedUI` | — | public |
| 103 | `Set_ReplayStatViewer_And_ImprovedUI_Visibility` | improvedUIIsVisible | public |
| 113 | `ShowImprovedUI` | — | public |
| 157 | `ShowClassicUI` | — | public |

### observerui/observeruiinitialization.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `ObserverUiInitialization:AddInitializable` | initializable, restrictTo2OrLessPlayers | public |
| 9 | `ObserverUiInitialization:Initialize` | — | public |
| 13 | `ObserverUiInitialization:Reset` | — | public |
| 17 | `ObserverUiInitialization:Resume` | — | public |
| 21 | `ObserverUiInitialization:Stop` | — | public |
| 25 | `ObserverUiInitialization:_Do` | method | public |

### observerui/observeruimessagesystem.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 9 | `ObserverUiMessageSystem:GetMessages` | — | public |
| 36 | `ObserverUiMessageSystem:AddMessage` | message | public |

### observerui/observeruirulesystem.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 7 | `ObserverUiRuleSystem:Initialize` | — | public |
| 19 | `ObserverUiRuleSystem:Reset` | — | public |
| 31 | `ObserverUiRuleSystem:Stop` | — | public |
| 39 | `ObserverUiRuleSystem:Resume` | — | public |
| 47 | `ObserverUiRuleSystem:AddSquadDataGatheringRule` | playerId, squadType, rule | public |
| 51 | `ObserverUiRuleSystem:AddEntityDataGatheringRule` | playerId, entityType, rule | public |
| 55 | `ObserverUiRuleSystem:AddDataGatheringPreparationRule` | playerId, rule | public |
| 59 | `ObserverUiRuleSystem:AddDataProcessingRule` | playerId, rule | public |
| 63 | `ObserverUiRuleSystem:AddUpdateUiDataContextForPlayerRule` | playerId, rule | public |
| 67 | `ObserverUiRuleSystem:AddUpdateUiDataContextRule` | rule | public |
| 71 | `ObserverUiRuleSystem:AddApplyUiDataContextRule` | rule | public |
| 75 | `_NoOp` | — | private |
| 79 | `_OneRuleToRingThemAll_TrackAlways` | — | private |
| 84 | `_OneRuleToRingThemAll_OnlyTrackWhenUpdatingUi` | — | private |
| 88 | `_OneRuleToRingThemAll` | updateUi | private |
| 111 | `ObserverUiRuleSystem:_InitializeDataStructure` | playerId | public |
| 119 | `routerForSquads` | group, index, squad | local |
| 129 | `routerForEntities` | group, index, entity | local |
| 151 | `ObserverUiRuleSystem:_AddRule` | playerId, rule, ... | public |

### observerui/observeruiupdateui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `AdaptIconPathForXaml` | iconPath | public |
| 50 | `InitializeObserverUIDataContext` | — | public |
| 100 | `PrepareObserverUIDataContextFor1v1` | — | public |
| 111 | `AssignSideToPlayerDataContexts` | — | public |
| 123 | `SwapSides` | — | public |
| 134 | `SwapPlayers1v1` | — | public |
| 141 | `ToggleSymmetricalUi` | — | public |
| 147 | `EfficiencyStatisticsDisplayModeCommand` | — | public |
| 153 | `ToggleMessages` | — | public |
| 159 | `ToggleArmy` | — | public |
| 164 | `SwapResourceWithIncomePerMinute` | — | public |
| 173 | `UpdateObserverUIDataContext` | — | public |
| 197 | `UpdateResources` | t, player | public |
| 214 | `GetPopulationVsMaximumPopulation` | player | public |
| 226 | `UpdatePopulationComposition` | t, player | public |
| 231 | `UpdateRelics` | t, player | public |
| 235 | `DismissErrors` | default, func | public |
| 244 | `GetIconNameFromSquadBlueprintUnsafe` | pbg, race | public |
| 248 | `GetIconNameFromSquadBlueprint` | pbg, race | public |
| 252 | `GetIconNameFromUpgradeBlueprintUnsafe` | pbg | public |
| 256 | `GetIconNameFromUpgradeBlueprint` | pbg | public |
| 260 | `HasMilitaryIcon` | bp, race | public |
| 264 | `AddOrAggregateCountWithExisting` | t, icon, count | public |
| 272 | `AddOrAggregateisMilitaryWithExisting` | t, icon, isMilitary | public |
| 280 | `GetUnits` | player, race, isMilitary | public |
| 295 | `GetQueuedStuff` | player, race, isMilitary | public |
| 315 | `HashSetToArray` | t | public |
| 323 | `BuildUnitsUiTable` | units, queued | public |
| 347 | `SplitByIsMilitary` | units, isMilitary | public |
| 361 | `UpdateUnitsAndQueuedStuff` | t, player, race | public |
| 389 | `CompareUnitCount` | unit1, unit2 | public |
| 396 | `UpdateIsUpping` | t, player | public |
| 401 | `UpdateCivSpecifics` | t, player | public |
| 409 | `UpdateEfficiencyStatistics` | playerTable, player | public |

### observerui/tracking_agingupprogress.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `AgingUpProgress:Initialize` | — | public |
| 12 | `AgingUpProgress:GetForPlayer_IsAgingUp_Progress_EstimatedTimeOfCompletion_Icon_Name` | player | public |
| 36 | `AgingUpProgress:_GetTrackingIntervalInTicks` | — | public |
| 40 | `AgingUpProgress:_Initialize` | player | public |
| 48 | `AgingUpProgress:_InitializeForAbbasid` | player | public |
| 52 | `rule` | — | local |
| 93 | `AgingUpProgress:_InitializeForNonAbbasid` | player | public |
| 96 | `rule` | — | local |
| 120 | `AgingUpProgress:_UpdateLandmarkProgress` | oldProgresses, newProgresses, entity | public |
| 134 | `AgingUpProgress:_GetForNonAbbasidPlayer_IsAgingUp` | player | public |
| 138 | `AgingUpProgress:_GetForNonAbbasidPlayer_Progress_EstimatedTimeOfCompletion_UiInfo` | player | public |
| 154 | `AgingUpProgress:_GetForAbbasidPlayer_IsAgingUp` | player | public |
| 158 | `AgingUpProgress:_GetForAbbasidPlayer_Progress_EstimatedTimeOfCompletion_UiInfo` | player | public |

### observerui/tracking_aginguptimings.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 13 | `AgingUpTimings:Initialize` | — | public |
| 24 | `AgingUpTimings:_Initialize` | player | public |
| 34 | `rule` | — | local |
| 64 | `AgingUpTimings:_AbbasidPlayerCanAffordNextAge` | player, age | public |
| 72 | `AgingUpTimings:_NonAbbasidPlayerCanAffordNextAge` | player, age | public |
| 83 | `AgingUpTimings:_PlayerCanAffordNextAge` | player, age | public |
| 90 | `AgingUpTimings:_IsAgingUp` | player, age | public |
| 112 | `AgingUpTimings:_AddAgeUpTimeDifferenceBetweenPlayersMessage` | age | public |
| 142 | `AgingUpTimings:_AddTimeBetweenCanAffordAndAgeUpMessage` | agingUpTimingsOfPlayer, age | public |

### observerui/tracking_gameobjectrepository.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `GameObjectRepository:Initialize` | — | public |
| 18 | `GameObjectRepository:_Initialize` | player | public |
| 22 | `preparation` | — | local |
| 28 | `preparation` | — | local |
| 34 | `rule` | entity | local |
| 45 | `preparation` | — | local |
| 51 | `rule` | entity | local |
| 68 | `preparation` | — | local |
| 73 | `rule` | entity | local |

### observerui/tracking_ownedsquads.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `OwnedSquads:Initialize` | — | public |
| 12 | `OwnedSquads:GetForPlayer` | player | public |
| 16 | `OwnedSquads:_Initialize` | player | public |
| 17 | `rule` | — | local |
| 23 | `rule` | squad | local |

### observerui/tracking_populationcapped.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `PopulationCapped:InitializePerPlayer` | i | public |
| 19 | `rule` | — | local |
| 28 | `PopulationCapped:GetForPlayer` | i | public |

### observerui/tracking_populationcomposition.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `PopulationComposition:Initialize` | — | public |
| 12 | `PopulationComposition:GetForPlayer_Worker_WorkerIdle_Military_MilitaryNonSiege_Siege` | player | public |
| 19 | `PopulationComposition:GetForPlayer_WorkerNonTrade_Trade_WorkerIdle_MilitaryNonSiege_Siege` | player | public |
| 25 | `PopulationComposition:_Initialize` | player | public |
| 35 | `rule` | — | local |
| 47 | `rule` | squad | local |
| 60 | `rule` | squad | local |

### observerui/tracking_queuedstuff.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `QueuedStuff:Initialize` | — | public |
| 12 | `QueuedStuff:GetForPlayer` | player | public |
| 16 | `QueuedStuff:_Initialize` | player | public |
| 17 | `rule` | — | local |
| 24 | `rule` | entity | local |

### observerui/tracking_reliclocations.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `RelicLocations:Initialize` | — | public |
| 12 | `RelicLocations:GetForPlayer_Carried_Deposited` | player | public |
| 17 | `RelicLocations:_Initialize` | player | public |
| 24 | `rule` | — | local |
| 32 | `rule` | squad | local |
| 40 | `rule` | entity | local |

### observerui/tracking_squadlosses.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `SquadLosses:GetForPlayer_Worker_Military` | i | public |
| 10 | `SquadLosses:Initialize` | — | public |
| 15 | `onSquadKilledRule` | context | local |
| 34 | `SquadLosses:InitializePerPlayer` | i | public |
| 43 | `SquadLosses:Reset` | — | public |
| 47 | `_OnSquadKilledRule` | context | private |

### observerui/tracking_towncenteridling.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `TownCenterIdling:Initialize` | — | public |
| 16 | `TownCenterIdling:GetForPlayer_IdleTime_Efficiency` | player | public |
| 29 | `TownCenterIdling:_Initialize` | player | public |
| 38 | `rule` | entity | local |
| 48 | `rule` | entity | public |
| 59 | `rule` | entity | public |

### observerui/tracking_workeridling.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `WorkerIdling:Initialize` | — | public |
| 16 | `WorkerIdling:GetForPlayer_IdleTime_Efficiency` | player | public |
| 29 | `WorkerIdling:_Initialize` | player | public |
| 45 | `rule` | squad | local |

### observerui/uidatacontext/initialize_numberofplayers.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiNumberOfPlayers:Initialize` | — | public |

### observerui/uidatacontext/initialize_observeruidatacontextmappings.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 9 | `ObserverUIDataContextMappings:Initialize` | — | public |
| 53 | `ComparePlayers` | player1, player2 | public |
| 57 | `ObserverUIDataContextMappings:_GetTeamConfiguration` | — | public |

### observerui/uidatacontext/updateui_landmarkvictory.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiLandmarkVictory:Initialize` | — | public |
| 22 | `rule` | — | local |

### observerui/uidatacontext/updateui_messages.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 12 | `UiMessages:Initialize` | — | public |
| 17 | `rule` | — | local |

### observerui/uidatacontext/updateui_populationcapped.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiPopulationCapped:InitializePerPlayer` | i | public |
| 15 | `rule` | — | local |

### observerui/uidatacontext/updateui_squadlosses.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiSquadLosses:InitializePerPlayer` | i | public |
| 14 | `rule` | — | local |

### observerui/uidatacontext/updateui_teamsummary.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiTeamSummary:Initialize` | — | public |
| 31 | `rule` | — | local |

### observerui/uidatacontext/updateui_victorycountdowns.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 5 | `UiVictoryCountdowns:Initialize` | — | public |
| 17 | `rule` | — | local |

## playerui

### playerui/playerui_animate.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 86 | `_PlayerUI_SafeElapsed` | pb, gameTime | private |
| 102 | `_PlayerUI_EaseOut` | t | private |
| 108 | `_PlayerUI_EaseIn` | t | private |
| 114 | `_PlayerUI_EaseInOut` | t | private |
| 124 | `_PlayerUI_SafeQueueEntry` | queue, index | private |
| 141 | `_PlayerUI_ValidateHexColor` | colorStr | private |
| 153 | `_PlayerUI_EnsureRewardsContext` | — | private |
| 166 | `_PlayerUI_SetIfChanged` | t, k, v | private |
| 186 | `_PlayerUI_GetOffsetXMargin` | offsetX | private |
| 203 | `_PlayerUI_GetStripOffsetMargin` | offsetX | private |
| 224 | `_PlayerUI_LerpHexColor` | colorA, colorB, t | private |
| 240 | `PlayerUI_Animate_Debug_ResetEliminationDiag` | — | public |
| 252 | `PlayerUI_Animate_Debug_PrintEliminationDiag` | — | public |
| 263 | `PlayerUI_Animate_GetEliminationLastProgress` | playerIndex | public |
| 271 | `PlayerUI_Animate_Debug_RetriggerElimFade` | index | public |
| 319 | `PlayerUI_Animate_Init` | — | public |
| 339 | `PlayerUI_Animate_SetTarget` | key, value, easing | public |
| 377 | `PlayerUI_Animate_GetDisplay` | key | public |
| 392 | `_PlayerUI_Animate_Tick` | — | private |
| 646 | `PlayerUI_Animate_SetPosition` | key, value | public |
| 657 | `PlayerUI_Animate_SetPositionTarget` | key, target | public |
| 673 | `PlayerUI_Animate_GetPosition` | key | public |
| 682 | `PlayerUI_Animate_HasArrived` | key | public |
| 692 | `PlayerUI_Animate_IsTransitioning` | key | public |
| 699 | `PlayerUI_Animate_TriggerDecay` | key, startValue, decayRate | public |
| 710 | `PlayerUI_Animate_GetDecay` | key | public |
| 719 | `PlayerUI_Animate_TriggerScorePulse` | playerIndex, newScore | public |
| 742 | `_PlayerUI_GlowFill` | opacity | local |
| 750 | `_PlayerUI_RowDimFill` | opacity | private |
| 758 | `_PlayerUI_NormalizeBorderColor` | color | local |
| 770 | `_PlayerUI_SmoothRewardIcons` | newIcons | private |
| 895 | `_PlayerUI_TickRewardIconSmoothing` | — | private |
| 988 | `_PlayerUI_FillPreviewSlots` | icons, player, pb, excludeMilestone | private |
| 1023 | `PlayerUI_Animate_ApplyDisplayValues` | — | public |
| 1550 | `PlayerUI_Animate_IsEliminationTransitionActive` | playerIndex | public |
| 1555 | `_PlayerUI_EliminationStateFromProgress` | progress | local |
| 1563 | `PlayerUI_Animate_ApplyEliminationTransitionFinalVisual` | data | public |
| 1582 | `PlayerUI_Animate_EliminationTransition` | playerIndex, duration, data | public |
| 1625 | `PlayerUI_Animate_GetEliminationState` | playerIndex | public |
| 1672 | `PlayerUI_Animate_ClearEliminationAnim` | playerIndex | public |
| 1683 | `PlayerUI_Animate_IsEliminationRevealActive` | playerIndex | public |
| 1688 | `_PlayerUI_RevealStateFromProgress` | progress | local |
| 1697 | `PlayerUI_Animate_EliminationReveal` | playerIndex, duration, data | public |
| 1727 | `PlayerUI_Animate_GetEliminationRevealState` | playerIndex | public |
| 1757 | `PlayerUI_Animate_ClearEliminationReveal` | playerIndex | public |
| 1768 | `PlayerUI_Animate_IsEliminationGlowActive` | playerIndex | public |
| 1773 | `_PlayerUI_GlowOpacityFromProgress` | progress | local |
| 1780 | `PlayerUI_Animate_EliminationGlow` | playerIndex, duration, data | public |
| 1809 | `PlayerUI_Animate_GetEliminationGlowState` | playerIndex | public |
| 1839 | `PlayerUI_Animate_ClearEliminationGlow` | playerIndex | public |
| 1847 | `PlayerUI_Animate_Reset` | — | public |

### playerui/playerui_initialization.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `PlayerUiInitialization:AddInitializable` | initializable | public |
| 15 | `PlayerUiInitialization:Initialize` | — | public |
| 19 | `PlayerUiInitialization:Reset` | — | public |
| 23 | `PlayerUiInitialization:Stop` | — | public |
| 27 | `PlayerUiInitialization:_Do` | method | public |

### playerui/playerui_ranking.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 66 | `_PlayerUI_Ranking_LogLock` | msg | local |
| 72 | `_Ranking_HasActiveEliminationSettleWindow` | — | private |
| 96 | `PlayerUI_Ranking_Init` | — | public |
| 121 | `_Ranking_BuildTeamState` | teamKey, teamSlots | private |
| 152 | `_Ranking_ComputePulseWindowEndTime` | now, period | private |
| 156 | `_Ranking_DebugInjectOneUpdate` | teamKey, rows | private |
| 169 | `PlayerUI_Ranking_Update` | — | public |
| 179 | `_Ranking_UpdateTeam` | teamKey, teamSlots, gameTime | private |
| 365 | `_Ranking_PinTopPlayer` | sorted, gameTime | private |
| 410 | `_Ranking_UpdateContestedFlags` | entries | private |
| 432 | `_Ranking_ComputePredictions` | entries | private |
| 487 | `_Ranking_WriteFieldsToSlots` | entries | private |
| 724 | `_Ranking_ProcessDeferredTarget` | — | private |
| 734 | `_Ranking_CleanStaleAnimKeys` | teamKey, teamSize | private |
| 751 | `_Ranking_StartFlipAnimation` | teamKey, sorted, movers | private |
| 812 | `_Ranking_ReorderDataContextArrays` | teamKey, sorted | private |
| 842 | `_Ranking_GetOffsetMargin` | translateY | private |
| 867 | `_Ranking_CheckTransitionConverged` | — | private |
| 933 | `PlayerUI_Ranking_ApplyAnimatedFields` | — | public |
| 1104 | `PlayerUI_Ranking_Reset` | — | public |
| 1117 | `PlayerUI_Ranking_DebugForceSwap` | teamKey, idx1, idx2 | public |
| 1171 | `PlayerUI_Debug_ForcePredictionState` | playerIndex, state, count | public |
| 1272 | `_PlayerUI_Debug_FindPredictionEntry` | slot | local |
| 1289 | `_PlayerUI_Debug_PredictionVisibilitySnapshot` | slot | local |
| 1326 | `PlayerUI_Debug_AuditPredictionVisibility` | playerIndex | public |
| 1430 | `PlayerUI_Debug_ForcePredictionCase` | playerIndex, caseName | public |
| 1566 | `PlayerUI_Debug_DemoPredictionStates` | — | public |
| 1597 | `PlayerUI_Ranking_DebugPrintState` | — | public |
| 1648 | `PlayerUI_Ranking_DebugSetScore` | teamKey, idx, newScore | public |
| 1677 | `PlayerUI_Debug_PredictionSnapshot` | tag, playerIndex | public |
| 1788 | `PlayerUI_Debug_ForceWaitAudit` | caseName, waitSeconds | public |
| 1811 | `_PlayerUI_Debug_FWA_DeferredAudit` | — | private |
| 1839 | `PlayerUI_Debug_PredictionDiagnostics` | — | public |
| 1871 | `PlayerUI_Ranking_DebugTestPredictions` | — | public |
| 1989 | `PlayerUI_Debug_SystemStatus` | — | public |
| 2092 | `PlayerUI_Debug_TestStability` | — | public |
| 2200 | `PlayerUI_Debug_TestContestedCollapse` | — | public |
| 2307 | `PlayerUI_Debug_TestSettingsMatrix` | — | public |

### playerui/playerui_rulesystem.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 13 | `PlayerUiRuleSystem:Initialize` | — | public |
| 32 | `PlayerUiRuleSystem:Reset` | — | public |
| 52 | `PlayerUiRuleSystem:Stop` | — | public |
| 58 | `PlayerUiRuleSystem:Resume` | — | public |
| 64 | `PlayerUiRuleSystem:AddSquadDataGatheringRule` | playerId, squadType, rule | public |
| 68 | `PlayerUiRuleSystem:AddEntityDataGatheringRule` | playerId, entityType, rule | public |
| 72 | `PlayerUiRuleSystem:AddDataGatheringPreparationRule` | playerId, rule | public |
| 76 | `PlayerUiRuleSystem:AddDataProcessingRule` | playerId, rule | public |
| 80 | `PlayerUiRuleSystem:AddUpdateUiDataContextForPlayerRule` | playerId, rule | public |
| 84 | `PlayerUiRuleSystem:AddUpdateUiDataContextRule` | rule | public |
| 88 | `PlayerUiRuleSystem:AddApplyUiDataContextRule` | rule | public |
| 96 | `_PlayerUI_NoOp` | — | private |
| 104 | `_PlayerUI_RingRule` | — | private |
| 131 | `PlayerUiRuleSystem:_InitializeDataStructure` | playerId | public |
| 142 | `routerForSquads` | group, index, squad | local |
| 153 | `routerForEntities` | group, index, entity | local |
| 177 | `PlayerUiRuleSystem:_AddRule` | playerId, rule, ... | public |

### playerui/playerui_updateui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 18 | `PlayerUI_ResetEliminationPresentationState` | — | public |
| 54 | `_PlayerUI_GetEliminationPresentationKey` | isEliminated, showEliminationPresentation, eliminationReason | private |
| 70 | `_PlayerUI_ApplyEliminationPresentationIfChanged` | data, presentationKey | private |
| 168 | `_PlayerUI_GetEliminationSteadyVisualKey` | isEliminated, dimEnabled | private |
| 178 | `_PlayerUI_ApplyEliminationSteadyVisualIfChanged` | data, steadyVisualKey | private |
| 186 | `setIfChanged` | t, k, v | public |
| 214 | `PlayerUI_Debug_PrintEliminationSnapshot` | index | public |
| 247 | `_PlayerUI_Debug_GetAnimEntryValue` | key, field, fallback | local |
| 259 | `_PlayerUI_Debug_GetDecayValue` | key | local |
| 267 | `PlayerUI_Debug_PrintFullSnapshot` | index | public |
| 344 | `_PlayerUI_IsEliminationAnimationActive` | index | private |
| 351 | `PlayerUI_UpdateEliminationPresentationForIndex` | index, playersEntryOverride | public |
| 443 | `PlayerUI_AdaptIconPathForXaml` | iconPath | public |
| 481 | `_PlayerUI_LerpColor` | c1, c2, t | private |
| 488 | `_PlayerUI_GetScoreColor` | score | private |
| 500 | `_PlayerUI_GetScoreGlowTier` | score | private |
| 510 | `PlayerUI_InitializeDataContext` | — | public |
| 629 | `PlayerUI_UpdateDataContext` | — | public |
| 873 | `PlayerUI_GetElapsedTimeDisplay` | — | public |
| 892 | `PlayerUI_UpdateTeamSummaries` | — | public |
| 950 | `PlayerUI_UpdateResources` | t, player | public |
| 981 | `PlayerUI_ApplyDataContext` | — | public |
| 1001 | `PlayerUI_GetPopulationVsMaximumPopulation` | player | public |
| 1011 | `PlayerUI_GetMaxPopulationDisplay` | player | public |
| 1020 | `PlayerUI_UpdatePopulationComposition` | t, player | public |
| 1040 | `PlayerUI_UpdateRelics` | t, player | public |
| 1048 | `PlayerUI_UpdateIsUpping` | t, player | public |
| 1057 | `PlayerUI_UpdateCivSpecifics` | t, player | public |
| 1068 | `PlayerUI_DismissErrors` | default, func | public |
| 1076 | `PlayerUI_GetIconNameFromSquadBlueprint` | pbg, race | public |
| 1080 | `PlayerUI_GetIconNameFromUpgradeBlueprint` | pbg | public |
| 1084 | `PlayerUI_HasMilitaryIcon` | bp, race | public |
| 1092 | `PlayerUI_GetUnits` | player, race, isMilitary | public |
| 1112 | `PlayerUI_GetQueuedStuff` | player, race, isMilitary | public |
| 1137 | `PlayerUI_HashSetToArray` | t | public |
| 1145 | `PlayerUI_BuildUnitsUiTable` | units, queued | public |
| 1166 | `PlayerUI_SplitByIsMilitary` | units, isMilitary | public |
| 1179 | `PlayerUI_CompareUnitCount` | unit1, unit2 | public |
| 1186 | `PlayerUI_UpdateUnitsAndQueuedStuff` | t, player, race | public |
| 1223 | `PlayerUI_GetLimitColors` | current, max | public |
| 1237 | `PlayerUI_UpdateLimits` | — | public |
| 1314 | `PlayerUI_GetNormalizedRewardTitle` | reward, player_id, raceName | public |
| 1359 | `PlayerUI_GetNextRewardTitle` | playersEntry | public |
| 1388 | `PlayerUI_GetNextRewardIcon` | playersEntry | public |
| 1399 | `PlayerUI_BuildRewardPreview` | player, count | public |
| 1468 | `PlayerUI_GetRewardProgressBounds` | current_kills, player_civ, objective_next_req | public |
| 1507 | `PlayerUI_ReconstructCrossedThresholds` | player_civ, old_req, new_req | public |
| 1529 | `PlayerUI_BuildPlaybackMilestone` | player, player_civ, threshold | public |
| 1587 | `PlayerUI_UpdateRewardProgress` | — | public |
| 1733 | `PlayerUI_RewardPlayback_AdvanceQueue` | pb, current_kills | public |
| 1778 | `PlayerUI_TrySetObjectiveVisible` | objectiveId, isVisible | public |
| 1789 | `PlayerUI_SetObjectivesVisible` | isVisible | public |
| 1840 | `PlayerUI_Toggle_TrySetProperty` | target, property, value | public |
| 1849 | `PlayerUI_Toggle_TrySetObjectivesVisible` | isVisible | public |
| 1858 | `PlayerUI_ToggleTrace` | msg | public |
| 1865 | `PlayerUI_Debug_ToggleProbe` | path | public |
| 1900 | `PlayerUI_Toggle` | — | public |
| 1971 | `PlayerUI_SwapResourceWithIncomePerMinute` | — | public |

### playerui/playerui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 56 | `PlayerUI_OnInit` | — | public |
| 190 | `PlayerUI_PresetFinalize` | — | public |

### playerui/tracking/tracking_agingupprogress.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 12 | `PlayerUI_AgingUpProgress:Initialize` | — | public |
| 22 | `PlayerUI_AgingUpProgress:GetForPlayer_IsAgingUp_Progress_EstimatedTimeOfCompletion_Icon_Name` | player | public |
| 48 | `PlayerUI_AgingUpProgress:_GetTrackingIntervalInTicks` | — | public |
| 52 | `PlayerUI_AgingUpProgress:_Initialize` | player | public |
| 60 | `PlayerUI_AgingUpProgress:_InitializeForAbbasid` | player | public |
| 64 | `rule` | — | local |
| 106 | `PlayerUI_AgingUpProgress:_InitializeForNonAbbasid` | player | public |
| 109 | `rule` | — | local |
| 139 | `PlayerUI_AgingUpProgress:_UpdateLandmarkProgress` | oldProgresses, newProgresses, entity | public |
| 157 | `PlayerUI_AgingUpProgress:_GetForNonAbbasidPlayer_IsAgingUp` | player | public |
| 161 | `PlayerUI_AgingUpProgress:_GetForNonAbbasidPlayer_Progress_EstimatedTimeOfCompletion_UiInfo` | player | public |
| 181 | `PlayerUI_AgingUpProgress:_GetForAbbasidPlayer_IsAgingUp` | player | public |
| 185 | `PlayerUI_AgingUpProgress:_GetForAbbasidPlayer_Progress_EstimatedTimeOfCompletion_UiInfo` | player | public |

### playerui/tracking/tracking_gameobjectrepository.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 17 | `PlayerUI_GameObjectRepository:Initialize` | — | public |
| 27 | `PlayerUI_GameObjectRepository:_Initialize` | player | public |
| 31 | `preparation` | — | local |
| 37 | `abbasidPrep` | — | local |
| 43 | `rule` | entity | local |
| 54 | `chinesePrep` | — | local |
| 60 | `rule` | entity | local |
| 76 | `defaultPrep` | — | local |
| 81 | `rule` | entity | local |

### playerui/tracking/tracking_ownedsquads.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `PlayerUI_OwnedSquads:Initialize` | — | public |
| 21 | `PlayerUI_OwnedSquads:GetForPlayer` | player | public |
| 25 | `PlayerUI_OwnedSquads:_Initialize` | player | public |
| 26 | `resetRule` | — | local |
| 32 | `countRule` | squad | local |

### playerui/tracking/tracking_populationcomposition.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `PlayerUI_PopulationComposition:Initialize` | — | public |
| 21 | `PlayerUI_PopulationComposition:GetForPlayer_Worker_WorkerIdle_Military_MilitaryNonSiege_Siege` | player | public |
| 31 | `PlayerUI_PopulationComposition:_Initialize` | player | public |
| 41 | `resetRule` | — | local |
| 53 | `workerRule` | squad | local |
| 66 | `militaryRule` | squad | local |

### playerui/tracking/tracking_queuedstuff.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `PlayerUI_QueuedStuff:Initialize` | — | public |
| 21 | `PlayerUI_QueuedStuff:GetForPlayer` | player | public |
| 25 | `PlayerUI_QueuedStuff:_Initialize` | player | public |
| 26 | `resetRule` | — | local |
| 33 | `scanRule` | entity | local |

### playerui/tracking/tracking_reliclocations.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 11 | `PlayerUI_RelicLocations:Initialize` | — | public |
| 21 | `PlayerUI_RelicLocations:GetForPlayer_Carried_Deposited` | player | public |
| 29 | `PlayerUI_RelicLocations:_Initialize` | player | public |
| 36 | `resetRule` | — | local |
| 44 | `carriedRule` | squad | local |
| 52 | `depositedRule` | entity | local |

### playerui/uidatacontext/initialize_datacontext.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 16 | `PlayerUIDataContextMappings:Initialize` | — | public |

## rewards

### rewards/cba_kill_scoring.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 24 | `CBA_GetKillPoints` | victim | public |

### rewards/cba_rewards_arena.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 9 | `CBA_Rewards_List_Arena` | — | public |

### rewards/cba_rewards_onslaught.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 8 | `CBA_Rewards_List_Onslaught` | — | public |

### rewards/cba_rewards.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 33 | `CBA_Rewards_UpdateModuleSettings` | — | public |
| 45 | `CBA_Rewards_PresetFinalize` | — | public |
| 276 | `CBA_Rewards_Start` | — | public |
| 280 | `CBA_Rewards_OnGameOver` | — | public |
| 287 | `CBA_Rewards_InitialSpawnWhenReady` | — | public |
| 301 | `CBA_Rewards_ToLocText` | value | public |
| 336 | `CBA_Rewards_FormatObjectiveTitle` | next_reward_title | public |
| 359 | `CBA_Rewards_SetupObjective` | — | public |
| 403 | `CBA_Rewards_SpawnUnits` | — | public |
| 433 | `CBA_Rewards_StartingUnits` | — | public |
| 443 | `CBA_Rewards_GetSpawnAnchor` | player | public |
| 470 | `CBA_Rewards_SpawnAndMove` | player, unit, num | public |
| 543 | `CBA_Rewards_nextRequirement` | player | public |
| 556 | `CBA_Rewards_OnEntityKilled` | context | public |
| 687 | `CBA_Rewards_ProcessQueue` | — | public |

## root

### ags_global_settings.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 233 | `AGS_GlobalSettings_SetupSettings` | options | public |
| 301 | `AGS_GlobalSettings_EarlyInitializations` | — | public |
| 307 | `AGS_GlobalSettings_OnGameOver` | — | public |
| 316 | `AGS_GlobalSettings_OnLocalPlayerChanged` | context | public |
| 328 | `AGS_GlobalSettings_DefineWinConditions` | category | public |
| 355 | `AGS_GlobalSettings_DefineGameConditions` | category | public |
| 381 | `AGS_GlobalSettings_DefineWinSettings` | category | public |
| 423 | `AGS_GlobalSettings_DefineGameSettings` | category | public |
| 467 | `AGS_GlobalSettings_DefinePlayerSettings` | category | public |
| 473 | `AGS_GlobalSettings_DefineMatchSettings` | category | public |
| 540 | `AGS_GlobalSettings_DefineLegacySettings` | category | public |
| 567 | `AGS_GlobalSettings_DefineHandicapSettings` | category | public |
| 574 | `AGS_GlobalSettings_DefineCbaSettings` | category | public |
| 582 | `AGS_GlobalSettings_DefineRestrictionSettings` | category | public |
| 614 | `AGS_GlobalSettings_SetMaintainTeamBalance` | maintain_team_balance | public |
| 641 | `AGS_GlobalSettings_SetSettlement` | settlement | public |
| 653 | `AGS_GlobalSettings_SetTreaty` | treaty | public |
| 661 | `AGS_GlobalSettings_SetTreatyTimer` | treaty | public |
| 691 | `AGS_GlobalSettings_SetTeamVictory` | team_victory | public |
| 701 | `AGS_GlobalSettings_SetWonderTimer` | wonder_timer | public |
| 743 | `AGS_GlobalSettings_SetWonderScaleCost` | scale_cost | public |
| 765 | `AGS_GlobalSettings_SetScoreTimer` | score_timer | public |
| 811 | `AGS_GlobalSettings_SetTeamVision` | team_vision | public |
| 821 | `AGS_GlobalSettings_SetMapVision` | map_vision | public |
| 831 | `AGS_GlobalSettings_SetStartingAge` | starting_age | public |
| 843 | `AGS_GlobalSettings_SetEndingAge` | ending_age | public |
| 857 | `AGS_GlobalSettings_SetTechnologyAge` | technology_age | public |
| 871 | `AGS_GlobalSettings_SetStartingResources` | starting_resources | public |
| 889 | `AGS_GlobalSettings_SetStartingVillagers` | starting_villagers | public |
| 939 | `AGS_GlobalSettings_SetStartingKeeps` | starting_keeps | public |
| 947 | `AGS_GlobalSettings_SetStartingKings` | starting_kings | public |
| 955 | `AGS_GlobalSettings_SetSimulationSpeed` | simulation_speed | public |
| 993 | `AGS_GlobalSettings_SetTownCenterRestricts` | tc_restrictions | public |
| 1003 | `AGS_GlobalSettings_SetHandicapType` | handicap_type | public |
| 1015 | `AGS_GlobalSettings_SetSlotHandicaps` | category | public |
| 1042 | `AGS_GlobalSettings_RetrieveSlotHandicap` | slot_handicap | public |
| 1076 | `AGS_GlobalSettings_SetReligiousTimer` | religious_timer | public |
| 1118 | `AGS_GlobalSettings_SetMinimumPopulation` | min_population | public |
| 1156 | `AGS_GlobalSettings_SetMaximumPopulation` | max_population | public |
| 1192 | `AGS_GlobalSettings_SetUnitRates` | unit_rates | public |
| 1218 | `AGS_GlobalSettings_SetGameRates` | game_rates | public |
| 1270 | `AGS_GlobalSettings_SetGatherRates` | gather_rates | public |
| 1320 | `AGS_GlobalSettings_SetAutoAge` | auto_age | public |
| 1332 | `AGS_GlobalSettings_SetPopulationinterval` | interval_population | public |
| 1352 | `AGS_GlobalSettings_SetMaximumMedicPopulation` | max_medicpopulation | public |
| 1376 | `AGS_GlobalSettings_SetMaximumProductionBuildings` | max_productionbuildings | public |
| 1400 | `AGS_GlobalSettings_SetMaximumSiegeWorkshop` | max_siegeworkshop | public |
| 1418 | `AGS_GlobalSettings_CBA_Rewards` | reward_list | public |

### cba_annihilation.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 64 | `Annihilation_DiplomacyEnabled` | is_enabled | public |
| 71 | `Annihilation_TributeEnabled` | is_enabled | public |
| 76 | `Annihilation_OnInit` | — | public |
| 92 | `Annihilation_Start` | — | public |
| 102 | `Annihilation_OnGameOver` | — | public |
| 113 | `Annihilation_OnConstructionComplete` | context | public |
| 130 | `Annihilation_OnLandmarkDestroyed` | context | public |
| 136 | `Annihilation_OnEntityKilled` | context | public |
| 141 | `Annihilation_CheckAnnihilationCondition` | victimOwner | public |
| 268 | `Annihilation_OnPlayerDefeated` | player, reason | public |
| 290 | `Annihilation_CheckVictory` | — | public |
| 343 | `Annihilation_GetActiveEnemyCount` | player | public |
| 363 | `Annihilation_IsACapital` | entity | public |
| 368 | `Annihilation_IsALandmark` | entity | public |
| 373 | `Annihilation_PlayerCanReceiveTribute` | player_id | public |
| 376 | `PlayerCanSendTribute` | player_id | local |
| 396 | `Annihilation_WinnerPresentation` | playerID | public |
| 414 | `Annihilation_LoserPresentation` | playerID | public |

### cba_religious.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 83 | `Religious_UpdateConditions` | _mod | public |
| 113 | `Religious_DiplomacyEnabled` | is_enabled | public |
| 118 | `Religious_OnInit` | — | public |
| 158 | `Religious_Start` | — | public |
| 178 | `Religious_OnPlayerDefeated` | player, reason | public |
| 197 | `Religious_OnGameOver` | — | public |
| 216 | `Religious_UpdatePlayerStats` | player, scarModel | public |
| 225 | `Religious_Update` | — | public |
| 284 | `Religious_OnHolySiteChange` | context | public |
| 735 | `Religious_OnLocalPlayerChanged` | context | public |
| 746 | `Religious_SitesOwnedByPlayer` | player | public |
| 765 | `Religious_AllSitesControlled` | — | public |
| 768 | `Religious_SitesOwnedByAllies` | player | local |
| 820 | `Religious_AddObjective` | — | public |
| 875 | `Religious_UpdateObjectiveState` | — | public |
| 878 | `Religious_ToggleCountdownObjective` | enable, is_friendly | local |
| 1106 | `Religious_UpdateObjectiveCounter` | — | public |
| 1141 | `Religious_DelayedNewObjective` | context, data | public |
| 1151 | `Religious_RemoveObjectives` | — | public |
| 1161 | `Religious_HolySiteMinimapBlips` | — | public |
| 1187 | `Religious_FlashAllHolySites` | — | public |
| 1231 | `Religious_WinnerPresentation` | playerID | public |
| 1263 | `Religious_LoserPresentation` | playerID | public |
| 1294 | `Religious_StopMusic` | — | public |

### cba.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 85 | `Debug_LeaverConversion_VisualCleanup` | — | public |
| 115 | `Onslaught_GetPlayerScore` | player | public |
| 122 | `Onslaught_SyncScoreToEngine` | — | public |
| 156 | `Onslaught_Trace` | tag, message | local |
| 163 | `Core_OnGameOver` | ... | public |
| 169 | `Onslaught_CrashProbeTick` | — | public |
| 183 | `Onslaught_TryQueueGameOver` | delay, payload | public |
| 196 | `_Onslaught_ResolvePlayerId` | playerLike | local |
| 214 | `_Onslaught_ResolvePlayersEntry` | playerLike | local |
| 228 | `_Onslaught_SetEliminationReason` | playerLike, reason | local |
| 253 | `Surrender_OnPlayerDefeated` | defeatedPlayer, reason | public |
| 263 | `Elimination_OnPlayerDefeated` | player, reason | public |
| 323 | `Mod_OnGameSetup` | — | public |
| 367 | `Mod_PreInit` | — | public |
| 375 | `Mod_OnInit` | — | public |
| 408 | `Mod_PostInit` | — | public |
| 414 | `Mod_Preset` | — | public |
| 422 | `Mod_PreStart` | — | public |
| 428 | `Mod_Start` | — | public |
| 560 | `Mod_OnGameOver` | — | public |
| 636 | `Mod_OnEntityKilled` | context | public |
| 683 | `Mod_RemoveGaia` | — | public |
| 695 | `Mod_setStartingResources` | — | public |
| 721 | `Mod_SetFOW` | — | public |
| 732 | `Mod_SetupObjective` | — | public |
| 773 | `Mod_FindKeep` | — | public |
| 816 | `Mod_ConfigureKeepAsCapitalAgeProducer` | player, keep_ent, ghost_ent, source_tag | public |
| 821 | `_KeepCap_GetSpecialUpgradeList` | player_civ | local |
| 851 | `_KeepCap_ResolveAgeUpAbility` | upg_name | local |
| 899 | `_KeepCap_InjectAgeUpAbilities` | player_obj, player_civ, keep_entity, tag | local |
| 969 | `Mod_EnsureKeepAsCapital` | player, source_tag, opt_force_respawn | public |
| 1059 | `Debug_KeepAsCapitalStatus` | opt_player_id | public |
| 1092 | `Debug_KeepAsCapitalApply` | opt_player_id, opt_force_respawn | public |
| 1107 | `Mod_WinnerPresentation` | playerID | public |
| 1139 | `Mod_LoserPresentation` | playerID | public |
| 1177 | `CBA_Options_SiegeLimit_Disable` | player_id, siege_limit, lock_type | public |
| 1364 | `CBA_Options_SiegeLimit_Cancel_filter` | siege_limit, player | public |
| 1409 | `CBA_Options_SiegeLimit_BuildItemComplete` | context | public |
| 1529 | `CBA_Options_SiegeLimit_SquadKilled` | context | public |
| 1627 | `_Leaver_WarmupPrecache` | — | private |
| 1745 | `_Leaver_IsAlwaysPrecacheBP` | bp_name | private |
| 1752 | `_Leaver_PrecacheSelectedBuildings` | active_player_ids | private |
| 1793 | `_Leaver_GetRequiredAgeForBP` | bp_name | private |
| 1807 | `_Leaver_IsPrecacheRequiredForReceiver` | bp_name, player_id | private |
| 1829 | `_Leaver_RuntimeTrackPrecache` | bp_name, player_id, context, route_label | private |
| 1887 | `_Leaver_BuildPrecacheManifest` | — | private |
| 2125 | `_Leaver_GetMilitarySuffix` | civ | private |
| 2157 | `_Leaver_IsSpawnerExemptBP` | bp_name | private |
| 2172 | `_Leaver_MeetsAgeRequirement` | bp_name, ags_key, player_id, context | private |
| 2259 | `_Leaver_ResolveUpgradeBP` | player_id, upgrade_key | private |
| 2281 | `_Leaver_PlayerHasUpgradeCached` | player_id, upgrade_key | private |
| 2302 | `_Leaver_MeetsCapabilityRequirement` | bp_name, ags_key, player_id, context | private |
| 2496 | `_Leaver_GetUnitRole` | sbp_name | private |
| 2615 | `_Leaver_IsCivUniqueFallbackCandidate` | sbp_name | private |
| 2627 | `_Leaver_GetCivUniquePolicy` | sbp_name | private |
| 2639 | `_Leaver_IsNeutralOrTransferOnlySquad` | squad, sbp_name | private |
| 2652 | `_ResolveReceiverClassFallback` | sbp_name, rcv_civ | private |
| 2734 | `_ResolveGenericArchetypeFallback` | sbp_name, rcv_civ | private |
| 2766 | `_Leaver_GetReverseMapKey` | bp_name | private |
| 2788 | `_ResolveFallbackSquadBP` | sbp_name, rcv_civ | private |
| 2822 | `_ResolveMilitarySquadBP` | sbp_name, src_civ, rcv_civ | private |
| 2860 | `_ResolveMilitaryRoute` | sbp_name, src_civ, rcv_civ | private |
| 2917 | `Mod_FindBestAlly` | victim_id | public |
| 2945 | `_Transfer_CanAcceptBuilding` | recipient | private |
| 2952 | `_Transfer_CanAcceptOutpost` | recipient | private |
| 2958 | `_Transfer_CanAcceptWorkshop` | recipient | private |
| 2966 | `_Transfer_ClassifyBuilding` | eid, owner_civ | private |
| 3013 | `_Transfer_FindLegalRecipient` | victim_id, bld_class | private |
| 3033 | `_Transfer_FindSameFactionAlly` | victim_id, source_faction | private |
| 3048 | `_Transfer_BuildingToPlayer` | eid, recipient | private |
| 3071 | `_Transfer_Resources` | victim_id, recipient | private |
| 3084 | `_Transfer_EjectGarrisons` | victim_id | private |
| 3101 | `_Convert_Building` | eid, recipient, receiver_civ, source_civ, stats, source_player_id | private |
| 3472 | `_Leaver_CountVillagers` | player | private |
| 3481 | `_Convert_EcoSquad` | squad, recipient, receiver_civ | private |
| 3536 | `Mod_EliminatePlayerUnits` | player, recipient_override, is_silent | public |
| 3721 | `_Leaver_ContinueTransfer` | — | private |
| 4256 | `_Leaver_PauseIntervalRules` | — | private |
| 4265 | `_Leaver_ResumeIntervalRules` | — | private |

### day night cycle.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 10 | `Mission_SetupPlayers` | — | public |
| 28 | `Mission_SetupVariables` | — | public |
| 38 | `Mission_SetRestrictions` | — | public |
| 46 | `Mission_Preset` | — | public |
| 53 | `Mission_Start` | — | public |
| 62 | `GetRecipe` | — | public |
| 108 | `statechange` | — | public |
| 117 | `toDay` | — | public |
| 120 | `toDusk` | — | public |
| 123 | `toDusk2` | — | public |
| 126 | `toNight` | — | public |
| 129 | `toNight2` | — | public |
| 132 | `toDawn` | — | public |

### onslaught.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 114 | `Mod_OnGameSetup` | — | public |
| 129 | `Mod_PreInit` | — | public |
| 137 | `Mod_OnInit` | — | public |
| 174 | `Mod_PostInit` | — | public |
| 180 | `Mod_Preset` | — | public |
| 188 | `Mod_PreStart` | — | public |
| 194 | `Mod_Start` | — | public |

### rewards.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 26 | `CBA_Rewards_UpdateModuleSettings` | — | public |
| 32 | `CBA_Rewards_PresetFinalize` | — | public |
| 265 | `CBA_Rewards_Start` | — | public |
| 274 | `CBA_Rewards_SetupObjective` | — | public |
| 318 | `CBA_Rewards_SpawnUnits` | — | public |
| 343 | `CBA_Rewards_StartingUnits` | — | public |
| 353 | `CBA_Rewards_SpawnAndMove` | player,unit,num | public |
| 378 | `CBA_Rewards_nextRequirement` | player | public |
| 391 | `CBA_Rewards_OnEntityKilled` | context | public |
| 515 | `CBA_Rewards_List_Onslaught` | — | public |
| 3629 | `CBA_Rewards_List_Arena` | — | public |

### wonder.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 96 | `Wonder_DiplomacyEnabled` | isEnabled | public |
| 102 | `Wonder_OnInit` | — | public |
| 122 | `Wonder_Start` | — | public |
| 148 | `Wonder_UpdatePlayerStats` | player, scarModel | public |
| 166 | `Wonder_OnPlayerDefeated` | player, reason | public |
| 179 | `Wonder_OnGameOver` | — | public |
| 200 | `Wonder_OnConstructionStart` | context | public |
| 254 | `Wonder_OnConstructionComplete` | context | public |
| 275 | `Wonder_OnEntityKilled` | context | public |
| 449 | `Wonder_OnDamageReceived` | context | public |
| 520 | `Wonder_OnLocalPlayerChanged` | context | public |
| 531 | `Wonder_Update` | — | public |
| 702 | `Wonder_CheckVictory` | — | public |
| 744 | `Wonder_AddObjective1` | player | public |
| 767 | `Wonder_AddObjective2` | ownerID, wonder_entity | public |
| 796 | `Wonder_RemoveObjective2` | player_owner | public |
| 826 | `Wonder_RemoveObjectives` | — | public |
| 838 | `Wonder_CreateEventCue` | context, data | public |
| 856 | `Wonder_WinnerPresentation` | playerID | public |
| 892 | `Wonder_LoserPresentation` | playerID | public |

## specials

### specials/ags_match_ui.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 46 | `AGS_MatchUI_UpdateModuleSettings` | — | public |
| 53 | `AGS_MatchUI_EarlyInitializations` | — | public |
| 58 | `AGS_MatchUI_OnPlay` | — | public |
| 63 | `AGS_MatchUI_OnGameRestore` | — | public |
| 69 | `AGS_MatchUI_OnGameOver` | — | public |
| 74 | `AGS_MatchUI_OnPlayerDefeated` | player, reason | public |
| 85 | `AGS_MatchUI_CreateDataContext` | — | public |
| 94 | `AGS_MatchUI_Update` | — | public |
| 104 | `AGS_MatchUI_Show` | show_ui | public |
| 111 | `AGS_MatchUI_CreateAndUpdateUI` | — | public |
| 116 | `AGS_MatchUI_CreateUI` | — | public |
| 361 | `AGS_MatchUI_ToggleDropdown` | context | public |
| 372 | `AGS_MatchUI_HideDropdown` | context | public |
| 378 | `AGS_MatchUI_ToggleObjectives` | context | public |

### specials/ags_testing.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 18 | `AGS_Testing_UpdateModuleSettings` | — | public |
| 25 | `AGS_Testing_OnPlay` | — | public |
| 35 | `AGS_Testing_RemoveGaia` | — | public |
| 43 | `AGS_Testing_RemoveUnits` | — | public |
| 49 | `AGS_Testing_HasCommandLineOption` | option_name | public |
| 53 | `AGS_Testing_SpawnTest` | — | public |

### specials/ags_utilities.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 66 | `AGS_Utilities_UpdateModuleSettings` | — | public |
| 73 | `AGS_Utilities_AdjustSettings` | — | public |
| 79 | `AGS_Utilities_LateInitializations` | — | public |
| 84 | `AGS_Utilities_OnPlay` | — | public |
| 93 | `Religious_UpdatePlayerStats` | player, scarModel | public |
| 102 | `Conquest_UpdatePlayerStats` | player, scarModel | public |
| 114 | `Wonder_UpdatePlayerStats` | player, scarModel | public |
| 138 | `AGS_Utilities_StandardReplay` | — | public |
| 152 | `AGS_Utilities_StandardReplayCallbacks` | — | public |

## startconditions

### startconditions/ags_start_scattered.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 23 | `AGS_Scattered_AdjustSettings` | — | public |
| 30 | `AGS_Scattered_UpdateModuleSettings` | — | public |
| 37 | `AGS_Scattered_EarlyInitializations` | — | public |
| 44 | `AGS_Scattered_PresetInitialize` | — | public |
| 51 | `AGS_Scattered_PresetExecute` | — | public |
| 56 | `AGS_Scattered_OnStarting` | — | public |
| 82 | `AGS_Scattered_DestroySpawn` | — | public |
| 90 | `AGS_Scattered_GetScatterPosition` | — | public |
| 97 | `AGS_Scattered_CreateSpawn` | — | public |

### startconditions/nomad_start.scar

| Line | Function | Params | Visibility |
|------|----------|--------|------------|
| 19 | `Nomad_OnGameSetup` | — | public |
| 40 | `Nomad_UpdateModuleSettings` | — | public |
| 45 | `Nomad_PresetFinalize` | — | public |
| 61 | `Nomad_Start` | — | public |
| 72 | `Nomad_UnlockVillagers` | — | public |
| 79 | `Nomad_OnConstructionComplete` | context | public |
| 113 | `Nomad_DestroySpawns` | — | public |
| 130 | `Nomad_SetupSpawns` | — | public |
| 182 | `Nomad_intMax` | x, y | public |

