# Onslaught SCAR API Usage Map

Auto-generated on 2026-04-02 05:31. Cross-reference of official SCAR engine API functions used in Onslaught.

- **862** unique API functions called
- **5850** total call sites across 144 files
- **106** files contain API calls

## Namespace Summary

| Namespace | Unique Functions | Total Calls |
|-----------|-----------------|-------------|
| `AGS` | 372 | 1073 |
| `Loc` | 3 | 853 |
| `Player` | 41 | 616 |
| `Entity` | 38 | 526 |
| `BP` | 13 | 484 |
| `Debug` | 241 | 473 |
| `Rule` | 11 | 302 |
| `World` | 19 | 234 |
| `Core` | 10 | 225 |
| `Squad` | 10 | 212 |
| `UI` | 19 | 184 |
| `EGroup` | 14 | 155 |
| `Obj` | 16 | 149 |
| `SGroup` | 10 | 126 |
| `Timer` | 7 | 58 |
| `Modifier` | 2 | 37 |
| `Game` | 3 | 35 |
| `Music` | 4 | 20 |
| `Sound` | 1 | 15 |
| `Misc` | 5 | 15 |
| `FOW` | 6 | 13 |
| `Util` | 5 | 12 |
| `Objective` | 3 | 7 |
| `Taskbar` | 1 | 6 |
| `Setup` | 1 | 5 |
| `EBP` | 1 | 4 |
| `SBP` | 1 | 4 |
| `HintPoint` | 2 | 3 |
| `AI` | 1 | 2 |
| `Camera` | 1 | 1 |
| `Table` | 1 | 1 |

## Top 50 Most-Called API Functions

| # | Function | Calls | Files | Example Location |
|---|----------|-------|-------|-----------------|
| 1 | `Loc_FormatText` | 769 | 10 | cba_annihilation.scar:235 |
| 2 | `BP_GetSquadBlueprint` | 354 | 10 | debug/cba_debug_ai_behavior.scar:106 |
| 3 | `Entity_IsOfType` | 210 | 18 | cba_annihilation.scar:114 |
| 4 | `AGS_Print` | 148 | 30 | ags_global_settings.scar:234 |
| 5 | `Squad_IsOfType` | 135 | 6 | cba_religious.scar:480 |
| 6 | `Player_GetRaceName` | 122 | 19 | cba.scar:946 |
| 7 | `Rule_AddOneShot` | 117 | 22 | cba_religious.scar:211 |
| 8 | `Player_SetEntityProductionAvailability` | 88 | 9 | cba.scar:997 |
| 9 | `World_GetGameTime` | 87 | 13 | debug/cba_debug_helpers.scar:1073 |
| 10 | `Entity_IsEBPOfType` | 85 | 3 | gameplay/cba_auto_age.scar:288 |
| 11 | `Loc_Empty` | 75 | 20 | cba_annihilation.scar:43 |
| 12 | `World_Pos` | 61 | 17 | cba.scar:1995 |
| 13 | `Core_GetPlayersTableEntry` | 55 | 18 | ags_global_settings.scar:319 |
| 14 | `Rule_AddGlobalEvent` | 53 | 19 | ags_global_settings.scar:304 |
| 15 | `Squad_IsSBPOfType` | 52 | 3 | cba.scar:1383 |
| 16 | `Player_ObserveRelationship` | 48 | 8 | cba_annihilation.scar:246 |
| 17 | `Player_GetEntities` | 46 | 14 | cba_annihilation.scar:173 |
| 18 | `UI_CreateEventCueClickable` | 44 | 8 | cba_religious.scar:315 |
| 19 | `Player_SetResource` | 43 | 7 | cba.scar:701 |
| 20 | `Core_RegisterModule` | 43 | 39 | ags_global_settings.scar:231 |
| 21 | `AGS_GetCivilizationEntity` | 42 | 10 | cba.scar:991 |
| 22 | `UI_SetPropertyValue` | 41 | 3 | observerui/observerui.scar:123 |
| 23 | `Core_IsPlayerEliminated` | 38 | 9 | cba_annihilation.scar:299 |
| 24 | `BP_GetName` | 37 | 3 | cba.scar:998 |
| 25 | `SGroup_Count` | 34 | 8 | cba_religious.scar:476 |
| 26 | `AGS_SetEntityProductionAvailabilitySafe` | 34 | 7 | cba.scar:1230 |
| 27 | `Core_CallDelegateFunctions` | 32 | 6 | cba.scar:353 |
| 28 | `Rule_RemoveGlobalEvent` | 32 | 11 | ags_global_settings.scar:309 |
| 29 | `Core_UnregisterModule` | 32 | 27 | cba_religious.scar:149 |
| 30 | `Rule_AddInterval` | 32 | 20 | cba_religious.scar:170 |
| 31 | `Entity_HasBlueprint` | 31 | 3 | cba.scar:2997 |
| 32 | `Debug_AskYesNo` | 30 | 4 | debug/cba_debug_ai_behavior.scar:121 |
| 33 | `BP_GetUpgradeBlueprint` | 29 | 4 | gameplay/cba_options.scar:900 |
| 34 | `Game_GetLocalPlayer` | 28 | 16 | ags_global_settings.scar:303 |
| 35 | `Entity_GetID` | 26 | 5 | cba_religious.scar:133 |
| 36 | `Player_SetUpgradeAvailability` | 26 | 3 | gameplay/cba_options.scar:900 |
| 37 | `EGroup_Destroy` | 24 | 9 | cba_annihilation.scar:220 |
| 38 | `Player_GetSquads` | 24 | 10 | cba.scar:3473 |
| 39 | `AGS_GetSiegeUnit` | 24 | 5 | cba.scar:1207 |
| 40 | `Obj_SetProgress` | 23 | 6 | cba_religious.scar:248 |
| 41 | `EGroup_Count` | 23 | 6 | cba.scar:1367 |
| 42 | `Rule_Exists` | 23 | 6 | debug/cba_debug_playerui_anim.scar:2021 |
| 43 | `Player_GetCurrentAge` | 23 | 12 | cba.scar:1819 |
| 44 | `AGS_LimitsUI_HexToByte` | 22 | 1 | gameplay/ags_limits_ui.scar:331 |
| 45 | `Timer_Exists` | 22 | 4 | cba_religious.scar:415 |
| 46 | `EGroup_CountSpawned` | 22 | 10 | cba_annihilation.scar:176 |
| 47 | `Entity_GetBuildingProgress` | 21 | 10 | cba_annihilation.scar:180 |
| 48 | `Player_GetResource` | 21 | 6 | cba_annihilation.scar:164 |
| 49 | `BP_GetEntityBlueprintsWithType` | 21 | 6 | gameplay/ags_game_rates.scar:29 |
| 50 | `SGroup_GetSquadAt` | 21 | 7 | cba_religious.scar:479 |

## Per-Namespace Detail

### AGS (372 functions, 1073 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `AGS_Print` | 148 | 30 |
| `AGS_GetCivilizationEntity` | 42 | 10 |
| `AGS_SetEntityProductionAvailabilitySafe` | 34 | 7 |
| `AGS_GetSiegeUnit` | 24 | 5 |
| `AGS_LimitsUI_HexToByte` | 22 | 1 |
| `AGS_IsSBPOfTypeSafe` | 21 | 3 |
| `AGS_SetSquadProductionAvailabilitySafe` | 19 | 4 |
| `AGS_CivTableHasExplicitFalse` | 16 | 4 |
| `AGS_Objectives_Set` | 16 | 4 |
| `AGS_LimitsUI_ClampByte` | 15 | 1 |
| `AGS_GetSiegeEntity` | 13 | 4 |
| `AGS_Handicaps_ApplyModifier` | 12 | 1 |
| `AGS_WarnNilBlueprint` | 10 | 2 |
| `AGS_LimitsUI_DeferUpdate` | 9 | 2 |
| `AGS_GlobalSettings_RetrieveSlotHandicap` | 9 | 1 |
| `AGS_Handicaps_ToRaw` | 9 | 1 |
| `AGS_GlobalSettings_DefineGameConditions` | 8 | 1 |
| `AGS_GetCivilizationUnit` | 8 | 6 |
| `AGS_LimitsUI_Lerp` | 8 | 1 |
| `AGS_LimitsUI_Update` | 7 | 2 |
| `AGS_GetCivilizationUpgrade` | 7 | 5 |
| `AGS_Objectives_Create` | 7 | 4 |
| `AGS_IsMutualRelation` | 7 | 3 |
| `AGS_SpecialPopulationUI_Update` | 6 | 1 |
| `AGS_PopulationAutomatic_ReconcileCapDrift` | 6 | 4 |
| `AGS_LimitsUI_Clamp01` | 6 | 1 |
| `AGS_ApplyUpgrade` | 5 | 2 |
| `AGS_GatherRates_ApplyModifier` | 5 | 1 |
| `AGS_Objectives_PresentWrap` | 5 | 2 |
| `AGS_Wonder_EnableConstruction` | 4 | 1 |
| `AGS_LimitsUI_ShouldTraceUpdateFlow` | 4 | 1 |
| `AGS_IsAWonder` | 4 | 2 |
| `AGS_Annihilation_CheckAnnihilation` | 4 | 1 |
| `AGS_Handicaps_AddModifier` | 4 | 1 |
| `AGS_GetRelation` | 4 | 2 |
| `AGS_SetPlayerDefeated` | 4 | 4 |
| `AGS_Teams_CountAlivePlayers` | 4 | 1 |
| `AGS_IsACapital` | 4 | 2 |
| `AGS_Teams_CountAliveInGroup` | 4 | 1 |
| `AGS_Notifications_Eliminated` | 4 | 4 |
| `AGS_Wonder_RemoveBuildObjective` | 4 | 1 |
| `AGS_Conditions_CheckVictory` | 4 | 4 |
| `AGS_GameRates_ApplyBonus` | 3 | 1 |
| `AGS_CompleteUpgradeSafe` | 3 | 3 |
| `AGS_PopulationAutomatic_ApplyStartCaps` | 3 | 1 |
| `AGS_LimitsUI_CreateUI` | 3 | 1 |
| `AGS_SpecialPopulationUI_Show` | 3 | 1 |
| `AGS_Scattered_GetScatterPosition` | 3 | 2 |
| `AGS_TeamBalance_UpdateTeam` | 3 | 2 |
| `AGS_MatchUI_Show` | 3 | 1 |
| `AGS_MatchUI_CreateAndUpdateUI` | 3 | 1 |
| `AGS_SGroupName` | 3 | 3 |
| `AGS_Teams_GetStaticTeamAliveMembers` | 3 | 2 |
| `AGS_TreeBombardment_DestroyTreeGroup` | 3 | 1 |
| `AGS_AutoPop_BuildForbiddenBPSet` | 3 | 2 |
| `AGS_LimitsUI_Show` | 3 | 1 |
| `AGS_Wonder_Construction` | 3 | 1 |
| `AGS_LimitsUI_AnimProgress` | 3 | 1 |
| `AGS_Wonder_UpdateWonderTimer` | 3 | 1 |
| `AGS_Wonder_CreateBuildObjective` | 3 | 1 |
| `AGS_GatherRates_ApplyBonus` | 3 | 1 |
| `AGS_AutoPop_ScheduleDeferredReconcile` | 3 | 1 |
| `AGS_Wonder_CleanWonder` | 3 | 1 |
| `AGS_Objectives_Present` | 3 | 1 |
| `AGS_UnitRates_ApplyBonus` | 3 | 1 |
| `AGS_Wonder_TryDeclareWinners` | 3 | 1 |
| `AGS_GlobalSettings_SetMaximumMedicPopulation` | 3 | 1 |
| `AGS_LimitsUI_CreateAndUpdateUI` | 3 | 1 |
| `AGS_Objectives_CreateFromCore` | 3 | 1 |
| `AGS_SpecialPopulationUI_CreateAndUpdateUI` | 3 | 1 |
| `AGS_DockHouse_IsDock` | 3 | 1 |
| `AGS_Handicaps_ApplyMilitaryBonus` | 3 | 1 |
| `AGS_MatchUI_CreateDataContext` | 2 | 1 |
| `AGS_SpecialPopulationUI_CreateDataContext` | 2 | 1 |
| `AGS_GlobalSettings_SetMapVision` | 2 | 1 |
| `AGS_Teams_AreTeamVictoryEligible` | 2 | 1 |
| `AGS_MedicPopulationCapacity_ApplyMinMedicPopulation` | 2 | 1 |
| `AGS_LimitsUI_BlendARGB` | 2 | 1 |
| `AGS_GlobalSettings_DefineGameSettings` | 2 | 1 |
| `AGS_Teams_CreateStaticTeams` | 2 | 1 |
| `AGS_Wonder_TimerProgressNotification` | 2 | 1 |
| `AGS_LimitsUI_BoostARGB` | 2 | 1 |
| `AGS_LimitsUI_BoostRGB` | 2 | 1 |
| `AGS_PopulationCapacity_ApplyMaxCapPopulation` | 2 | 1 |
| `AGS_Teams_GetStaticTeamWinnders` | 2 | 1 |
| `AGS_GlobalSettings_DefineMatchSettings` | 2 | 1 |
| `AGS_LimitsUI_GetColors` | 2 | 1 |
| `AGS_GlobalSettings_SetUnitRates` | 2 | 1 |
| `AGS_Scattered_CreateSpawn` | 2 | 1 |
| `AGS_Wonder_ResetTimerObjective` | 2 | 1 |
| `AGS_TreeBombardment_OnExpectedLanding` | 2 | 1 |
| `AGS_Utilities_StandardReplay` | 2 | 1 |
| `AGS_Utilities_StandardReplayCallbacks` | 2 | 1 |
| `AGS_Annihilation_CreateObjective` | 2 | 1 |
| `AGS_Handicaps_CreateListFrom` | 2 | 1 |
| `AGS_Wonder_UpdateTimerObjectives` | 2 | 1 |
| `AGS_PopulationAutomatic_NormalizeStartCap` | 2 | 1 |
| `AGS_GlobalSettings_SetTreaty` | 2 | 1 |
| `AGS_MedicPopulationCapacity_SetMinMedicPopulation` | 2 | 1 |
| `AGS_LimitsUI_BlendRGB` | 2 | 1 |
| `AGS_GlobalSettings_SetSettlement` | 2 | 1 |
| `AGS_GlobalSettings_SetMaintainTeamBalance` | 2 | 1 |
| `AGS_Annihilation_IsAbleToProduce` | 2 | 1 |
| `AGS_GlobalSettings_SetMaximumPopulation` | 2 | 1 |
| `AGS_LimitsUI_LogRecreate` | 2 | 1 |
| `AGS_StartingAge_UpgradePlayer` | 2 | 1 |
| `AGS_Wonder_InitializeWonders` | 2 | 1 |
| `AGS_GlobalSettings_SetReligiousTimer` | 2 | 1 |
| `AGS_Contains` | 2 | 1 |
| `AGS_RevealFowOnElimination_Reveal` | 2 | 1 |
| `AGS_SpawnSquad` | 2 | 2 |
| `AGS_LimitsUI_RecreateUI` | 2 | 1 |
| `AGS_Wonder_RemoveAllObjectives` | 2 | 1 |
| `AGS_UnitRates_ApplyModifier` | 2 | 1 |
| `AGS_GlobalSettings_DefineHandicapSettings` | 2 | 1 |
| `AGS_Teams_CountAliveAllies` | 2 | 1 |
| `AGS_GlobalSettings_SetScoreTimer` | 2 | 1 |
| `AGS_NoDock_Lock` | 2 | 1 |
| `AGS_GlobalSettings_SetHandicapType` | 2 | 1 |
| `AGS_Surrender_CheckAI` | 2 | 1 |
| `AGS_Teams_CreateInitialTeams` | 2 | 1 |
| `AGS_GlobalSettings_DefineWinSettings` | 2 | 1 |
| `AGS_GlobalSettings_SetWonderScaleCost` | 2 | 1 |
| `AGS_GlobalSettings_SetSlotHandicaps` | 2 | 1 |
| `AGS_GlobalSettings_DefineRestrictionSettings` | 2 | 1 |
| `AGS_StartingAge_UpgradeAllPlayers` | 2 | 1 |
| `AGS_Wonder_DeactivateTimers` | 2 | 1 |
| `AGS_GlobalSettings_SetTreatyTimer` | 2 | 1 |
| `AGS_TeamBalance_UpdateTeamResources` | 2 | 1 |
| `AGS_Wonder_StartCountdown` | 2 | 1 |
| `AGS_GlobalSettings_SetStartingKeeps` | 2 | 1 |
| `AGS_GlobalSettings_SetWonderTimer` | 2 | 1 |
| `AGS_IsATownCenter` | 2 | 2 |
| `AGS_Annihilation_PlayerCanReceiveTribute` | 2 | 1 |
| `AGS_Wonder_CreateTimerNotifications` | 2 | 1 |
| `AGS_TeamBalance_IncreaseMaxCapPopulation` | 2 | 1 |
| `AGS_GlobalSettings_SetSimulationSpeed` | 2 | 1 |
| `AGS_GlobalSettings_SetTechnologyAge` | 2 | 1 |
| `AGS_GlobalSettings_SetAutoAge` | 2 | 1 |
| `AGS_Annihilation_DefineCheapestSquads` | 2 | 1 |
| `AGS_MedicPopulationCapacity_ApplyMaxCapMedicPopulation` | 2 | 1 |
| `AGS_Annihilation_AreOnlyValidSquads` | 2 | 1 |
| `AGS_Annihilation_Eliminate` | 2 | 1 |
| `AGS_Handicaps_ApplyPerPlayer` | 2 | 1 |
| `AGS_Teams_GetSoloTeamWinner` | 2 | 1 |
| `AGS_Wonder_WarnEveryone` | 2 | 1 |
| `AGS_GlobalSettings_CBA_Rewards` | 2 | 1 |
| `AGS_GlobalSettings_SetTownCenterRestricts` | 2 | 1 |
| `AGS_GameRates_ApplyModifier` | 2 | 1 |
| `AGS_Wonder_Destroyed` | 2 | 1 |
| `AGS_Teams_GetAllCurrentOpponents` | 2 | 2 |
| `AGS_PopulationCapacity_Change` | 2 | 1 |
| `AGS_MatchUI_CreateUI` | 2 | 1 |
| `AGS_GlobalSettings_DefineLegacySettings` | 2 | 1 |
| `AGS_Wonder_InformNegativeProgressChange` | 2 | 1 |
| `AGS_GlobalSettings_SetTeamVictory` | 2 | 1 |
| `AGS_GlobalSettings_DefineWinConditions` | 2 | 1 |
| `AGS_MatchUI_ToggleDropdown` | 2 | 1 |
| `AGS_TeamBalance_UpdateAutoRates` | 2 | 1 |
| `AGS_Wonder_CreateTimerObjective` | 2 | 1 |
| `AGS_PopulationCapacity_ApplyMinPopulation` | 2 | 1 |
| `AGS_GlobalSettings_SetGameRates` | 2 | 1 |
| `AGS_LimitsUI_BuildSnapshot` | 2 | 1 |
| `AGS_DockHouse_AddMinPopulation` | 2 | 1 |
| `AGS_Wonder_TimerUpdate` | 2 | 1 |
| `AGS_GlobalSettings_SetGatherRates` | 2 | 1 |
| `AGS_GlobalSettings_SetEndingAge` | 2 | 1 |
| `AGS_Teams_GetDynamicTeamWinners` | 2 | 1 |
| `AGS_IsThisSpecialMobileBuildingDead` | 2 | 2 |
| `AGS_Wonder_FailTimerObjective` | 2 | 1 |
| `AGS_GlobalSettings_SetMinimumPopulation` | 2 | 1 |
| `AGS_GlobalSettings_DefineCbaSettings` | 2 | 1 |
| `AGS_AutoPopulationStart` | 2 | 1 |
| `AGS_DockHouse_RemoveMinPopulation` | 2 | 1 |
| `AGS_NoWall_Lock` | 2 | 1 |
| `AGS_Teams_CreateFFA` | 2 | 1 |
| `AGS_Wonder_RemoveTimerObjectives` | 2 | 1 |
| `AGS_GlobalSettings_SetTeamVision` | 2 | 1 |
| `AGS_Scattered_DestroySpawn` | 2 | 1 |
| `AGS_PopulationCapacity_SetMinPopulation` | 2 | 1 |
| `AGS_SpecialPopulationUI_CreateUI` | 2 | 1 |
| `AGS_GlobalSettings_SetStartingVillagers` | 2 | 1 |
| `AGS_Toggle_EconBuildings` | 2 | 1 |
| `AGS_Annihilation_RemoveObjective` | 2 | 1 |
| `AGS_TeamBalance_IncreaseCapPopulation` | 2 | 1 |
| `AGS_Wonder_VictoryTriggered` | 2 | 1 |
| `AGS_Handicaps_ApplyWorkerBonus` | 2 | 1 |
| `AGS_GlobalSettings_OnLocalPlayerChanged` | 2 | 1 |
| `AGS_GlobalSettings_SetStartingResources` | 2 | 1 |
| `AGS_GlobalSettings_SetPopulationinterval` | 2 | 1 |
| `AGS_NoSiege_Lock` | 2 | 1 |
| `AGS_SpecialPopulationUI_MarginError` | 2 | 1 |
| `AGS_Teams_IsTeamVictoryEligible` | 2 | 2 |
| `AGS_NoArsenal_Lock` | 2 | 1 |
| `AGS_GlobalSettings_DefinePlayerSettings` | 2 | 1 |
| `AGS_GlobalSettings_SetStartingAge` | 2 | 1 |
| `AGS_TeamBalance_UpdateTeamPopulation` | 2 | 1 |
| `AGS_GlobalSettings_SetStartingKings` | 2 | 1 |
| `AGS_TeamBalance_UpdateAllLimits` | 2 | 1 |
| `AGS_DockHouse_OnEntityKilled` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnBuildItemComplete` | 1 | 1 |
| `AGS_MatchUI_OnGameOver` | 1 | 1 |
| `AGS_PopulationCapacity_UpdateModuleSettings` | 1 | 1 |
| `AGS_MatchUI_ToggleObjectives` | 1 | 1 |
| `AGS_DockHouse_AddMaxCapPopulation` | 1 | 1 |
| `AGS_Conditions_IsAnyHumanAlive` | 1 | 1 |
| `AGS_TreeBombardment_UpdateModuleSettings` | 1 | 1 |
| `AGS_AutoResources_PresetFinalize` | 1 | 1 |
| `AGS_Surrender_RemoveObjective` | 1 | 1 |
| `AGS_Utilities_AdjustSettings` | 1 | 1 |
| `AGS_Testing_SpawnTest` | 1 | 1 |
| `AGS_TeamBalance_UpdateTeamMedicPopulation` | 1 | 1 |
| `AGS_TeamBalance_OnPlayerDefeated` | 1 | 1 |
| `AGS_Notifications_Destroyed` | 1 | 1 |
| `AGS_GetNeutralUnit` | 1 | 1 |
| `AGS_MedicPopulationCapacity_PresetFinalize` | 1 | 1 |
| `AGS_TeamBalance_UpdateModuleSettings` | 1 | 1 |
| `AGS_UnitRates_PresetFinalize` | 1 | 1 |
| `AGS_LimitsUI_OnGameRestore` | 1 | 1 |
| `AGS_GlobalSettings_EarlyInitializations` | 1 | 1 |
| `AGS_MatchUI_OnGameRestore` | 1 | 1 |
| `AGS_Testing_RemoveUnits` | 1 | 1 |
| `AGS_Annihilation_OnConstructionComplete` | 1 | 1 |
| `AGS_IncreasePopulation` | 1 | 1 |
| `AGS_EGroupName` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnGameOver` | 1 | 1 |
| `AGS_Starts_GetStartPosition` | 1 | 1 |
| `AGS_Wonder_OnPlay` | 1 | 1 |
| `AGS_LimitsUI_OnEntityKilled` | 1 | 1 |
| `AGS_Wonder_TreatyStarted` | 1 | 1 |
| `AGS_GatherRates_PresetFinalize` | 1 | 1 |
| `AGS_SpecialPopulationUI_UpdateModuleSettings` | 1 | 1 |
| `AGS_Annihilation_OnLandmarkDestroyed` | 1 | 1 |
| `AGS_Teams_DoesWinnerGroupExists` | 1 | 1 |
| `AGS_Elimination_CreateObjective` | 1 | 1 |
| `AGS_Wonder_OnEntityKilled` | 1 | 1 |
| `AGS_PopulationCapacity_AdjustSettings` | 1 | 1 |
| `AGS_MatchUI_HideDropdown` | 1 | 1 |
| `AGS_DockHouse_OnPlay` | 1 | 1 |
| `AGS_SpawnEntity` | 1 | 1 |
| `AGS_PopulationAutomatic_CompensateInnate` | 1 | 1 |
| `AGS_StartingAge_LateInitializations` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnPlay` | 1 | 1 |
| `AGS_UnitRates_UpdateModuleSettings` | 1 | 1 |
| `AGS_Utilities_OnPlay` | 1 | 1 |
| `AGS_StartingAge_UpdateModuleSettings` | 1 | 1 |
| `AGS_MedicPopulationCapacity_Change` | 1 | 1 |
| `AGS_Teams_GetAllCurrentTeammates` | 1 | 1 |
| `AGS_Wonder_TreatyEnded` | 1 | 1 |
| `AGS_LimitsUI_AnimTick` | 1 | 1 |
| `AGS_Wonder_UpdateModuleSettings` | 1 | 1 |
| `AGS_Scattered_EarlyInitializations` | 1 | 1 |
| `AGS_Wonder_OnConstructionComplete` | 1 | 1 |
| `AGS_Scattered_UpdateModuleSettings` | 1 | 1 |
| `AGS_NoSiege_UpdateModuleSettings` | 1 | 1 |
| `AGS_SpecialPopulationUI_EarlyInitializations` | 1 | 1 |
| `AGS_MatchUI_UpdateModuleSettings` | 1 | 1 |
| `AGS_DockHouse_RemoveMaxCapPopulation` | 1 | 1 |
| `AGS_GlobalSettings_SetMaximumSiegeWorkshop` | 1 | 1 |
| `AGS_Wonder_OnRelationshipChanged` | 1 | 1 |
| `AGS_Pilgrims_GetScatterPosition` | 1 | 1 |
| `AGS_Objectives_Progress` | 1 | 1 |
| `AGS_AutoPop_RunDeferredReconcile` | 1 | 1 |
| `AGS_Wonder_OnObjectiveToggle` | 1 | 1 |
| `AGS_Surrender_Notify` | 1 | 1 |
| `AGS_Teams_EarlyInitializations` | 1 | 1 |
| `AGS_Annihilation_UpdateModuleSettings` | 1 | 1 |
| `AGS_DockHouse_UpdateModuleSettings` | 1 | 1 |
| `AGS_PopulationAutomatic_PresetFinalize` | 1 | 1 |
| `AGS_Annihilation_OnGameOver` | 1 | 1 |
| `AGS_GatherRates_UpdateModuleSettings` | 1 | 1 |
| `AGS_LimitsUI_ApplyMargin` | 1 | 1 |
| `AGS_Utilities_UpdateModuleSettings` | 1 | 1 |
| `AGS_Annihilation_OnEntityKilled` | 1 | 1 |
| `AGS_GetNeutralEntity` | 1 | 1 |
| `AGS_Elimination_OnPlayerAITakeover` | 1 | 1 |
| `AGS_AutoPop_OnConstructionComplete` | 1 | 1 |
| `AGS_AutoPop_OnEntityKilled` | 1 | 1 |
| `AGS_Annihilation_PresetFinalize` | 1 | 1 |
| `AGS_Religious_CountSitesControlled` | 1 | 1 |
| `AGS_Notifications_CountdownNotification` | 1 | 1 |
| `AGS_Annihilation_TreatyStarted` | 1 | 1 |
| `AGS_GameRates_UpdateModuleSettings` | 1 | 1 |
| `AGS_Annihilation_OnPlayerDefeated` | 1 | 1 |
| `AGS_NoDock_UpdateModuleSettings` | 1 | 1 |
| `AGS_Wonder_OnTimerTick` | 1 | 1 |
| `AGS_Utilities_LateInitializations` | 1 | 1 |
| `AGS_CountItems` | 1 | 1 |
| `AGS_Conquest_GetPlayerConquerableCount` | 1 | 1 |
| `AGS_Testing_UpdateModuleSettings` | 1 | 1 |
| `AGS_RevealFowOnElimination_UpdateModuleSettings` | 1 | 1 |
| `AGS_Scattered_OnStarting` | 1 | 1 |
| `AGS_MatchUI_OnPlayerDefeated` | 1 | 1 |
| `AGS_MatchUI_Update` | 1 | 1 |
| `AGS_Notifications_ObjectiveAction` | 1 | 1 |
| `AGS_Testing_RemoveGaia` | 1 | 1 |
| `AGS_Wonder_ConstructionStarted` | 1 | 1 |
| `AGS_TreeBombardment_PrepareStart` | 1 | 1 |
| `AGS_PopulationAutomatic_UpdateModuleSettings` | 1 | 1 |
| `AGS_GlobalSettings_OnGameOver` | 1 | 1 |
| `AGS_LimitsUI_UpdateModuleSettings` | 1 | 1 |
| `AGS_Testing_OnPlay` | 1 | 1 |
| `AGS_Elimination_UpdateModuleSettings` | 1 | 1 |
| `AGS_IsLocalGame` | 1 | 1 |
| `AGS_NoWall_UpdateModuleSettings` | 1 | 1 |
| `AGS_Surrender_UpdateModuleSettings` | 1 | 1 |
| `AGS_Testing_HasCommandLineOption` | 1 | 1 |
| `AGS_GlobalSettings_SetMaximumProductionBuildings` | 1 | 1 |
| `AGS_AutoResources_UpdateModuleSettings` | 1 | 1 |
| `AGS_LimitsUI_OnPlay` | 1 | 1 |
| `AGS_PopulationCapacity_PresetFinalize` | 1 | 1 |
| `AGS_Annihilation_OnObjectiveToggle` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnSquadKilled` | 1 | 1 |
| `AGS_Elimination_RemoveObjective` | 1 | 1 |
| `AGS_Teams_IsTeamAlive` | 1 | 1 |
| `AGS_LimitsUI_OnBuildItemComplete` | 1 | 1 |
| `AGS_GlobalSettings_SetupSettings` | 1 | 1 |
| `AGS_MatchUI_EarlyInitializations` | 1 | 1 |
| `AGS_Annihilation_TreatyEnded` | 1 | 1 |
| `AGS_NoSiege_PresetFinalize` | 1 | 1 |
| `AGS_Elimination_OnPlayerDefeated` | 1 | 1 |
| `AGS_LimitsUI_OnSquadKilled` | 1 | 1 |
| `AGS_NoArsenal_PresetFinalize` | 1 | 1 |
| `AGS_TreeBombardment_OnProjectileFired` | 1 | 1 |
| `AGS_MatchUI_OnPlay` | 1 | 1 |
| `AGS_TreeBombardment_OnProjectileLanded` | 1 | 1 |
| `AGS_LimitsUI_OnPlayerDefeated` | 1 | 1 |
| `AGS_Wonder_OnGameOver` | 1 | 1 |
| `AGS_DockHouse_OnConstructionComplete` | 1 | 1 |
| `AGS_CalculateCenterOffset` | 1 | 1 |
| `AGS_AutoResources` | 1 | 1 |
| `AGS_SetPlayerGroupDefeated` | 1 | 1 |
| `AGS_DockHouse_GameOver` | 1 | 1 |
| `AGS_EGroupNeutralName` | 1 | 1 |
| `AGS_LimitsUI_EarlyInitializations` | 1 | 1 |
| `AGS_Surrender_OnPlayerDefeated` | 1 | 1 |
| `AGS_Annihilation_OnPlay` | 1 | 1 |
| `AGS_GameRates_PresetFinalize` | 1 | 1 |
| `AGS_Surrender_OnPlay` | 1 | 1 |
| `AGS_NoWall_PresetFinalize` | 1 | 1 |
| `AGS_LimitsUI_OnConstructionComplete` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnEntityKilled` | 1 | 1 |
| `AGS_Wonder_OnDamageReceived` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnGameRestore` | 1 | 1 |
| `AGS_GetFreeItems` | 1 | 1 |
| `AGS_LimitsUI_OnGameOver` | 1 | 1 |
| `AGS_IsALandmark` | 1 | 1 |
| `AGS_MedicPopulationCapacity_UpdateModuleSettings` | 1 | 1 |
| `AGS_Scattered_PresetExecute` | 1 | 1 |
| `AGS_EndGame` | 1 | 1 |
| `AGS_Wonder_OnPlayerDefeated` | 1 | 1 |
| `AGS_RevealFowOnElimination_OnPlayerDefeated` | 1 | 1 |
| `AGS_Surrender_OnSurrenderMatchRequested` | 1 | 1 |
| `AGS_RemoveUpgrade` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnConstructionComplete` | 1 | 1 |
| `AGS_Wonder_ConstructionCompleted` | 1 | 1 |
| `AGS_NoArsenal_UpdateModuleSettings` | 1 | 1 |
| `AGS_SpecialPopulationUI_OnPlayerDefeated` | 1 | 1 |
| `AGS_Notifications_Damaged` | 1 | 1 |
| `AGS_TreeBombardment_OnGameOver` | 1 | 1 |
| `AGS_Handicaps_PresetFinalize` | 1 | 1 |
| `AGS_Teams_OnPlayerDefeated` | 1 | 1 |
| `AGS_Scattered_AdjustSettings` | 1 | 1 |
| `AGS_Objectives_SetTitle` | 1 | 1 |
| `AGS_PopulationAutomatic_EarlyInitializations` | 1 | 1 |
| `AGS_Wonder_OnConstructionStart` | 1 | 1 |
| `AGS_IsAKeep` | 1 | 1 |
| `AGS_NoDock_PresetFinalize` | 1 | 1 |
| `AGS_Handicaps_UpdateModuleSettings` | 1 | 1 |
| `AGS_Scattered_PresetInitialize` | 1 | 1 |
| `AGS_Annihilation_OnDamageReceived` | 1 | 1 |
| `AGS_Teams_GetAllMutualFriendshipPlayers` | 1 | 1 |

### Loc (3 functions, 853 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Loc_FormatText` | 769 | 10 |
| `Loc_Empty` | 75 | 20 |
| `Loc_GetString` | 9 | 4 |

### Player (41 functions, 616 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Player_GetRaceName` | 122 | 19 |
| `Player_SetEntityProductionAvailability` | 88 | 9 |
| `Player_ObserveRelationship` | 48 | 8 |
| `Player_GetEntities` | 46 | 14 |
| `Player_SetResource` | 43 | 7 |
| `Player_SetUpgradeAvailability` | 26 | 3 |
| `Player_GetSquads` | 24 | 10 |
| `Player_GetCurrentAge` | 23 | 12 |
| `Player_GetResource` | 21 | 6 |
| `Player_GetUIColour` | 20 | 7 |
| `Player_GetRace` | 19 | 8 |
| `Player_GetCurrentPopulationCap` | 12 | 9 |
| `Player_SetSquadProductionAvailability` | 12 | 4 |
| `Player_GetCurrentPopulation` | 11 | 7 |
| `Player_GetStartingPosition` | 10 | 3 |
| `Player_SetCurrentAge` | 10 | 3 |
| `Player_SetStateModelFloat` | 9 | 5 |
| `Player_AddResource` | 7 | 4 |
| `Player_GiftResource` | 7 | 3 |
| `Player_SetMaximumAge` | 6 | 1 |
| `Player_GetTeam` | 4 | 2 |
| `Player_HasUpgrade` | 4 | 3 |
| `Player_CompleteUpgrade` | 4 | 3 |
| `Player_IsAlive` | 4 | 4 |
| `Player_GetStrategicPointCaptureProgress` | 4 | 1 |
| `Player_GetResources` | 3 | 3 |
| `Player_SetStateModelBool` | 3 | 3 |
| `Player_GetStateModelFloat` | 3 | 3 |
| `Player_GetEntityCountByUnitType` | 3 | 2 |
| `Player_GetSquadBPCost` | 2 | 2 |
| `Player_GetAllEntities` | 2 | 2 |
| `Player_GetResourceRate` | 2 | 2 |
| `Player_GetAll` | 2 | 2 |
| `Player_GetEntitiesFromType` | 2 | 1 |
| `Player_GetStateModelInt` | 2 | 2 |
| `Player_CanConstruct` | 2 | 2 |
| `Player_SetMaxPopulation` | 2 | 1 |
| `Player_IsHuman` | 1 | 1 |
| `Player_RemoveUpgrade` | 1 | 1 |
| `Player_GetDisplayName` | 1 | 1 |
| `Player_GetMaximumAge` | 1 | 1 |

### Entity (38 functions, 526 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Entity_IsOfType` | 210 | 18 |
| `Entity_IsEBPOfType` | 85 | 3 |
| `Entity_HasBlueprint` | 31 | 3 |
| `Entity_GetID` | 26 | 5 |
| `Entity_GetBuildingProgress` | 21 | 10 |
| `Entity_GetPosition` | 19 | 8 |
| `Entity_FromID` | 18 | 9 |
| `Entity_GetProductionQueueSize` | 11 | 7 |
| `Entity_IsAlive` | 11 | 3 |
| `Entity_GetPlayerOwner` | 10 | 5 |
| `Entity_IsValid` | 10 | 7 |
| `Entity_GetProductionQueueItemType` | 9 | 4 |
| `Entity_GetProductionQueueItem` | 8 | 5 |
| `Entity_GetBlueprint` | 8 | 5 |
| `Entity_CancelProductionQueueItem` | 7 | 2 |
| `Entity_HasProductionQueue` | 6 | 2 |
| `Entity_GetStateModelBool` | 4 | 3 |
| `Entity_RemoveAbility` | 3 | 2 |
| `Entity_HasAbility` | 3 | 2 |
| `Entity_Spawn` | 3 | 2 |
| `Entity_SnapToGridAndGround` | 2 | 2 |
| `Entity_ForceConstruct` | 2 | 2 |
| `Entity_IsProductionQueueAvailable` | 2 | 2 |
| `Entity_Destroy` | 2 | 2 |
| `Entity_Kill` | 2 | 2 |
| `Entity_VisHide` | 1 | 1 |
| `Entity_GetHealthPercentage` | 1 | 1 |
| `Entity_IsBuilding` | 1 | 1 |
| `Entity_IsPlannedStructure` | 1 | 1 |
| `Entity_CreateFacing` | 1 | 1 |
| `Entity_SetPlayerOwner` | 1 | 1 |
| `Entity_SetInvulnerableMinCap` | 1 | 1 |
| `Entity_Create` | 1 | 1 |
| `Entity_GetHeading` | 1 | 1 |
| `Entity_AddAbility` | 1 | 1 |
| `Entity_SetTargetingType` | 1 | 1 |
| `Entity_GetSquad` | 1 | 1 |
| `Entity_SetHealth` | 1 | 1 |

### BP (13 functions, 484 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `BP_GetSquadBlueprint` | 354 | 10 |
| `BP_GetName` | 37 | 3 |
| `BP_GetUpgradeBlueprint` | 29 | 4 |
| `BP_GetEntityBlueprintsWithType` | 21 | 6 |
| `BP_GetEntityBlueprint` | 19 | 9 |
| `BP_GetSquadUIInfo` | 6 | 2 |
| `BP_GetUpgradeUIInfo` | 4 | 4 |
| `BP_GetAbilityBlueprint` | 4 | 2 |
| `BP_IsUpgradeOfType` | 3 | 3 |
| `BP_GetSquadBlueprintsWithType` | 2 | 1 |
| `BP_GetEntityUIInfo` | 2 | 2 |
| `BP_GetPropertyBagGroupCount` | 2 | 1 |
| `BP_GetSquadBlueprints` | 1 | 1 |

### Debug (241 functions, 473 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Debug_AskYesNo` | 30 | 4 |
| `Debug_FocusPlayer` | 8 | 2 |
| `Debug_PlayerUI_Anim_TogglePaths` | 8 | 1 |
| `Debug_PlayerUI_Anim_Snapshot` | 7 | 1 |
| `Debug_ForceKeepDestroy` | 6 | 2 |
| `Debug_RegisterHook` | 6 | 2 |
| `Debug_RegisterRule` | 6 | 1 |
| `Debug_Answer` | 5 | 1 |
| `Debug_PlayerUI_Anim_Features` | 5 | 1 |
| `Debug_RunSpawnPlan` | 5 | 2 |
| `Debug_PlayerUI_Anim_ApplyWhenVisible` | 5 | 1 |
| `Debug_PlayerUI` | 5 | 2 |
| `Debug_LeaverConversion_Full` | 5 | 1 |
| `Debug_ForceTransferTest` | 5 | 1 |
| `Debug_PlayerUI_Anim_ToggleProbe` | 5 | 1 |
| `Debug_ForceDisconnect` | 4 | 2 |
| `Debug_StepMode` | 4 | 2 |
| `Debug_PlayerUI_Anim_FeatureStatus` | 4 | 1 |
| `Debug_ForceSurrender` | 4 | 2 |
| `Debug_PauseAI` | 4 | 2 |
| `Debug_Get_EliminationSettleState` | 4 | 1 |
| `Debug_ForceEliminatePlayer` | 4 | 2 |
| `Debug_ClearHooks` | 3 | 2 |
| `Debug_Get_RankingAnimKeyAudit` | 3 | 1 |
| `Debug_Get_RankingOverview` | 3 | 1 |
| `Debug_LeaverWeaponAudit` | 3 | 1 |
| `Debug_PlayerUI_Anim_RestoreStage3` | 3 | 1 |
| `Debug_PrecacheManifest_Gaps` | 3 | 1 |
| `Debug_PlayerUI_Anim_RestoreStage5` | 3 | 1 |
| `Debug_ListSettings` | 3 | 1 |
| `Debug_Get_RewardPlaybackState` | 3 | 1 |
| `Debug_Get_RewardHealthSummary` | 3 | 1 |
| `Debug_ResumeAI` | 3 | 2 |
| `Debug_FireHook` | 3 | 2 |
| `Debug_PlayerUI_Anim_RestoreStage4` | 3 | 1 |
| `Debug_ForceAnnihilation` | 3 | 1 |
| `Debug_PlayerUI_RewardPlayback_Snapshot` | 3 | 1 |
| `Debug_AutoPop_FullValidation` | 3 | 1 |
| `Debug_PlayerUI_Anim_MonitorStop` | 3 | 1 |
| `Debug_FullSystemValidation` | 3 | 1 |
| `Debug_PlayerUI_Anim_RestoreStage2` | 3 | 1 |
| `Debug_PlayerUI_Anim_RestoreStage1` | 3 | 1 |
| `Debug_Continue` | 3 | 1 |
| `Debug_LeaverCoverage_Pair` | 2 | 1 |
| `Debug_AutoPop_CheckReconcilerState` | 2 | 1 |
| `Debug_CivOverview_Summary` | 2 | 1 |
| `Debug_PlayerUI_Anim` | 2 | 1 |
| `Debug_AutoPop_CheckCapAlignment` | 2 | 1 |
| `Debug_AdvStress_ConcurrentThrash` | 2 | 1 |
| `Debug_GetBuildingLimitState` | 2 | 2 |
| `Debug_TransferValidation` | 2 | 1 |
| `Debug_EventProbes` | 2 | 2 |
| `Debug_LeaverCrossCivMatrix` | 2 | 1 |
| `Debug_DataExtract_AllBlueprints` | 2 | 1 |
| `Debug_CivOverview_Civ` | 2 | 1 |
| `Debug_LeaverCoverage_Civ` | 2 | 1 |
| `Debug_AutoPop_CheckRewardSuppression` | 2 | 1 |
| `Debug_CivOverview_Build` | 2 | 1 |
| `Debug_PlayerUI_Anim_TogglePresetFull` | 2 | 1 |
| `Debug_AdvStress_BuildingLimitOscillation` | 2 | 1 |
| `Debug_Skip` | 2 | 1 |
| `Debug_ValidateModules` | 2 | 1 |
| `Debug_AutoPop_PrintSummary` | 2 | 1 |
| `Debug_AdvStress_SiegeCascade` | 2 | 1 |
| `Debug_ScenarioStop` | 2 | 1 |
| `Debug_DataExtract_RaceSquads` | 2 | 1 |
| `Debug_CivOverview_Audit` | 2 | 1 |
| `Debug_SealModuleRegistry` | 2 | 2 |
| `Debug_AdvStress_BlueprintStorm` | 2 | 1 |
| `Debug_PlayerUI_RewardPlayback_Inject` | 2 | 1 |
| `Debug_ListModules` | 2 | 1 |
| `Debug_AutoPop_CheckEventDriven` | 2 | 1 |
| `Debug_ListHooks` | 2 | 1 |
| `Debug_PlayerUI_RegressionCheck` | 2 | 1 |
| `Debug_GetSiegeLimitState` | 2 | 2 |
| `Debug_LimitEnforcementValidator` | 2 | 1 |
| `Debug_RegisterModule` | 2 | 2 |
| `Debug_InteractiveCheck_Precache` | 2 | 1 |
| `Debug_ConstructionTrace` | 2 | 1 |
| `Debug_SpawnPlan_SiegeStress` | 2 | 2 |
| `Debug_AutoPop_CheckUpgradeLocks` | 2 | 1 |
| `Debug_LeaverMilTest` | 2 | 1 |
| `Debug_DataExtract_UnitCosts` | 2 | 1 |
| `Debug_Confirm` | 2 | 1 |
| `Debug_FullValidation_All` | 2 | 1 |
| `Debug_LeaverMilCoverage_Pair` | 2 | 1 |
| `Debug_CoverageTest` | 2 | 2 |
| `Debug_DataExtract_BuildingData` | 2 | 1 |
| `Debug_SiegeTest` | 2 | 1 |
| `Debug_LeaverConversion_Stress` | 2 | 1 |
| `Debug_PlayerUI_Anim_RestoreStage6` | 2 | 1 |
| `Debug_Demo_RewardPlayback` | 2 | 1 |
| `Debug_InteractiveCheck_SiegeLimitUI` | 2 | 1 |
| `Debug_PlayerUI_RewardPlayback_CaptureFull` | 2 | 1 |
| `Debug_AutoPop_CheckBuildingLocks` | 2 | 1 |
| `Debug_GetPostDefeatState` | 2 | 2 |
| `Debug_FullValidation` | 2 | 2 |
| `Debug_LeaverConversion_VisualCleanup` | 2 | 2 |
| `Debug_AdvStress_RapidElimination` | 2 | 1 |
| `Debug_PlayerUI_Anim_Monitor` | 2 | 1 |
| `Debug_Reject` | 2 | 1 |
| `Debug_GetLeaverBalanceState` | 2 | 2 |
| `Debug_GetLimitsUIState` | 2 | 2 |
| `Debug_CivOverview_DumpStructured` | 2 | 1 |
| `Debug_RunSmokeTests` | 2 | 2 |
| `Debug_LeaverConversion_VisualByCiv` | 2 | 1 |
| `Debug_KeepAsCapitalStatus` | 2 | 1 |
| `Debug_AdvStress_MaxPopPressure` | 2 | 1 |
| `Debug_InteractiveCheck_KeepState` | 2 | 1 |
| `Debug_StressTest` | 2 | 2 |
| `Debug_LeaverTransferInspector` | 2 | 1 |
| `Debug_AskChoice` | 2 | 1 |
| `Debug_PlayerUI_Anim_SetMinimalHud` | 2 | 1 |
| `Debug_ListRules` | 2 | 1 |
| `Debug_CheckRules` | 2 | 1 |
| `Debug_RunAll` | 2 | 1 |
| `Debug_ValidateSiegeClassifications` | 1 | 1 |
| `Debug_ListPlayerSlots` | 1 | 1 |
| `Debug_TeamBalancePerLimit` | 1 | 1 |
| `Debug_SiegeLimitFullDump` | 1 | 1 |
| `Debug_ToggleOverlays` | 1 | 1 |
| `Debug_AIBehavior_Scenario` | 1 | 1 |
| `Debug_PlayerUI_Anim_TogglePresetHudOnly` | 1 | 1 |
| `Debug_StressStage` | 1 | 1 |
| `Debug_SiegeStatus` | 1 | 1 |
| `Debug_AutoPopHouseGuard` | 1 | 1 |
| `Debug_GetKeepOwnershipMap` | 1 | 1 |
| `Debug_LeaverValidation` | 1 | 1 |
| `Debug_VerifyDynastiesData` | 1 | 1 |
| `Debug_LeaverPipelineStatus` | 1 | 1 |
| `Debug_PlayerUI_Anim_Stress` | 1 | 1 |
| `Debug_PrecacheManifest_Confirmed` | 1 | 1 |
| `Debug_AdvancedStressAll` | 1 | 1 |
| `Debug_GetTagModuleMap` | 1 | 1 |
| `Debug_ValidateAgeGateCoverage` | 1 | 1 |
| `Debug_GetSetting` | 1 | 1 |
| `Debug_PlayerUI_UI` | 1 | 1 |
| `Debug_GetAutoAgeStatus` | 1 | 1 |
| `Debug_AIBehavior` | 1 | 1 |
| `Debug_PrecacheManifest_ForcedCoverage` | 1 | 1 |
| `Debug_PrecacheManifest_Report` | 1 | 1 |
| `Debug_LeaverMilProof_OneShot` | 1 | 1 |
| `Debug_QADiagnosticStatus` | 1 | 1 |
| `Debug_ResetSettings` | 1 | 1 |
| `Debug_Scenario` | 1 | 1 |
| `Debug_ValidateSpawnAnchors` | 1 | 1 |
| `Debug_GetBestAllyInfo` | 1 | 1 |
| `Debug_ComprehensiveStress_Cat` | 1 | 1 |
| `Debug_BlueprintAudit_Civ` | 1 | 1 |
| `Debug_ComprehensiveStressStatus` | 1 | 1 |
| `Debug_SetBaseline` | 1 | 1 |
| `Debug_RamSiegeTowerLimitState` | 1 | 1 |
| `Debug_SpawnPlan_MixedArmy` | 1 | 1 |
| `Debug_FactionMapDiagnostic` | 1 | 1 |
| `Debug_GetModuleCount` | 1 | 1 |
| `Debug_GetPopCap` | 1 | 1 |
| `Debug_LeaverCoverage_AllCivPairs` | 1 | 1 |
| `Debug_LimitsUI_TraceUpdateFlow` | 1 | 1 |
| `Debug_GetAllModuleManifests` | 1 | 1 |
| `Debug_GetAllSettingSchemas` | 1 | 1 |
| `Debug_PlayerUI_RewardPlayback_SkipPhase` | 1 | 1 |
| `Debug_GetAutoAgeState` | 1 | 1 |
| `Debug_EnumerateAllCivUnits` | 1 | 1 |
| `Debug_LeaverPerformance` | 1 | 1 |
| `Debug_ValidateAutoPopulation` | 1 | 1 |
| `Debug_PlayerUI_Elim_ValidateFull` | 1 | 1 |
| `Debug_RuleInfo` | 1 | 1 |
| `Debug_ComprehensiveStressStop` | 1 | 1 |
| `Debug_PlayerUI_RewardPlayback_ValidateCycle` | 1 | 1 |
| `Debug_RunFullValidation` | 1 | 1 |
| `Debug_RuleReport` | 1 | 1 |
| `Debug_LimitsUIStress` | 1 | 1 |
| `Debug_DataExtract_Summary` | 1 | 1 |
| `Debug_ModuleInfo` | 1 | 1 |
| `Debug_SetSetting` | 1 | 1 |
| `Debug_RamLimitFullTrace` | 1 | 1 |
| `Debug_CoverageBatch` | 1 | 1 |
| `Debug_PlayerUI_RewardPlayback_InjectReal` | 1 | 1 |
| `Debug_PlayerUI_Anim_ValidateDataContext` | 1 | 1 |
| `Debug_SiegeLimitStressTest` | 1 | 1 |
| `Debug_LeaverSpawnerExemptProof` | 1 | 1 |
| `Debug_KeepAsCapitalApply` | 1 | 1 |
| `Debug_SiegePerfReset` | 1 | 1 |
| `Debug_FocusPosition` | 1 | 1 |
| `Debug_RecountValidate` | 1 | 1 |
| `Debug_GetVillagerState` | 1 | 1 |
| `Debug_QADiagnostic_TransferScenarios` | 1 | 1 |
| `Debug_LeaverResolve_ForcedBP` | 1 | 1 |
| `Debug_PlayerUI_Anim_Pulse` | 1 | 1 |
| `Debug_ScenarioStatus` | 1 | 1 |
| `Debug_LeaverWeaponAudit_ReceiverClass` | 1 | 1 |
| `Debug_Run_PlayerUI_PhaseBSuite` | 1 | 1 |
| `Debug_LeaverConversion_Visual` | 1 | 1 |
| `Debug_ComprehensiveStress` | 1 | 1 |
| `Debug_SiegeLimitCrossValidation` | 1 | 1 |
| `Debug_DismissPrompt` | 1 | 1 |
| `Debug_VisualValidation_KeepDestroy` | 1 | 1 |
| `Debug_GetRuleCount` | 1 | 1 |
| `Debug_StepStatus` | 1 | 1 |
| `Debug_GetWonderState` | 1 | 1 |
| `Debug_SpawnAndValidate` | 1 | 1 |
| `Debug_LeaverConversion_MilResolve` | 1 | 1 |
| `Debug_DumpBlueprintsForSuffix` | 1 | 1 |
| `Debug_GetStarterKeepState` | 1 | 1 |
| `Debug_GetReligiousState` | 1 | 1 |
| `Debug_PlayerUI_Ranking` | 1 | 1 |
| `Debug_PlayerUI_Anim_RunStaged` | 1 | 1 |
| `Debug_PopAudit` | 1 | 1 |
| `Debug_PlayerUI_RewardPlayback_Reset` | 1 | 1 |
| `Debug_Spawn` | 1 | 1 |
| `Debug_LeaverTransferInspector_AllPairs` | 1 | 1 |
| `Debug_PlayerUI_Anim_PresetSafe` | 1 | 1 |
| `Debug_PrecacheStatus` | 1 | 1 |
| `Debug_GetSettingSchema` | 1 | 1 |
| `Debug_WaitForVisual` | 1 | 1 |
| `Debug_LeaverSummary` | 1 | 1 |
| `Debug_BlueprintAudit_LeaverFallback` | 1 | 1 |
| `Debug_GetAllRules` | 1 | 1 |
| `Debug_IsRegistrySealed` | 1 | 1 |
| `Debug_GetKillScore` | 1 | 1 |
| `Debug_AIBehaviorStatus` | 1 | 1 |
| `Debug_DependencyGraph` | 1 | 1 |
| `Debug_AutoAge_CheckSpecialUpgradeIds` | 1 | 1 |
| `Debug_LeaverPerformance_6Player` | 1 | 1 |
| `Debug_PrecacheManifest_Summary` | 1 | 1 |
| `Debug_CheckUpgradeBlueprint` | 1 | 1 |
| `Debug_TeamBalanceCapState` | 1 | 1 |
| `Debug_LeaverConversion_Inspect` | 1 | 1 |
| `Debug_PlayerUI_Anim_PresetAll` | 1 | 1 |
| `Debug_LeaverMilCoverage_AllPairs` | 1 | 1 |
| `Debug_InteractiveChecks` | 1 | 1 |
| `Debug_PlayerUI_Data` | 1 | 1 |
| `Debug_VisualValidation_SiegeSpawn` | 1 | 1 |
| `Debug_KeepDiagnostic` | 1 | 1 |
| `Debug_KeepCap_CheckSpecialAgeAbilityResolution` | 1 | 1 |
| `Debug_SlowMotion` | 1 | 1 |
| `Debug_BlueprintAudit` | 1 | 1 |
| `Debug_QADiagnostic` | 1 | 1 |
| `Debug_SiegePerfReport` | 1 | 1 |
| `Debug_QADiagnostic_Topic` | 1 | 1 |
| `Debug_GetOptionParseResults` | 1 | 1 |

### Rule (11 functions, 302 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Rule_AddOneShot` | 117 | 22 |
| `Rule_AddGlobalEvent` | 53 | 19 |
| `Rule_RemoveGlobalEvent` | 32 | 11 |
| `Rule_AddInterval` | 32 | 20 |
| `Rule_Exists` | 23 | 6 |
| `Rule_Unpause` | 15 | 5 |
| `Rule_RemoveMe` | 13 | 7 |
| `Rule_Remove` | 10 | 7 |
| `Rule_Pause` | 5 | 3 |
| `Rule_Add` | 1 | 1 |
| `Rule_IsPaused` | 1 | 1 |

### World (19 functions, 234 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `World_GetGameTime` | 87 | 13 |
| `World_Pos` | 61 | 17 |
| `World_GetPlayerIndex` | 21 | 9 |
| `World_OwnsEntity` | 13 | 6 |
| `World_GetPlayerCount` | 11 | 6 |
| `World_GetHeightAt` | 6 | 4 |
| `World_GetGameTicks` | 6 | 4 |
| `World_GetAllNeutralEntities` | 5 | 4 |
| `World_GetRand` | 4 | 2 |
| `World_GetWidth` | 4 | 3 |
| `World_KillPlayer` | 4 | 4 |
| `World_GetPlayerAt` | 3 | 2 |
| `World_GetRaceIcon` | 2 | 2 |
| `World_GetLength` | 2 | 2 |
| `World_OwnsSquad` | 1 | 1 |
| `World_GetEntitiesNearPoint` | 1 | 1 |
| `World_GetBlueprintEntities` | 1 | 1 |
| `World_IsMultiplayerGame` | 1 | 1 |
| `World_GetSquadsNearPoint` | 1 | 1 |

### Core (10 functions, 225 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Core_GetPlayersTableEntry` | 55 | 18 |
| `Core_RegisterModule` | 43 | 39 |
| `Core_IsPlayerEliminated` | 38 | 9 |
| `Core_UnregisterModule` | 32 | 27 |
| `Core_CallDelegateFunctions` | 32 | 6 |
| `Core_SetPlayerDefeated` | 9 | 7 |
| `Core_OnGameOver` | 6 | 4 |
| `Core_SetPlayerVictorious` | 5 | 4 |
| `Core_IsModuleRegistered` | 3 | 3 |
| `Core_WinnerlessGameOver` | 2 | 2 |

### Squad (10 functions, 212 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Squad_IsOfType` | 135 | 6 |
| `Squad_IsSBPOfType` | 52 | 3 |
| `Squad_GetPlayerOwner` | 6 | 2 |
| `Squad_SetPlayerOwner` | 4 | 1 |
| `Squad_IsAlive` | 4 | 2 |
| `Squad_Destroy` | 3 | 2 |
| `Squad_GetBlueprint` | 3 | 2 |
| `Squad_GetFirstEntity` | 3 | 1 |
| `Squad_IsIdle` | 1 | 1 |
| `Squad_GetPosition` | 1 | 1 |

### UI (19 functions, 184 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `UI_CreateEventCueClickable` | 44 | 8 |
| `UI_SetPropertyValue` | 41 | 3 |
| `UI_CreateCommand` | 15 | 5 |
| `UI_AddChild` | 15 | 6 |
| `UI_CreateDataContext` | 14 | 6 |
| `UI_SetDataContext` | 12 | 6 |
| `UI_SetEntityDataContext` | 8 | 1 |
| `UI_CreateEventCue` | 8 | 3 |
| `UI_CreateMinimapBlipOnPosFrom` | 6 | 1 |
| `UI_StopFlashing` | 5 | 1 |
| `UI_IsReplay` | 4 | 4 |
| `UI_GetColourAsString` | 3 | 3 |
| `UI_FlashObjectiveIcon` | 3 | 1 |
| `UI_RemoveEventHandler` | 1 | 1 |
| `UI_Remove` | 1 | 1 |
| `UI_AddEventHandler` | 1 | 1 |
| `UI_SetShowPlayerScores` | 1 | 1 |
| `UI_SetPlayerDataContext` | 1 | 1 |
| `UI_CreateMinimapBlip` | 1 | 1 |

### EGroup (14 functions, 155 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `EGroup_Destroy` | 24 | 9 |
| `EGroup_Count` | 23 | 6 |
| `EGroup_CountSpawned` | 22 | 10 |
| `EGroup_GetEntityAt` | 20 | 7 |
| `EGroup_GetSpawnedEntityAt` | 17 | 6 |
| `EGroup_Filter` | 16 | 8 |
| `EGroup_ForEach` | 8 | 5 |
| `EGroup_DestroyAllEntities` | 7 | 6 |
| `EGroup_CreateUnique` | 7 | 6 |
| `EGroup_CreateIfNotFound` | 3 | 3 |
| `EGroup_Clear` | 2 | 2 |
| `EGroup_GetPosition` | 2 | 1 |
| `EGroup_Add` | 2 | 2 |
| `EGroup_Create` | 2 | 2 |

### Obj (16 functions, 149 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Obj_SetProgress` | 23 | 6 |
| `Obj_SetCounterCount` | 20 | 6 |
| `Obj_SetState` | 17 | 7 |
| `Obj_SetVisible` | 14 | 7 |
| `Obj_SetCounterType` | 11 | 7 |
| `Obj_Create` | 11 | 7 |
| `Obj_CreatePopup` | 11 | 4 |
| `Obj_SetCounterMax` | 9 | 6 |
| `Obj_SetTitle` | 9 | 4 |
| `Obj_SetProgressVisible` | 7 | 6 |
| `Obj_SetCounterTimerSeconds` | 6 | 3 |
| `Obj_GetState` | 5 | 2 |
| `Obj_GetCounterType` | 2 | 1 |
| `Obj_Delete` | 2 | 1 |
| `Obj_SetColour` | 1 | 1 |
| `Obj_GetCounterCount` | 1 | 1 |

### SGroup (10 functions, 126 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `SGroup_Count` | 34 | 8 |
| `SGroup_GetSquadAt` | 21 | 7 |
| `SGroup_CreateIfNotFound` | 18 | 7 |
| `SGroup_CreateUnique` | 15 | 7 |
| `SGroup_Clear` | 15 | 2 |
| `SGroup_Destroy` | 10 | 3 |
| `SGroup_DestroyAllSquads` | 5 | 4 |
| `SGroup_Filter` | 4 | 4 |
| `SGroup_ForEach` | 2 | 2 |
| `SGroup_AddGroup` | 2 | 1 |

### Timer (7 functions, 58 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Timer_Exists` | 22 | 4 |
| `Timer_GetRemaining` | 19 | 5 |
| `Timer_End` | 8 | 3 |
| `Timer_Start` | 6 | 4 |
| `Timer_Resume` | 1 | 1 |
| `Timer_Pause` | 1 | 1 |
| `Timer_GetElapsed` | 1 | 1 |

### Modifier (2 functions, 37 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Modifier_Create` | 19 | 9 |
| `Modifier_ApplyToPlayer` | 18 | 8 |

### Game (3 functions, 35 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Game_GetLocalPlayer` | 28 | 16 |
| `Game_TransitionToState` | 6 | 1 |
| `Game_SendCustomChallengeEvent` | 1 | 1 |

### Music (4 functions, 20 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Music_LockIntensity` | 6 | 2 |
| `Music_PlayStinger` | 6 | 3 |
| `Music_UnlockIntensity` | 5 | 3 |
| `Music_PersistentStop` | 3 | 3 |

### Sound (1 functions, 15 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Sound_Play2D` | 15 | 4 |

### Misc (5 functions, 15 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Misc_ClearSelection` | 6 | 3 |
| `Misc_GetCommandLineString` | 4 | 2 |
| `Misc_IsCommandLineOptionSet` | 3 | 3 |
| `Misc_IsSquadOnScreen` | 1 | 1 |
| `Misc_SetEntitySelectable` | 1 | 1 |

### FOW (6 functions, 13 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `FOW_RevealArea` | 5 | 4 |
| `FOW_UnRevealArea` | 2 | 2 |
| `FOW_ExploreAll` | 2 | 2 |
| `FOW_ForceRevealAllUnblockedAreas` | 2 | 2 |
| `FOW_UnExploreAll` | 1 | 1 |
| `FOW_UIRevealAll` | 1 | 1 |

### Util (5 functions, 12 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Util_GetPositionFromAtoB` | 3 | 2 |
| `Util_GetPlayerOwner` | 3 | 3 |
| `Util_GetOffsetPosition` | 3 | 2 |
| `Util_PrintObject` | 2 | 1 |
| `Util_CreateEntities` | 1 | 1 |

### Objective (3 functions, 7 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Objective_IsComplete` | 4 | 1 |
| `Objective_Complete` | 2 | 1 |
| `Objective_Start` | 1 | 1 |

### Taskbar (1 functions, 6 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Taskbar_SetVisibility` | 6 | 3 |

### Setup (1 functions, 5 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Setup_GetWinConditionOptions` | 5 | 3 |

### EBP (1 functions, 4 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `EBP_Exists` | 4 | 1 |

### SBP (1 functions, 4 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `SBP_Exists` | 4 | 1 |

### HintPoint (2 functions, 3 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `HintPoint_Add` | 2 | 1 |
| `HintPoint_Remove` | 1 | 1 |

### AI (1 functions, 2 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `AI_PauseCurrentTasks` | 2 | 1 |

### Camera (1 functions, 1 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Camera_MoveTo` | 1 | 1 |

### Table (1 functions, 1 calls)

| Function | Calls | Files |
|----------|-------|-------|
| `Table_Contains` | 1 | 1 |

## Top 20 Files by API Call Density

| # | File | API Calls |
|---|------|-----------|
| 1 | gameplay/cba_options.scar | 625 |
| 2 | rewards.scar | 564 |
| 3 | rewards/cba_rewards_onslaught.scar | 548 |
| 4 | cba.scar | 438 |
| 5 | debug/cba_debug_leaver.scar | 277 |
| 6 | cba_religious.scar | 261 |
| 7 | wonder.scar | 200 |
| 8 | conditions/ags_wonder.scar | 176 |
| 9 | gameplay/ags_limits_ui.scar | 148 |
| 10 | debug/cba_debug_playerui_anim.scar | 135 |
| 11 | debug/cba_debug_inspectors.scar | 126 |
| 12 | ags_global_settings.scar | 114 |
| 13 | gameplay/cba_auto_age.scar | 94 |
| 14 | rewards/cba_rewards.scar | 94 |
| 15 | helpers/ags_blueprints.scar | 93 |
| 16 | conditions/ags_annihilation.scar | 88 |
| 17 | debug/cba_debug_helpers.scar | 81 |
| 18 | gameplay/ags_auto_population.scar | 67 |
| 19 | observerui/observerui.scar | 66 |
| 20 | debug/cba_debug_siege_test.scar | 66 |

