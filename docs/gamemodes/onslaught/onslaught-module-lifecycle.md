# Onslaught Module Lifecycle Map

Auto-generated on 2026-04-02 05:31. Maps all registered modules to their lifecycle delegate functions.

- **41** registered modules
- **566** delegate function implementations
- **22** canonical lifecycle phases

## Lifecycle Phase Order

Delegates are called in this order during match initialization (from `cba.scar`):

1. **SetupSettings** — 1 modules
2. **AdjustSettings** — 3 modules
3. **UpdateModuleSettings** — 31 modules
4. **DiplomacyEnabled** — 2 modules
5. **TributeEnabled** — 1 modules
6. **EarlyInitializations** — 8 modules
7. **LateInitializations** — 2 modules
8. **PresetInitialize** — 1 modules
9. **PresetExecute** — 1 modules
10. **PresetFinalize** — 18 modules
11. **PrepareStart** — 1 modules
12. **OnStarting** — 1 modules
13. **OnPlay** — 8 modules
14. **OnPlayerDefeated** — 12 modules
15. **OnGameOver** — 10 modules
16. **OnObjectiveToggle** — 2 modules
17. **TreatyStarted** — 2 modules
18. **TreatyEnded** — 2 modules
19. **OnDamageReceived** — 3 modules
20. **OnEntityKilled** — 7 modules
21. **OnLandmarkDestroyed** — 2 modules
22. **OnConstructionComplete** — 7 modules

## Phase Participation Matrix

| Module | SetupSettings | AdjustSettings | UpdateModuleSettings | DiplomacyEnabled | TributeEnabled | EarlyInitializations | LateInitializations | PresetInitialize | PresetExecute | PresetFinalize | PrepareStart | OnStarting | OnPlay |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| _religious.module |  |  |  |  |  |  |  |  |  |  |  |  |  |
| AGS_Annihilation |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  | ✓ |
| AGS_AutoResources |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_Elimination |  |  | ✓ |  |  |  |  |  |  |  |  |  |  |
| AGS_GameRates |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_GatherRates |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_GlobalSettings | ✓ |  |  |  |  | ✓ |  |  |  |  |  |  |  |
| AGS_Handicaps |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_LimitsUI |  |  | ✓ |  |  | ✓ |  |  |  |  |  |  | ✓ |
| AGS_MatchUI |  |  | ✓ |  |  | ✓ |  |  |  |  |  |  | ✓ |
| AGS_MedicPopulationCapacity |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_NoArsenal |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_NoDock |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_NoSiege |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_NoWall |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_PopulationAutomatic |  |  | ✓ |  |  | ✓ |  |  |  | ✓ |  |  |  |
| AGS_PopulationCapacity |  | ✓ | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_RevealFowOnElimination |  |  | ✓ |  |  |  |  |  |  |  |  |  |  |
| AGS_Scattered |  | ✓ | ✓ |  |  | ✓ |  | ✓ | ✓ |  |  | ✓ |  |
| AGS_SpecialPopulationUI |  |  | ✓ |  |  | ✓ |  |  |  |  |  |  | ✓ |
| AGS_StartingAge |  |  | ✓ |  |  |  | ✓ |  |  |  |  |  |  |
| AGS_Surrender |  |  | ✓ |  |  |  |  |  |  |  |  |  | ✓ |
| AGS_TeamBalance |  |  | ✓ |  |  |  |  |  |  |  |  |  |  |
| AGS_Teams |  |  |  |  |  | ✓ |  |  |  |  |  |  |  |
| AGS_Testing |  |  | ✓ |  |  |  |  |  |  |  |  |  | ✓ |
| AGS_TreeBombardment |  |  | ✓ |  |  |  |  |  |  |  | ✓ |  |  |
| AGS_UnitRates |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| AGS_Utilities |  | ✓ | ✓ |  |  |  | ✓ |  |  |  |  |  | ✓ |
| AGS_Wonder |  |  | ✓ |  |  |  |  |  |  |  |  |  | ✓ |
| Annihilation |  |  |  | ✓ | ✓ |  |  |  |  |  |  |  |  |
| CBA_AutoAge |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| CBA_Debug |  |  | ✓ |  |  | ✓ |  |  |  |  |  |  |  |
| CBA_HREBalance |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| CBA_Options |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| CBA_REWARDS_CBAULE |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Mod |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Nomad |  |  | ✓ |  |  |  |  |  |  | ✓ |  |  |  |
| ObserverUI |  |  |  |  |  |  |  |  |  |  |  |  |  |
| ObserverUI_GameStateTracking_Tribute |  |  |  |  |  |  |  |  |  |  |  |  |  |
| PlayerUI |  |  |  |  |  |  |  |  |  | ✓ |  |  |  |
| Wonder |  |  |  | ✓ |  |  |  |  |  |  |  |  |  |

## Module Details

### _religious.module

- **Registration:** cba_religious.scar:78
- **Delegates:** 0

### AGS_Annihilation

- **Registration:** conditions/ags_annihilation.scar:32
- **Delegates:** 20

| Phase | Function | File | Line |
|-------|----------|------|------|
| AreOnlyValidSquads | `AGS_Annihilation_AreOnlyValidSquads` | conditions/ags_annihilation.scar | 173 |
| CheckAnnihilation | `AGS_Annihilation_CheckAnnihilation` | conditions/ags_annihilation.scar | 153 |
| CreateObjective | `AGS_Annihilation_CreateObjective` | conditions/ags_annihilation.scar | 133 |
| DefineCheapestSquads | `AGS_Annihilation_DefineCheapestSquads` | conditions/ags_annihilation.scar | 199 |
| Eliminate | `AGS_Annihilation_Eliminate` | conditions/ags_annihilation.scar | 142 |
| IsAbleToProduce | `AGS_Annihilation_IsAbleToProduce` | conditions/ags_annihilation.scar | 213 |
| OnConstructionComplete | `AGS_Annihilation_OnConstructionComplete` | conditions/ags_annihilation.scar | 116 |
| OnDamageReceived | `AGS_Annihilation_OnDamageReceived` | conditions/ags_annihilation.scar | 97 |
| OnEntityKilled | `AGS_Annihilation_OnEntityKilled` | conditions/ags_annihilation.scar | 104 |
| OnGameOver | `AGS_Annihilation_OnGameOver` | conditions/ags_annihilation.scar | 84 |
| OnLandmarkDestroyed | `AGS_Annihilation_OnLandmarkDestroyed` | conditions/ags_annihilation.scar | 110 |
| OnObjectiveToggle | `AGS_Annihilation_OnObjectiveToggle` | conditions/ags_annihilation.scar | 77 |
| OnPlay | `AGS_Annihilation_OnPlay` | conditions/ags_annihilation.scar | 46 |
| OnPlayerDefeated | `AGS_Annihilation_OnPlayerDefeated` | conditions/ags_annihilation.scar | 65 |
| PlayerCanReceiveTribute | `AGS_Annihilation_PlayerCanReceiveTribute` | conditions/ags_annihilation.scar | 287 |
| PresetFinalize | `AGS_Annihilation_PresetFinalize` | conditions/ags_annihilation.scar | 41 |
| RemoveObjective | `AGS_Annihilation_RemoveObjective` | conditions/ags_annihilation.scar | 138 |
| TreatyEnded | `AGS_Annihilation_TreatyEnded` | conditions/ags_annihilation.scar | 60 |
| TreatyStarted | `AGS_Annihilation_TreatyStarted` | conditions/ags_annihilation.scar | 55 |
| UpdateModuleSettings | `AGS_Annihilation_UpdateModuleSettings` | conditions/ags_annihilation.scar | 34 |

### AGS_AutoResources

- **Registration:** gameplay/ags_auto_resources.scar:16
- **Delegates:** 2

| Phase | Function | File | Line |
|-------|----------|------|------|
| PresetFinalize | `AGS_AutoResources_PresetFinalize` | gameplay/ags_auto_resources.scar | 24 |
| UpdateModuleSettings | `AGS_AutoResources_UpdateModuleSettings` | gameplay/ags_auto_resources.scar | 18 |

### AGS_Elimination

- **Registration:** conditions/ags_elimination.scar:21
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| OnPlayerAITakeover | `AGS_Elimination_OnPlayerAITakeover` | conditions/ags_elimination.scar | 30 |
| OnPlayerDefeated | `AGS_Elimination_OnPlayerDefeated` | conditions/ags_elimination.scar | 60 |
| UpdateModuleSettings | `AGS_Elimination_UpdateModuleSettings` | conditions/ags_elimination.scar | 23 |

### AGS_GameRates

- **Registration:** gameplay/ags_game_rates.scar:17
- **Delegates:** 4

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyBonus | `AGS_GameRates_ApplyBonus` | gameplay/ags_game_rates.scar | 38 |
| ApplyModifier | `AGS_GameRates_ApplyModifier` | gameplay/ags_game_rates.scar | 51 |
| PresetFinalize | `AGS_GameRates_PresetFinalize` | gameplay/ags_game_rates.scar | 27 |
| UpdateModuleSettings | `AGS_GameRates_UpdateModuleSettings` | gameplay/ags_game_rates.scar | 20 |

### AGS_GatherRates

- **Registration:** gameplay/ags_gather_rates.scar:17
- **Delegates:** 4

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyBonus | `AGS_GatherRates_ApplyBonus` | gameplay/ags_gather_rates.scar | 36 |
| ApplyModifier | `AGS_GatherRates_ApplyModifier` | gameplay/ags_gather_rates.scar | 51 |
| PresetFinalize | `AGS_GatherRates_PresetFinalize` | gameplay/ags_gather_rates.scar | 26 |
| UpdateModuleSettings | `AGS_GatherRates_UpdateModuleSettings` | gameplay/ags_gather_rates.scar | 19 |

### AGS_GlobalSettings

- **Registration:** ags_global_settings.scar:231
- **Delegates:** 48

| Phase | Function | File | Line |
|-------|----------|------|------|
| CBA_Rewards | `AGS_GlobalSettings_CBA_Rewards` | ags_global_settings.scar | 1418 |
| DefineCbaSettings | `AGS_GlobalSettings_DefineCbaSettings` | ags_global_settings.scar | 574 |
| DefineGameConditions | `AGS_GlobalSettings_DefineGameConditions` | ags_global_settings.scar | 355 |
| DefineGameSettings | `AGS_GlobalSettings_DefineGameSettings` | ags_global_settings.scar | 423 |
| DefineHandicapSettings | `AGS_GlobalSettings_DefineHandicapSettings` | ags_global_settings.scar | 567 |
| DefineLegacySettings | `AGS_GlobalSettings_DefineLegacySettings` | ags_global_settings.scar | 540 |
| DefineMatchSettings | `AGS_GlobalSettings_DefineMatchSettings` | ags_global_settings.scar | 473 |
| DefinePlayerSettings | `AGS_GlobalSettings_DefinePlayerSettings` | ags_global_settings.scar | 467 |
| DefineRestrictionSettings | `AGS_GlobalSettings_DefineRestrictionSettings` | ags_global_settings.scar | 582 |
| DefineWinConditions | `AGS_GlobalSettings_DefineWinConditions` | ags_global_settings.scar | 328 |
| DefineWinSettings | `AGS_GlobalSettings_DefineWinSettings` | ags_global_settings.scar | 381 |
| EarlyInitializations | `AGS_GlobalSettings_EarlyInitializations` | ags_global_settings.scar | 301 |
| OnGameOver | `AGS_GlobalSettings_OnGameOver` | ags_global_settings.scar | 307 |
| OnLocalPlayerChanged | `AGS_GlobalSettings_OnLocalPlayerChanged` | ags_global_settings.scar | 316 |
| RetrieveSlotHandicap | `AGS_GlobalSettings_RetrieveSlotHandicap` | ags_global_settings.scar | 1042 |
| SetAutoAge | `AGS_GlobalSettings_SetAutoAge` | ags_global_settings.scar | 1320 |
| SetEndingAge | `AGS_GlobalSettings_SetEndingAge` | ags_global_settings.scar | 843 |
| SetGameRates | `AGS_GlobalSettings_SetGameRates` | ags_global_settings.scar | 1218 |
| SetGatherRates | `AGS_GlobalSettings_SetGatherRates` | ags_global_settings.scar | 1270 |
| SetHandicapType | `AGS_GlobalSettings_SetHandicapType` | ags_global_settings.scar | 1003 |
| SetMaintainTeamBalance | `AGS_GlobalSettings_SetMaintainTeamBalance` | ags_global_settings.scar | 614 |
| SetMapVision | `AGS_GlobalSettings_SetMapVision` | ags_global_settings.scar | 821 |
| SetMaximumMedicPopulation | `AGS_GlobalSettings_SetMaximumMedicPopulation` | ags_global_settings.scar | 1352 |
| SetMaximumPopulation | `AGS_GlobalSettings_SetMaximumPopulation` | ags_global_settings.scar | 1156 |
| SetMaximumProductionBuildings | `AGS_GlobalSettings_SetMaximumProductionBuildings` | ags_global_settings.scar | 1376 |
| SetMaximumSiegeWorkshop | `AGS_GlobalSettings_SetMaximumSiegeWorkshop` | ags_global_settings.scar | 1400 |
| SetMinimumPopulation | `AGS_GlobalSettings_SetMinimumPopulation` | ags_global_settings.scar | 1118 |
| SetPopulationinterval | `AGS_GlobalSettings_SetPopulationinterval` | ags_global_settings.scar | 1332 |
| SetReligiousTimer | `AGS_GlobalSettings_SetReligiousTimer` | ags_global_settings.scar | 1076 |
| SetScoreTimer | `AGS_GlobalSettings_SetScoreTimer` | ags_global_settings.scar | 765 |
| SetSettlement | `AGS_GlobalSettings_SetSettlement` | ags_global_settings.scar | 641 |
| SetSimulationSpeed | `AGS_GlobalSettings_SetSimulationSpeed` | ags_global_settings.scar | 955 |
| SetSlotHandicaps | `AGS_GlobalSettings_SetSlotHandicaps` | ags_global_settings.scar | 1015 |
| SetStartingAge | `AGS_GlobalSettings_SetStartingAge` | ags_global_settings.scar | 831 |
| SetStartingKeeps | `AGS_GlobalSettings_SetStartingKeeps` | ags_global_settings.scar | 939 |
| SetStartingKings | `AGS_GlobalSettings_SetStartingKings` | ags_global_settings.scar | 947 |
| SetStartingResources | `AGS_GlobalSettings_SetStartingResources` | ags_global_settings.scar | 871 |
| SetStartingVillagers | `AGS_GlobalSettings_SetStartingVillagers` | ags_global_settings.scar | 889 |
| SetTeamVictory | `AGS_GlobalSettings_SetTeamVictory` | ags_global_settings.scar | 691 |
| SetTeamVision | `AGS_GlobalSettings_SetTeamVision` | ags_global_settings.scar | 811 |
| SetTechnologyAge | `AGS_GlobalSettings_SetTechnologyAge` | ags_global_settings.scar | 857 |
| SetTownCenterRestricts | `AGS_GlobalSettings_SetTownCenterRestricts` | ags_global_settings.scar | 993 |
| SetTreaty | `AGS_GlobalSettings_SetTreaty` | ags_global_settings.scar | 653 |
| SetTreatyTimer | `AGS_GlobalSettings_SetTreatyTimer` | ags_global_settings.scar | 661 |
| SetUnitRates | `AGS_GlobalSettings_SetUnitRates` | ags_global_settings.scar | 1192 |
| SetupSettings | `AGS_GlobalSettings_SetupSettings` | ags_global_settings.scar | 233 |
| SetWonderScaleCost | `AGS_GlobalSettings_SetWonderScaleCost` | ags_global_settings.scar | 743 |
| SetWonderTimer | `AGS_GlobalSettings_SetWonderTimer` | ags_global_settings.scar | 701 |

### AGS_Handicaps

- **Registration:** gameplay/ags_handicaps.scar:28
- **Delegates:** 9

| Phase | Function | File | Line |
|-------|----------|------|------|
| AddModifier | `AGS_Handicaps_AddModifier` | gameplay/ags_handicaps.scar | 108 |
| ApplyMilitaryBonus | `AGS_Handicaps_ApplyMilitaryBonus` | gameplay/ags_handicaps.scar | 85 |
| ApplyModifier | `AGS_Handicaps_ApplyModifier` | gameplay/ags_handicaps.scar | 105 |
| ApplyPerPlayer | `AGS_Handicaps_ApplyPerPlayer` | gameplay/ags_handicaps.scar | 46 |
| ApplyWorkerBonus | `AGS_Handicaps_ApplyWorkerBonus` | gameplay/ags_handicaps.scar | 62 |
| CreateListFrom | `AGS_Handicaps_CreateListFrom` | gameplay/ags_handicaps.scar | 113 |
| PresetFinalize | `AGS_Handicaps_PresetFinalize` | gameplay/ags_handicaps.scar | 37 |
| ToRaw | `AGS_Handicaps_ToRaw` | gameplay/ags_handicaps.scar | 126 |
| UpdateModuleSettings | `AGS_Handicaps_UpdateModuleSettings` | gameplay/ags_handicaps.scar | 30 |

### AGS_LimitsUI

- **Registration:** gameplay/ags_limits_ui.scar:200
- **Delegates:** 23

| Phase | Function | File | Line |
|-------|----------|------|------|
| AnimTick | `AGS_LimitsUI_AnimTick` | gameplay/ags_limits_ui.scar | 574 |
| ApplyMargin | `AGS_LimitsUI_ApplyMargin` | gameplay/ags_limits_ui.scar | 692 |
| BlendARGB | `AGS_LimitsUI_BlendARGB` | gameplay/ags_limits_ui.scar | 389 |
| BlendRGB | `AGS_LimitsUI_BlendRGB` | gameplay/ags_limits_ui.scar | 373 |
| BoostARGB | `AGS_LimitsUI_BoostARGB` | gameplay/ags_limits_ui.scar | 673 |
| BoostRGB | `AGS_LimitsUI_BoostRGB` | gameplay/ags_limits_ui.scar | 654 |
| CreateAndUpdateUI | `AGS_LimitsUI_CreateAndUpdateUI` | gameplay/ags_limits_ui.scar | 740 |
| CreateUI | `AGS_LimitsUI_CreateUI` | gameplay/ags_limits_ui.scar | 748 |
| DeferUpdate | `AGS_LimitsUI_DeferUpdate` | gameplay/ags_limits_ui.scar | 274 |
| EarlyInitializations | `AGS_LimitsUI_EarlyInitializations` | gameplay/ags_limits_ui.scar | 215 |
| GetColors | `AGS_LimitsUI_GetColors` | gameplay/ags_limits_ui.scar | 312 |
| OnBuildItemComplete | `AGS_LimitsUI_OnBuildItemComplete` | gameplay/ags_limits_ui.scar | 294 |
| OnConstructionComplete | `AGS_LimitsUI_OnConstructionComplete` | gameplay/ags_limits_ui.scar | 290 |
| OnEntityKilled | `AGS_LimitsUI_OnEntityKilled` | gameplay/ags_limits_ui.scar | 298 |
| OnGameOver | `AGS_LimitsUI_OnGameOver` | gameplay/ags_limits_ui.scar | 249 |
| OnGameRestore | `AGS_LimitsUI_OnGameRestore` | gameplay/ags_limits_ui.scar | 243 |
| OnPlay | `AGS_LimitsUI_OnPlay` | gameplay/ags_limits_ui.scar | 219 |
| OnPlayerDefeated | `AGS_LimitsUI_OnPlayerDefeated` | gameplay/ags_limits_ui.scar | 262 |
| OnSquadKilled | `AGS_LimitsUI_OnSquadKilled` | gameplay/ags_limits_ui.scar | 302 |
| RecreateUI | `AGS_LimitsUI_RecreateUI` | gameplay/ags_limits_ui.scar | 727 |
| Show | `AGS_LimitsUI_Show` | gameplay/ags_limits_ui.scar | 712 |
| Update | `AGS_LimitsUI_Update` | gameplay/ags_limits_ui.scar | 441 |
| UpdateModuleSettings | `AGS_LimitsUI_UpdateModuleSettings` | gameplay/ags_limits_ui.scar | 202 |

### AGS_MatchUI

- **Registration:** specials/ags_match_ui.scar:44
- **Delegates:** 14

| Phase | Function | File | Line |
|-------|----------|------|------|
| CreateAndUpdateUI | `AGS_MatchUI_CreateAndUpdateUI` | specials/ags_match_ui.scar | 111 |
| CreateDataContext | `AGS_MatchUI_CreateDataContext` | specials/ags_match_ui.scar | 85 |
| CreateUI | `AGS_MatchUI_CreateUI` | specials/ags_match_ui.scar | 116 |
| EarlyInitializations | `AGS_MatchUI_EarlyInitializations` | specials/ags_match_ui.scar | 53 |
| HideDropdown | `AGS_MatchUI_HideDropdown` | specials/ags_match_ui.scar | 372 |
| OnGameOver | `AGS_MatchUI_OnGameOver` | specials/ags_match_ui.scar | 69 |
| OnGameRestore | `AGS_MatchUI_OnGameRestore` | specials/ags_match_ui.scar | 63 |
| OnPlay | `AGS_MatchUI_OnPlay` | specials/ags_match_ui.scar | 58 |
| OnPlayerDefeated | `AGS_MatchUI_OnPlayerDefeated` | specials/ags_match_ui.scar | 74 |
| Show | `AGS_MatchUI_Show` | specials/ags_match_ui.scar | 104 |
| ToggleDropdown | `AGS_MatchUI_ToggleDropdown` | specials/ags_match_ui.scar | 361 |
| ToggleObjectives | `AGS_MatchUI_ToggleObjectives` | specials/ags_match_ui.scar | 378 |
| Update | `AGS_MatchUI_Update` | specials/ags_match_ui.scar | 94 |
| UpdateModuleSettings | `AGS_MatchUI_UpdateModuleSettings` | specials/ags_match_ui.scar | 46 |

### AGS_MedicPopulationCapacity

- **Registration:** gameplay/ags_population_capacity.scar:41
- **Delegates:** 6

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyMaxCapMedicPopulation | `AGS_MedicPopulationCapacity_ApplyMaxCapMedicPopulation` | gameplay/ags_population_capacity.scar | 107 |
| ApplyMinMedicPopulation | `AGS_MedicPopulationCapacity_ApplyMinMedicPopulation` | gameplay/ags_population_capacity.scar | 103 |
| Change | `AGS_MedicPopulationCapacity_Change` | gameplay/ags_population_capacity.scar | 90 |
| PresetFinalize | `AGS_MedicPopulationCapacity_PresetFinalize` | gameplay/ags_population_capacity.scar | 50 |
| SetMinMedicPopulation | `AGS_MedicPopulationCapacity_SetMinMedicPopulation` | gameplay/ags_population_capacity.scar | 97 |
| UpdateModuleSettings | `AGS_MedicPopulationCapacity_UpdateModuleSettings` | gameplay/ags_population_capacity.scar | 43 |

### AGS_NoArsenal

- **Registration:** gameplay/ags_no_dock.scar:68
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| Lock | `AGS_NoArsenal_Lock` | gameplay/ags_no_dock.scar | 160 |
| PresetFinalize | `AGS_NoArsenal_PresetFinalize` | gameplay/ags_no_dock.scar | 77 |
| UpdateModuleSettings | `AGS_NoArsenal_UpdateModuleSettings` | gameplay/ags_no_dock.scar | 70 |

### AGS_NoDock

- **Registration:** gameplay/ags_no_dock.scar:23
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| Lock | `AGS_NoDock_Lock` | gameplay/ags_no_dock.scar | 86 |
| PresetFinalize | `AGS_NoDock_PresetFinalize` | gameplay/ags_no_dock.scar | 33 |
| UpdateModuleSettings | `AGS_NoDock_UpdateModuleSettings` | gameplay/ags_no_dock.scar | 26 |

### AGS_NoSiege

- **Registration:** gameplay/ags_no_dock.scar:53
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| Lock | `AGS_NoSiege_Lock` | gameplay/ags_no_dock.scar | 106 |
| PresetFinalize | `AGS_NoSiege_PresetFinalize` | gameplay/ags_no_dock.scar | 63 |
| UpdateModuleSettings | `AGS_NoSiege_UpdateModuleSettings` | gameplay/ags_no_dock.scar | 56 |

### AGS_NoWall

- **Registration:** gameplay/ags_no_dock.scar:38
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| Lock | `AGS_NoWall_Lock` | gameplay/ags_no_dock.scar | 93 |
| PresetFinalize | `AGS_NoWall_PresetFinalize` | gameplay/ags_no_dock.scar | 48 |
| UpdateModuleSettings | `AGS_NoWall_UpdateModuleSettings` | gameplay/ags_no_dock.scar | 41 |

### AGS_PopulationAutomatic

- **Registration:** gameplay/ags_auto_population.scar:35
- **Delegates:** 7

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyStartCaps | `AGS_PopulationAutomatic_ApplyStartCaps` | gameplay/ags_auto_population.scar | 96 |
| CompensateInnate | `AGS_PopulationAutomatic_CompensateInnate` | gameplay/ags_auto_population.scar | 65 |
| EarlyInitializations | `AGS_PopulationAutomatic_EarlyInitializations` | gameplay/ags_auto_population.scar | 46 |
| NormalizeStartCap | `AGS_PopulationAutomatic_NormalizeStartCap` | gameplay/ags_auto_population.scar | 82 |
| PresetFinalize | `AGS_PopulationAutomatic_PresetFinalize` | gameplay/ags_auto_population.scar | 52 |
| ReconcileCapDrift | `AGS_PopulationAutomatic_ReconcileCapDrift` | gameplay/ags_auto_population.scar | 171 |
| UpdateModuleSettings | `AGS_PopulationAutomatic_UpdateModuleSettings` | gameplay/ags_auto_population.scar | 38 |

### AGS_PopulationCapacity

- **Registration:** gameplay/ags_population_capacity.scar:19
- **Delegates:** 7

| Phase | Function | File | Line |
|-------|----------|------|------|
| AdjustSettings | `AGS_PopulationCapacity_AdjustSettings` | gameplay/ags_population_capacity.scar | 28 |
| ApplyMaxCapPopulation | `AGS_PopulationCapacity_ApplyMaxCapPopulation` | gameplay/ags_population_capacity.scar | 84 |
| ApplyMinPopulation | `AGS_PopulationCapacity_ApplyMinPopulation` | gameplay/ags_population_capacity.scar | 80 |
| Change | `AGS_PopulationCapacity_Change` | gameplay/ags_population_capacity.scar | 60 |
| PresetFinalize | `AGS_PopulationCapacity_PresetFinalize` | gameplay/ags_population_capacity.scar | 35 |
| SetMinPopulation | `AGS_PopulationCapacity_SetMinPopulation` | gameplay/ags_population_capacity.scar | 67 |
| UpdateModuleSettings | `AGS_PopulationCapacity_UpdateModuleSettings` | gameplay/ags_population_capacity.scar | 21 |

### AGS_RevealFowOnElimination

- **Registration:** gameplay/ags_reveal_fow_on_elimination.scar:16
- **Delegates:** 3

| Phase | Function | File | Line |
|-------|----------|------|------|
| OnPlayerDefeated | `AGS_RevealFowOnElimination_OnPlayerDefeated` | gameplay/ags_reveal_fow_on_elimination.scar | 25 |
| Reveal | `AGS_RevealFowOnElimination_Reveal` | gameplay/ags_reveal_fow_on_elimination.scar | 34 |
| UpdateModuleSettings | `AGS_RevealFowOnElimination_UpdateModuleSettings` | gameplay/ags_reveal_fow_on_elimination.scar | 18 |

### AGS_Scattered

- **Registration:** startconditions/ags_start_scattered.scar:21
- **Delegates:** 9

| Phase | Function | File | Line |
|-------|----------|------|------|
| AdjustSettings | `AGS_Scattered_AdjustSettings` | startconditions/ags_start_scattered.scar | 23 |
| CreateSpawn | `AGS_Scattered_CreateSpawn` | startconditions/ags_start_scattered.scar | 97 |
| DestroySpawn | `AGS_Scattered_DestroySpawn` | startconditions/ags_start_scattered.scar | 82 |
| EarlyInitializations | `AGS_Scattered_EarlyInitializations` | startconditions/ags_start_scattered.scar | 37 |
| GetScatterPosition | `AGS_Scattered_GetScatterPosition` | startconditions/ags_start_scattered.scar | 90 |
| OnStarting | `AGS_Scattered_OnStarting` | startconditions/ags_start_scattered.scar | 56 |
| PresetExecute | `AGS_Scattered_PresetExecute` | startconditions/ags_start_scattered.scar | 51 |
| PresetInitialize | `AGS_Scattered_PresetInitialize` | startconditions/ags_start_scattered.scar | 44 |
| UpdateModuleSettings | `AGS_Scattered_UpdateModuleSettings` | startconditions/ags_start_scattered.scar | 30 |

### AGS_SpecialPopulationUI

- **Registration:** gameplay/ags_special_population_ui.scar:32
- **Delegates:** 16

| Phase | Function | File | Line |
|-------|----------|------|------|
| CreateAndUpdateUI | `AGS_SpecialPopulationUI_CreateAndUpdateUI` | gameplay/ags_special_population_ui.scar | 151 |
| CreateDataContext | `AGS_SpecialPopulationUI_CreateDataContext` | gameplay/ags_special_population_ui.scar | 99 |
| CreateUI | `AGS_SpecialPopulationUI_CreateUI` | gameplay/ags_special_population_ui.scar | 156 |
| EarlyInitializations | `AGS_SpecialPopulationUI_EarlyInitializations` | gameplay/ags_special_population_ui.scar | 41 |
| MarginError | `AGS_SpecialPopulationUI_MarginError` | gameplay/ags_special_population_ui.scar | 129 |
| OnBuildItemComplete | `AGS_SpecialPopulationUI_OnBuildItemComplete` | gameplay/ags_special_population_ui.scar | 85 |
| OnConstructionComplete | `AGS_SpecialPopulationUI_OnConstructionComplete` | gameplay/ags_special_population_ui.scar | 82 |
| OnEntityKilled | `AGS_SpecialPopulationUI_OnEntityKilled` | gameplay/ags_special_population_ui.scar | 88 |
| OnGameOver | `AGS_SpecialPopulationUI_OnGameOver` | gameplay/ags_special_population_ui.scar | 62 |
| OnGameRestore | `AGS_SpecialPopulationUI_OnGameRestore` | gameplay/ags_special_population_ui.scar | 56 |
| OnPlay | `AGS_SpecialPopulationUI_OnPlay` | gameplay/ags_special_population_ui.scar | 46 |
| OnPlayerDefeated | `AGS_SpecialPopulationUI_OnPlayerDefeated` | gameplay/ags_special_population_ui.scar | 71 |
| OnSquadKilled | `AGS_SpecialPopulationUI_OnSquadKilled` | gameplay/ags_special_population_ui.scar | 91 |
| Show | `AGS_SpecialPopulationUI_Show` | gameplay/ags_special_population_ui.scar | 144 |
| Update | `AGS_SpecialPopulationUI_Update` | gameplay/ags_special_population_ui.scar | 108 |
| UpdateModuleSettings | `AGS_SpecialPopulationUI_UpdateModuleSettings` | gameplay/ags_special_population_ui.scar | 34 |

### AGS_StartingAge

- **Registration:** gameplay/ags_starting_age.scar:16
- **Delegates:** 4

| Phase | Function | File | Line |
|-------|----------|------|------|
| LateInitializations | `AGS_StartingAge_LateInitializations` | gameplay/ags_starting_age.scar | 25 |
| UpdateModuleSettings | `AGS_StartingAge_UpdateModuleSettings` | gameplay/ags_starting_age.scar | 18 |
| UpgradeAllPlayers | `AGS_StartingAge_UpgradeAllPlayers` | gameplay/ags_starting_age.scar | 34 |
| UpgradePlayer | `AGS_StartingAge_UpgradePlayer` | gameplay/ags_starting_age.scar | 40 |

### AGS_Surrender

- **Registration:** conditions/ags_surrender.scar:21
- **Delegates:** 6

| Phase | Function | File | Line |
|-------|----------|------|------|
| CheckAI | `AGS_Surrender_CheckAI` | conditions/ags_surrender.scar | 94 |
| Notify | `AGS_Surrender_Notify` | conditions/ags_surrender.scar | 84 |
| OnPlay | `AGS_Surrender_OnPlay` | conditions/ags_surrender.scar | 30 |
| OnPlayerDefeated | `AGS_Surrender_OnPlayerDefeated` | conditions/ags_surrender.scar | 53 |
| OnSurrenderMatchRequested | `AGS_Surrender_OnSurrenderMatchRequested` | conditions/ags_surrender.scar | 47 |
| UpdateModuleSettings | `AGS_Surrender_UpdateModuleSettings` | conditions/ags_surrender.scar | 23 |

### AGS_TeamBalance

- **Registration:** gameplay/ags_team_balance.scar:23
- **Delegates:** 10

| Phase | Function | File | Line |
|-------|----------|------|------|
| IncreaseCapPopulation | `AGS_TeamBalance_IncreaseCapPopulation` | gameplay/ags_team_balance.scar | 213 |
| IncreaseMaxCapPopulation | `AGS_TeamBalance_IncreaseMaxCapPopulation` | gameplay/ags_team_balance.scar | 217 |
| OnPlayerDefeated | `AGS_TeamBalance_OnPlayerDefeated` | gameplay/ags_team_balance.scar | 32 |
| UpdateAllLimits | `AGS_TeamBalance_UpdateAllLimits` | gameplay/ags_team_balance.scar | 165 |
| UpdateAutoRates | `AGS_TeamBalance_UpdateAutoRates` | gameplay/ags_team_balance.scar | 191 |
| UpdateModuleSettings | `AGS_TeamBalance_UpdateModuleSettings` | gameplay/ags_team_balance.scar | 25 |
| UpdateTeam | `AGS_TeamBalance_UpdateTeam` | gameplay/ags_team_balance.scar | 41 |
| UpdateTeamMedicPopulation | `AGS_TeamBalance_UpdateTeamMedicPopulation` | gameplay/ags_team_balance.scar | 125 |
| UpdateTeamPopulation | `AGS_TeamBalance_UpdateTeamPopulation` | gameplay/ags_team_balance.scar | 99 |
| UpdateTeamResources | `AGS_TeamBalance_UpdateTeamResources` | gameplay/ags_team_balance.scar | 147 |

### AGS_Teams

- **Registration:** helpers/ags_teams.scar:17
- **Delegates:** 19

| Phase | Function | File | Line |
|-------|----------|------|------|
| AreTeamVictoryEligible | `AGS_Teams_AreTeamVictoryEligible` | helpers/ags_teams.scar | 269 |
| CountAliveAllies | `AGS_Teams_CountAliveAllies` | helpers/ags_teams.scar | 303 |
| CountAliveInGroup | `AGS_Teams_CountAliveInGroup` | helpers/ags_teams.scar | 289 |
| CountAlivePlayers | `AGS_Teams_CountAlivePlayers` | helpers/ags_teams.scar | 299 |
| CreateFFA | `AGS_Teams_CreateFFA` | helpers/ags_teams.scar | 66 |
| CreateInitialTeams | `AGS_Teams_CreateInitialTeams` | helpers/ags_teams.scar | 47 |
| CreateStaticTeams | `AGS_Teams_CreateStaticTeams` | helpers/ags_teams.scar | 78 |
| DoesWinnerGroupExists | `AGS_Teams_DoesWinnerGroupExists` | helpers/ags_teams.scar | 106 |
| EarlyInitializations | `AGS_Teams_EarlyInitializations` | helpers/ags_teams.scar | 19 |
| GetAllCurrentOpponents | `AGS_Teams_GetAllCurrentOpponents` | helpers/ags_teams.scar | 212 |
| GetAllCurrentTeammates | `AGS_Teams_GetAllCurrentTeammates` | helpers/ags_teams.scar | 240 |
| GetAllMutualFriendshipPlayers | `AGS_Teams_GetAllMutualFriendshipPlayers` | helpers/ags_teams.scar | 199 |
| GetDynamicTeamWinners | `AGS_Teams_GetDynamicTeamWinners` | helpers/ags_teams.scar | 158 |
| GetSoloTeamWinner | `AGS_Teams_GetSoloTeamWinner` | helpers/ags_teams.scar | 132 |
| GetStaticTeamAliveMembers | `AGS_Teams_GetStaticTeamAliveMembers` | helpers/ags_teams.scar | 181 |
| GetStaticTeamWinnders | `AGS_Teams_GetStaticTeamWinnders` | helpers/ags_teams.scar | 146 |
| IsTeamAlive | `AGS_Teams_IsTeamAlive` | helpers/ags_teams.scar | 120 |
| IsTeamVictoryEligible | `AGS_Teams_IsTeamVictoryEligible` | helpers/ags_teams.scar | 264 |
| OnPlayerDefeated | `AGS_Teams_OnPlayerDefeated` | helpers/ags_teams.scar | 25 |

### AGS_Testing

- **Registration:** specials/ags_testing.scar:16
- **Delegates:** 6

| Phase | Function | File | Line |
|-------|----------|------|------|
| HasCommandLineOption | `AGS_Testing_HasCommandLineOption` | specials/ags_testing.scar | 49 |
| OnPlay | `AGS_Testing_OnPlay` | specials/ags_testing.scar | 25 |
| RemoveGaia | `AGS_Testing_RemoveGaia` | specials/ags_testing.scar | 35 |
| RemoveUnits | `AGS_Testing_RemoveUnits` | specials/ags_testing.scar | 43 |
| SpawnTest | `AGS_Testing_SpawnTest` | specials/ags_testing.scar | 53 |
| UpdateModuleSettings | `AGS_Testing_UpdateModuleSettings` | specials/ags_testing.scar | 18 |

### AGS_TreeBombardment

- **Registration:** gameplay/ags_tree_bombardment.scar:35
- **Delegates:** 7

| Phase | Function | File | Line |
|-------|----------|------|------|
| DestroyTreeGroup | `AGS_TreeBombardment_DestroyTreeGroup` | gameplay/ags_tree_bombardment.scar | 103 |
| OnExpectedLanding | `AGS_TreeBombardment_OnExpectedLanding` | gameplay/ags_tree_bombardment.scar | 88 |
| OnGameOver | `AGS_TreeBombardment_OnGameOver` | gameplay/ags_tree_bombardment.scar | 50 |
| OnProjectileFired | `AGS_TreeBombardment_OnProjectileFired` | gameplay/ags_tree_bombardment.scar | 60 |
| OnProjectileLanded | `AGS_TreeBombardment_OnProjectileLanded` | gameplay/ags_tree_bombardment.scar | 72 |
| PrepareStart | `AGS_TreeBombardment_PrepareStart` | gameplay/ags_tree_bombardment.scar | 44 |
| UpdateModuleSettings | `AGS_TreeBombardment_UpdateModuleSettings` | gameplay/ags_tree_bombardment.scar | 37 |

### AGS_UnitRates

- **Registration:** gameplay/ags_unit_rates.scar:17
- **Delegates:** 4

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyBonus | `AGS_UnitRates_ApplyBonus` | gameplay/ags_unit_rates.scar | 36 |
| ApplyModifier | `AGS_UnitRates_ApplyModifier` | gameplay/ags_unit_rates.scar | 47 |
| PresetFinalize | `AGS_UnitRates_PresetFinalize` | gameplay/ags_unit_rates.scar | 26 |
| UpdateModuleSettings | `AGS_UnitRates_UpdateModuleSettings` | gameplay/ags_unit_rates.scar | 19 |

### AGS_Utilities

- **Registration:** specials/ags_utilities.scar:64
- **Delegates:** 6

| Phase | Function | File | Line |
|-------|----------|------|------|
| AdjustSettings | `AGS_Utilities_AdjustSettings` | specials/ags_utilities.scar | 73 |
| LateInitializations | `AGS_Utilities_LateInitializations` | specials/ags_utilities.scar | 79 |
| OnPlay | `AGS_Utilities_OnPlay` | specials/ags_utilities.scar | 84 |
| StandardReplay | `AGS_Utilities_StandardReplay` | specials/ags_utilities.scar | 138 |
| StandardReplayCallbacks | `AGS_Utilities_StandardReplayCallbacks` | specials/ags_utilities.scar | 152 |
| UpdateModuleSettings | `AGS_Utilities_UpdateModuleSettings` | specials/ags_utilities.scar | 66 |

### AGS_Wonder

- **Registration:** conditions/ags_wonder.scar:33
- **Delegates:** 38

| Phase | Function | File | Line |
|-------|----------|------|------|
| CleanWonder | `AGS_Wonder_CleanWonder` | conditions/ags_wonder.scar | 412 |
| Construction | `AGS_Wonder_Construction` | conditions/ags_wonder.scar | 176 |
| ConstructionCompleted | `AGS_Wonder_ConstructionCompleted` | conditions/ags_wonder.scar | 209 |
| ConstructionStarted | `AGS_Wonder_ConstructionStarted` | conditions/ags_wonder.scar | 201 |
| CreateBuildObjective | `AGS_Wonder_CreateBuildObjective` | conditions/ags_wonder.scar | 349 |
| CreateTimerNotifications | `AGS_Wonder_CreateTimerNotifications` | conditions/ags_wonder.scar | 390 |
| CreateTimerObjective | `AGS_Wonder_CreateTimerObjective` | conditions/ags_wonder.scar | 303 |
| DeactivateTimers | `AGS_Wonder_DeactivateTimers` | conditions/ags_wonder.scar | 290 |
| Destroyed | `AGS_Wonder_Destroyed` | conditions/ags_wonder.scar | 488 |
| EnableConstruction | `AGS_Wonder_EnableConstruction` | conditions/ags_wonder.scar | 284 |
| FailTimerObjective | `AGS_Wonder_FailTimerObjective` | conditions/ags_wonder.scar | 358 |
| InformNegativeProgressChange | `AGS_Wonder_InformNegativeProgressChange` | conditions/ags_wonder.scar | 467 |
| InitializeWonders | `AGS_Wonder_InitializeWonders` | conditions/ags_wonder.scar | 270 |
| OnConstructionComplete | `AGS_Wonder_OnConstructionComplete` | conditions/ags_wonder.scar | 172 |
| OnConstructionStart | `AGS_Wonder_OnConstructionStart` | conditions/ags_wonder.scar | 168 |
| OnDamageReceived | `AGS_Wonder_OnDamageReceived` | conditions/ags_wonder.scar | 132 |
| OnEntityKilled | `AGS_Wonder_OnEntityKilled` | conditions/ags_wonder.scar | 215 |
| OnGameOver | `AGS_Wonder_OnGameOver` | conditions/ags_wonder.scar | 116 |
| OnObjectiveToggle | `AGS_Wonder_OnObjectiveToggle` | conditions/ags_wonder.scar | 109 |
| OnPlay | `AGS_Wonder_OnPlay` | conditions/ags_wonder.scar | 46 |
| OnPlayerDefeated | `AGS_Wonder_OnPlayerDefeated` | conditions/ags_wonder.scar | 72 |
| OnRelationshipChanged | `AGS_Wonder_OnRelationshipChanged` | conditions/ags_wonder.scar | 82 |
| OnTimerTick | `AGS_Wonder_OnTimerTick` | conditions/ags_wonder.scar | 251 |
| RemoveAllObjectives | `AGS_Wonder_RemoveAllObjectives` | conditions/ags_wonder.scar | 298 |
| RemoveBuildObjective | `AGS_Wonder_RemoveBuildObjective` | conditions/ags_wonder.scar | 354 |
| RemoveTimerObjectives | `AGS_Wonder_RemoveTimerObjectives` | conditions/ags_wonder.scar | 341 |
| ResetTimerObjective | `AGS_Wonder_ResetTimerObjective` | conditions/ags_wonder.scar | 398 |
| StartCountdown | `AGS_Wonder_StartCountdown` | conditions/ags_wonder.scar | 376 |
| TimerProgressNotification | `AGS_Wonder_TimerProgressNotification` | conditions/ags_wonder.scar | 516 |
| TimerUpdate | `AGS_Wonder_TimerUpdate` | conditions/ags_wonder.scar | 503 |
| TreatyEnded | `AGS_Wonder_TreatyEnded` | conditions/ags_wonder.scar | 66 |
| TreatyStarted | `AGS_Wonder_TreatyStarted` | conditions/ags_wonder.scar | 59 |
| TryDeclareWinners | `AGS_Wonder_TryDeclareWinners` | conditions/ags_wonder.scar | 457 |
| UpdateModuleSettings | `AGS_Wonder_UpdateModuleSettings` | conditions/ags_wonder.scar | 35 |
| UpdateTimerObjectives | `AGS_Wonder_UpdateTimerObjectives` | conditions/ags_wonder.scar | 325 |
| UpdateWonderTimer | `AGS_Wonder_UpdateWonderTimer` | conditions/ags_wonder.scar | 334 |
| VictoryTriggered | `AGS_Wonder_VictoryTriggered` | conditions/ags_wonder.scar | 434 |
| WarnEveryone | `AGS_Wonder_WarnEveryone` | conditions/ags_wonder.scar | 367 |

### Annihilation

- **Registration:** cba_annihilation.scar:55
- **Delegates:** 17

| Phase | Function | File | Line |
|-------|----------|------|------|
| CheckAnnihilationCondition | `Annihilation_CheckAnnihilationCondition` | cba_annihilation.scar | 141 |
| CheckVictory | `Annihilation_CheckVictory` | cba_annihilation.scar | 290 |
| DiplomacyEnabled | `Annihilation_DiplomacyEnabled` | cba_annihilation.scar | 64 |
| GetActiveEnemyCount | `Annihilation_GetActiveEnemyCount` | cba_annihilation.scar | 343 |
| IsACapital | `Annihilation_IsACapital` | cba_annihilation.scar | 363 |
| IsALandmark | `Annihilation_IsALandmark` | cba_annihilation.scar | 368 |
| LoserPresentation | `Annihilation_LoserPresentation` | cba_annihilation.scar | 414 |
| OnConstructionComplete | `Annihilation_OnConstructionComplete` | cba_annihilation.scar | 113 |
| OnEntityKilled | `Annihilation_OnEntityKilled` | cba_annihilation.scar | 136 |
| OnGameOver | `Annihilation_OnGameOver` | cba_annihilation.scar | 102 |
| OnInit | `Annihilation_OnInit` | cba_annihilation.scar | 76 |
| OnLandmarkDestroyed | `Annihilation_OnLandmarkDestroyed` | cba_annihilation.scar | 130 |
| OnPlayerDefeated | `Annihilation_OnPlayerDefeated` | cba_annihilation.scar | 268 |
| PlayerCanReceiveTribute | `Annihilation_PlayerCanReceiveTribute` | cba_annihilation.scar | 373 |
| Start | `Annihilation_Start` | cba_annihilation.scar | 92 |
| TributeEnabled | `Annihilation_TributeEnabled` | cba_annihilation.scar | 71 |
| WinnerPresentation | `Annihilation_WinnerPresentation` | cba_annihilation.scar | 396 |

### CBA_AutoAge

- **Registration:** gameplay/cba_auto_age.scar:57
- **Delegates:** 12

| Phase | Function | File | Line |
|-------|----------|------|------|
| ConstructionComplete | `CBA_AutoAge_ConstructionComplete` | gameplay/cba_auto_age.scar | 279 |
| PlayerHasAnyUpgrade | `CBA_AutoAge_PlayerHasAnyUpgrade` | gameplay/cba_auto_age.scar | 80 |
| PresetFinalize | `CBA_AutoAge_PresetFinalize` | gameplay/cba_auto_age.scar | 66 |
| ReconcileSpecialProgress | `CBA_AutoAge_ReconcileSpecialProgress` | gameplay/cba_auto_age.scar | 163 |
| SetBuildCount | `CBA_AutoAge_SetBuildCount` | gameplay/cba_auto_age.scar | 142 |
| SetMaxAge | `CBA_AutoAge_SetMaxAge` | gameplay/cba_auto_age.scar | 356 |
| SetUpgradeAvailabilitySafe | `CBA_AutoAge_SetUpgradeAvailabilitySafe` | gameplay/cba_auto_age.scar | 93 |
| SetupObjective | `CBA_AutoAge_SetupObjective` | gameplay/cba_auto_age.scar | 198 |
| SyncSpecialUpgradeAvailability | `CBA_AutoAge_SyncSpecialUpgradeAvailability` | gameplay/cba_auto_age.scar | 111 |
| UpdateModuleSettings | `CBA_AutoAge_UpdateModuleSettings` | gameplay/cba_auto_age.scar | 59 |
| UpdateTimer | `CBA_AutoAge_UpdateTimer` | gameplay/cba_auto_age.scar | 261 |
| UpgradeComplete | `CBA_AutoAge_UpgradeComplete` | gameplay/cba_auto_age.scar | 183 |

### CBA_Debug

- **Registration:** debug/cba_debug_core.scar:59
- **Delegates:** 2

| Phase | Function | File | Line |
|-------|----------|------|------|
| EarlyInitializations | `CBA_Debug_EarlyInitializations` | debug/cba_debug_core.scar | 73 |
| UpdateModuleSettings | `CBA_Debug_UpdateModuleSettings` | debug/cba_debug_core.scar | 65 |

### CBA_HREBalance

- **Registration:** gameplay/cba_hre_balance.scar:18
- **Delegates:** 4

| Phase | Function | File | Line |
|-------|----------|------|------|
| ApplyModifier | `CBA_HREBalance_ApplyModifier` | gameplay/cba_hre_balance.scar | 67 |
| ApplyPenalty | `CBA_HREBalance_ApplyPenalty` | gameplay/cba_hre_balance.scar | 44 |
| PresetFinalize | `CBA_HREBalance_PresetFinalize` | gameplay/cba_hre_balance.scar | 28 |
| UpdateModuleSettings | `CBA_HREBalance_UpdateModuleSettings` | gameplay/cba_hre_balance.scar | 20 |

### CBA_Options

- **Registration:** gameplay/cba_options.scar:11
- **Delegates:** 84

| Phase | Function | File | Line |
|-------|----------|------|------|
| AddScuttle_ConstructionComplete | `CBA_Options_AddScuttle_ConstructionComplete` | gameplay/cba_options.scar | 797 |
| BuildingLimit_ConstructionCancelled | `CBA_Options_BuildingLimit_ConstructionCancelled` | gameplay/cba_options.scar | 460 |
| BuildingLimit_ConstructionStart | `CBA_Options_BuildingLimit_ConstructionStart` | gameplay/cba_options.scar | 338 |
| BuildingLimit_EnforceExcess | `CBA_Options_BuildingLimit_EnforceExcess` | gameplay/cba_options.scar | 1765 |
| BuildingLimit_OnEntityKilled | `CBA_Options_BuildingLimit_OnEntityKilled` | gameplay/cba_options.scar | 573 |
| BuildingLimit_RecountPlayer | `CBA_Options_BuildingLimit_RecountPlayer` | gameplay/cba_options.scar | 1696 |
| BuildingLimit_SetupObjective | `CBA_Options_BuildingLimit_SetupObjective` | gameplay/cba_options.scar | 237 |
| DarkAge_Unlocks | `CBA_Options_DarkAge_Unlocks` | gameplay/cba_options.scar | 816 |
| EnforcePopulationCap | `CBA_Options_EnforcePopulationCap` | gameplay/cba_options.scar | 1824 |
| EnforcePostTransfer | `CBA_Options_EnforcePostTransfer` | gameplay/cba_options.scar | 1878 |
| EnforcePostTransfer_Enforce | `CBA_Options_EnforcePostTransfer_Enforce` | gameplay/cba_options.scar | 1915 |
| EnforcePostTransfer_Recount | `CBA_Options_EnforcePostTransfer_Recount` | gameplay/cba_options.scar | 1906 |
| EnforcePostTransfer_UI | `CBA_Options_EnforcePostTransfer_UI` | gameplay/cba_options.scar | 1933 |
| FieldConstruct_Gate | `CBA_Options_FieldConstruct_Gate` | gameplay/cba_options.scar | 2048 |
| GetPlayerOutpostLimit | `CBA_Options_GetPlayerOutpostLimit` | gameplay/cba_options.scar | 197 |
| GetPlayerProdLimit | `CBA_Options_GetPlayerProdLimit` | gameplay/cba_options.scar | 165 |
| GetPlayerRamLimit | `CBA_Options_GetPlayerRamLimit` | gameplay/cba_options.scar | 187 |
| GetPlayerSiegeLimit | `CBA_Options_GetPlayerSiegeLimit` | gameplay/cba_options.scar | 182 |
| GetPlayerSiegeTowerLimit | `CBA_Options_GetPlayerSiegeTowerLimit` | gameplay/cba_options.scar | 192 |
| GetPlayerWorkshopLimit | `CBA_Options_GetPlayerWorkshopLimit` | gameplay/cba_options.scar | 177 |
| GetRamLimitMax | `CBA_Options_GetRamLimitMax` | gameplay/cba_options.scar | 2268 |
| GetRamWeight | `CBA_Options_GetRamWeight` | gameplay/cba_options.scar | 2715 |
| GetRamWeightEntity | `CBA_Options_GetRamWeightEntity` | gameplay/cba_options.scar | 2729 |
| GetRamWeightSBP | `CBA_Options_GetRamWeightSBP` | gameplay/cba_options.scar | 2722 |
| GetSiegeTowerLimitMax | `CBA_Options_GetSiegeTowerLimitMax` | gameplay/cba_options.scar | 2272 |
| GetSiegeWeaponBPMaps | `CBA_Options_GetSiegeWeaponBPMaps` | gameplay/cba_options.scar | 2511 |
| GetSiegeWeaponPointsEBP | `CBA_Options_GetSiegeWeaponPointsEBP` | gameplay/cba_options.scar | 2648 |
| GetSiegeWeaponPointsEntity | `CBA_Options_GetSiegeWeaponPointsEntity` | gameplay/cba_options.scar | 2680 |
| GetSiegeWeaponPointsSBP | `CBA_Options_GetSiegeWeaponPointsSBP` | gameplay/cba_options.scar | 2612 |
| GetWorkshopLimit | `CBA_Options_GetWorkshopLimit` | gameplay/cba_options.scar | 170 |
| HasSiegeEngineers | `CBA_Options_HasSiegeEngineers` | gameplay/cba_options.scar | 1617 |
| IsRamTowerEBP | `CBA_Options_IsRamTowerEBP` | gameplay/cba_options.scar | 2479 |
| IsRamTowerEntity | `CBA_Options_IsRamTowerEntity` | gameplay/cba_options.scar | 2493 |
| IsRamTowerSBP | `CBA_Options_IsRamTowerSBP` | gameplay/cba_options.scar | 2453 |
| IsRamTowerSquad | `CBA_Options_IsRamTowerSquad` | gameplay/cba_options.scar | 2467 |
| IsSiegeWeaponBPMatch_EBP | `CBA_Options_IsSiegeWeaponBPMatch_EBP` | gameplay/cba_options.scar | 2589 |
| IsSiegeWeaponBPMatch_SBP | `CBA_Options_IsSiegeWeaponBPMatch_SBP` | gameplay/cba_options.scar | 2598 |
| OutpostRestrictions | `CBA_Options_OutpostRestrictions` | gameplay/cba_options.scar | 894 |
| PresetFinalize | `CBA_Options_PresetFinalize` | gameplay/cba_options.scar | 53 |
| RamLimit_ApplyThreshold | `CBA_Options_RamLimit_ApplyThreshold` | gameplay/cba_options.scar | 2196 |
| RamLimit_Disable | `CBA_Options_RamLimit_Disable` | gameplay/cba_options.scar | 2141 |
| RamLimit_EnforceSpawnCap | `CBA_Options_RamLimit_EnforceSpawnCap` | gameplay/cba_options.scar | 2321 |
| RamLimit_GetQueuedCount | `CBA_Options_RamLimit_GetQueuedCount` | gameplay/cba_options.scar | 2940 |
| RamLimit_Recount | `CBA_Options_RamLimit_Recount` | gameplay/cba_options.scar | 2771 |
| RamLimit_RollbackExcessScaffolds | `CBA_Options_RamLimit_RollbackExcessScaffolds` | gameplay/cba_options.scar | 2736 |
| RamLimit_TrimQueue | `CBA_Options_RamLimit_TrimQueue` | gameplay/cba_options.scar | 2966 |
| RamTowerOnly_Disable | `CBA_Options_RamTowerOnly_Disable` | gameplay/cba_options.scar | 2170 |
| RevalidateAll | `CBA_Options_RevalidateAll` | gameplay/cba_options.scar | 1944 |
| RevalidateAllPlayers | `CBA_Options_RevalidateAllPlayers` | gameplay/cba_options.scar | 1960 |
| ShouldLogSiegeStandard | `CBA_Options_ShouldLogSiegeStandard` | gameplay/cba_options.scar | 20 |
| ShouldLogSiegeStateChange | `CBA_Options_ShouldLogSiegeStateChange` | gameplay/cba_options.scar | 34 |
| ShouldLogSiegeVerbose | `CBA_Options_ShouldLogSiegeVerbose` | gameplay/cba_options.scar | 24 |
| SiegeLimit_ApplyAllThresholds | `CBA_Options_SiegeLimit_ApplyAllThresholds` | gameplay/cba_options.scar | 912 |
| SiegeLimit_ApplyThreshold | `CBA_Options_SiegeLimit_ApplyThreshold` | gameplay/cba_options.scar | 1627 |
| SiegeLimit_BuildItemComplete | `CBA_Options_SiegeLimit_BuildItemComplete` | cba.scar | 1409 |
| SiegeLimit_Cancel_1 | `CBA_Options_SiegeLimit_Cancel_1` | gameplay/cba_options.scar | 736 |
| SiegeLimit_Cancel_2 | `CBA_Options_SiegeLimit_Cancel_2` | gameplay/cba_options.scar | 756 |
| SiegeLimit_Cancel_3 | `CBA_Options_SiegeLimit_Cancel_3` | gameplay/cba_options.scar | 776 |
| SiegeLimit_Cancel_filter | `CBA_Options_SiegeLimit_Cancel_filter` | cba.scar | 1364 |
| SiegeLimit_ConstructionCancelled | `CBA_Options_SiegeLimit_ConstructionCancelled` | gameplay/cba_options.scar | 1140 |
| SiegeLimit_ConstructionComplete | `CBA_Options_SiegeLimit_ConstructionComplete` | gameplay/cba_options.scar | 1200 |
| SiegeLimit_ConstructionStart | `CBA_Options_SiegeLimit_ConstructionStart` | gameplay/cba_options.scar | 931 |
| SiegeLimit_Disable | `CBA_Options_SiegeLimit_Disable` | cba.scar | 1177 |
| SiegeLimit_EnforceSpawnCap | `CBA_Options_SiegeLimit_EnforceSpawnCap` | gameplay/cba_options.scar | 2371 |
| SiegeLimit_EntityKilled | `CBA_Options_SiegeLimit_EntityKilled` | gameplay/cba_options.scar | 1260 |
| SiegeLimit_GetGateTotals | `CBA_Options_SiegeLimit_GetGateTotals` | gameplay/cba_options.scar | 3064 |
| SiegeLimit_GetQueuedPoints | `CBA_Options_SiegeLimit_GetQueuedPoints` | gameplay/cba_options.scar | 3022 |
| SiegeLimit_Reconcile | `CBA_Options_SiegeLimit_Reconcile` | gameplay/cba_options.scar | 1971 |
| SiegeLimit_Recount | `CBA_Options_SiegeLimit_Recount` | gameplay/cba_options.scar | 1530 |
| SiegeLimit_RecountAll | `CBA_Options_SiegeLimit_RecountAll` | gameplay/cba_options.scar | 1349 |
| SiegeLimit_RollbackExcessScaffolds | `CBA_Options_SiegeLimit_RollbackExcessScaffolds` | gameplay/cba_options.scar | 2419 |
| SiegeLimit_RunDeferredRecheck | `CBA_Options_SiegeLimit_RunDeferredRecheck` | gameplay/cba_options.scar | 1068 |
| SiegeLimit_ScheduleDeferredRecheck | `CBA_Options_SiegeLimit_ScheduleDeferredRecheck` | gameplay/cba_options.scar | 1055 |
| SiegeLimit_SquadKilled | `CBA_Options_SiegeLimit_SquadKilled` | cba.scar | 1529 |
| SiegeLimit_TrimQueue | `CBA_Options_SiegeLimit_TrimQueue` | gameplay/cba_options.scar | 3035 |
| SiegeTowerLimit_ApplyThreshold | `CBA_Options_SiegeTowerLimit_ApplyThreshold` | gameplay/cba_options.scar | 2236 |
| SiegeTowerLimit_Disable | `CBA_Options_SiegeTowerLimit_Disable` | gameplay/cba_options.scar | 2178 |
| SiegeTowerLimit_GetQueuedCount | `CBA_Options_SiegeTowerLimit_GetQueuedCount` | gameplay/cba_options.scar | 2955 |
| SiegeTowerLimit_Recount | `CBA_Options_SiegeTowerLimit_Recount` | gameplay/cba_options.scar | 2838 |
| SiegeTowerLimit_TrimQueue | `CBA_Options_SiegeTowerLimit_TrimQueue` | gameplay/cba_options.scar | 2997 |
| UpdateModuleSettings | `CBA_Options_UpdateModuleSettings` | gameplay/cba_options.scar | 45 |
| ValidateEnforcement | `CBA_Options_ValidateEnforcement` | gameplay/cba_options.scar | 2280 |
| VillagerSpawner | `CBA_Options_VillagerSpawner` | gameplay/cba_options.scar | 831 |
| WorkshopLimit_ApplyThreshold | `CBA_Options_WorkshopLimit_ApplyThreshold` | gameplay/cba_options.scar | 203 |

### CBA_REWARDS_CBAULE

- **Registration:** rewards.scar:24
- **Delegates:** 0

### Mod

- **Registration:** cba.scar:316
- **Delegates:** 27

| Phase | Function | File | Line |
|-------|----------|------|------|
| ConfigureKeepAsCapitalAgeProducer | `Mod_ConfigureKeepAsCapitalAgeProducer` | cba.scar | 816 |
| EliminatePlayerUnits | `Mod_EliminatePlayerUnits` | cba.scar | 3536 |
| EnsureKeepAsCapital | `Mod_EnsureKeepAsCapital` | cba.scar | 969 |
| FindBestAlly | `Mod_FindBestAlly` | cba.scar | 2917 |
| FindKeep | `Mod_FindKeep` | cba.scar | 773 |
| LoserPresentation | `Mod_LoserPresentation` | cba.scar | 1139 |
| OnEntityKilled | `Mod_OnEntityKilled` | cba.scar | 636 |
| OnGameOver | `Mod_OnGameOver` | cba.scar | 560 |
| OnGameSetup | `Mod_OnGameSetup` | onslaught.scar | 114 |
| OnGameSetup | `Mod_OnGameSetup` | cba.scar | 323 |
| OnInit | `Mod_OnInit` | onslaught.scar | 137 |
| OnInit | `Mod_OnInit` | cba.scar | 375 |
| PostInit | `Mod_PostInit` | cba.scar | 408 |
| PostInit | `Mod_PostInit` | onslaught.scar | 174 |
| PreInit | `Mod_PreInit` | cba.scar | 367 |
| PreInit | `Mod_PreInit` | onslaught.scar | 129 |
| Preset | `Mod_Preset` | onslaught.scar | 180 |
| Preset | `Mod_Preset` | cba.scar | 414 |
| PreStart | `Mod_PreStart` | onslaught.scar | 188 |
| PreStart | `Mod_PreStart` | cba.scar | 422 |
| RemoveGaia | `Mod_RemoveGaia` | cba.scar | 683 |
| SetFOW | `Mod_SetFOW` | cba.scar | 721 |
| setStartingResources | `Mod_setStartingResources` | cba.scar | 695 |
| SetupObjective | `Mod_SetupObjective` | cba.scar | 732 |
| Start | `Mod_Start` | cba.scar | 428 |
| Start | `Mod_Start` | onslaught.scar | 194 |
| WinnerPresentation | `Mod_WinnerPresentation` | cba.scar | 1107 |

### Nomad

- **Registration:** startconditions/nomad_start.scar:37
- **Delegates:** 9

| Phase | Function | File | Line |
|-------|----------|------|------|
| DestroySpawns | `Nomad_DestroySpawns` | startconditions/nomad_start.scar | 113 |
| intMax | `Nomad_intMax` | startconditions/nomad_start.scar | 182 |
| OnConstructionComplete | `Nomad_OnConstructionComplete` | startconditions/nomad_start.scar | 79 |
| OnGameSetup | `Nomad_OnGameSetup` | startconditions/nomad_start.scar | 19 |
| PresetFinalize | `Nomad_PresetFinalize` | startconditions/nomad_start.scar | 45 |
| SetupSpawns | `Nomad_SetupSpawns` | startconditions/nomad_start.scar | 130 |
| Start | `Nomad_Start` | startconditions/nomad_start.scar | 61 |
| UnlockVillagers | `Nomad_UnlockVillagers` | startconditions/nomad_start.scar | 72 |
| UpdateModuleSettings | `Nomad_UpdateModuleSettings` | startconditions/nomad_start.scar | 40 |

### ObserverUI

- **Registration:** observerui/observerui.scar:45
- **Delegates:** 2

| Phase | Function | File | Line |
|-------|----------|------|------|
| GameStateTracking_Tribute_OnTributeSent | `ObserverUI_GameStateTracking_Tribute_OnTributeSent` | observerui/gamestatetracking/ontributesent.scar | 10 |
| OnInit | `ObserverUI_OnInit` | observerui/observerui.scar | 47 |

### ObserverUI_GameStateTracking_Tribute

- **Registration:** observerui/gamestatetracking/ontributesent.scar:1
- **Delegates:** 1

| Phase | Function | File | Line |
|-------|----------|------|------|
| OnTributeSent | `ObserverUI_GameStateTracking_Tribute_OnTributeSent` | observerui/gamestatetracking/ontributesent.scar | 10 |

### PlayerUI

- **Registration:** playerui/playerui.scar:50
- **Delegates:** 100

| Phase | Function | File | Line |
|-------|----------|------|------|
| AdaptIconPathForXaml | `PlayerUI_AdaptIconPathForXaml` | playerui/playerui_updateui.scar | 443 |
| Animate_ApplyDisplayValues | `PlayerUI_Animate_ApplyDisplayValues` | playerui/playerui_animate.scar | 1023 |
| Animate_ApplyEliminationTransitionFinalVisual | `PlayerUI_Animate_ApplyEliminationTransitionFinalVisual` | playerui/playerui_animate.scar | 1563 |
| Animate_ClearEliminationAnim | `PlayerUI_Animate_ClearEliminationAnim` | playerui/playerui_animate.scar | 1672 |
| Animate_ClearEliminationGlow | `PlayerUI_Animate_ClearEliminationGlow` | playerui/playerui_animate.scar | 1839 |
| Animate_ClearEliminationReveal | `PlayerUI_Animate_ClearEliminationReveal` | playerui/playerui_animate.scar | 1757 |
| Animate_Debug_PrintEliminationDiag | `PlayerUI_Animate_Debug_PrintEliminationDiag` | playerui/playerui_animate.scar | 252 |
| Animate_Debug_ResetEliminationDiag | `PlayerUI_Animate_Debug_ResetEliminationDiag` | playerui/playerui_animate.scar | 240 |
| Animate_Debug_RetriggerElimFade | `PlayerUI_Animate_Debug_RetriggerElimFade` | playerui/playerui_animate.scar | 271 |
| Animate_EliminationGlow | `PlayerUI_Animate_EliminationGlow` | playerui/playerui_animate.scar | 1780 |
| Animate_EliminationReveal | `PlayerUI_Animate_EliminationReveal` | playerui/playerui_animate.scar | 1697 |
| Animate_EliminationTransition | `PlayerUI_Animate_EliminationTransition` | playerui/playerui_animate.scar | 1582 |
| Animate_GetDecay | `PlayerUI_Animate_GetDecay` | playerui/playerui_animate.scar | 710 |
| Animate_GetDisplay | `PlayerUI_Animate_GetDisplay` | playerui/playerui_animate.scar | 377 |
| Animate_GetEliminationGlowState | `PlayerUI_Animate_GetEliminationGlowState` | playerui/playerui_animate.scar | 1809 |
| Animate_GetEliminationLastProgress | `PlayerUI_Animate_GetEliminationLastProgress` | playerui/playerui_animate.scar | 263 |
| Animate_GetEliminationRevealState | `PlayerUI_Animate_GetEliminationRevealState` | playerui/playerui_animate.scar | 1727 |
| Animate_GetEliminationState | `PlayerUI_Animate_GetEliminationState` | playerui/playerui_animate.scar | 1625 |
| Animate_GetPosition | `PlayerUI_Animate_GetPosition` | playerui/playerui_animate.scar | 673 |
| Animate_HasArrived | `PlayerUI_Animate_HasArrived` | playerui/playerui_animate.scar | 682 |
| Animate_Init | `PlayerUI_Animate_Init` | playerui/playerui_animate.scar | 319 |
| Animate_IsEliminationGlowActive | `PlayerUI_Animate_IsEliminationGlowActive` | playerui/playerui_animate.scar | 1768 |
| Animate_IsEliminationRevealActive | `PlayerUI_Animate_IsEliminationRevealActive` | playerui/playerui_animate.scar | 1683 |
| Animate_IsEliminationTransitionActive | `PlayerUI_Animate_IsEliminationTransitionActive` | playerui/playerui_animate.scar | 1550 |
| Animate_IsTransitioning | `PlayerUI_Animate_IsTransitioning` | playerui/playerui_animate.scar | 692 |
| Animate_Reset | `PlayerUI_Animate_Reset` | playerui/playerui_animate.scar | 1847 |
| Animate_SetPosition | `PlayerUI_Animate_SetPosition` | playerui/playerui_animate.scar | 646 |
| Animate_SetPositionTarget | `PlayerUI_Animate_SetPositionTarget` | playerui/playerui_animate.scar | 657 |
| Animate_SetTarget | `PlayerUI_Animate_SetTarget` | playerui/playerui_animate.scar | 339 |
| Animate_TriggerDecay | `PlayerUI_Animate_TriggerDecay` | playerui/playerui_animate.scar | 699 |
| Animate_TriggerScorePulse | `PlayerUI_Animate_TriggerScorePulse` | playerui/playerui_animate.scar | 719 |
| ApplyDataContext | `PlayerUI_ApplyDataContext` | playerui/playerui_updateui.scar | 981 |
| BuildPlaybackMilestone | `PlayerUI_BuildPlaybackMilestone` | playerui/playerui_updateui.scar | 1529 |
| BuildRewardPreview | `PlayerUI_BuildRewardPreview` | playerui/playerui_updateui.scar | 1399 |
| BuildUnitsUiTable | `PlayerUI_BuildUnitsUiTable` | playerui/playerui_updateui.scar | 1145 |
| CompareUnitCount | `PlayerUI_CompareUnitCount` | playerui/playerui_updateui.scar | 1179 |
| Debug_AuditPredictionVisibility | `PlayerUI_Debug_AuditPredictionVisibility` | playerui/playerui_ranking.scar | 1326 |
| Debug_DemoPredictionStates | `PlayerUI_Debug_DemoPredictionStates` | playerui/playerui_ranking.scar | 1566 |
| Debug_FeatureStatus | `PlayerUI_Debug_FeatureStatus` | debug/cba_debug_playerui_anim.scar | 141 |
| Debug_ForcePredictionCase | `PlayerUI_Debug_ForcePredictionCase` | playerui/playerui_ranking.scar | 1430 |
| Debug_ForcePredictionState | `PlayerUI_Debug_ForcePredictionState` | playerui/playerui_ranking.scar | 1171 |
| Debug_ForceWaitAudit | `PlayerUI_Debug_ForceWaitAudit` | playerui/playerui_ranking.scar | 1788 |
| Debug_PredictionDiagnostics | `PlayerUI_Debug_PredictionDiagnostics` | playerui/playerui_ranking.scar | 1839 |
| Debug_PredictionSnapshot | `PlayerUI_Debug_PredictionSnapshot` | playerui/playerui_ranking.scar | 1677 |
| Debug_PrintEliminationSnapshot | `PlayerUI_Debug_PrintEliminationSnapshot` | playerui/playerui_updateui.scar | 214 |
| Debug_PrintFullSnapshot | `PlayerUI_Debug_PrintFullSnapshot` | playerui/playerui_updateui.scar | 267 |
| Debug_SystemStatus | `PlayerUI_Debug_SystemStatus` | playerui/playerui_ranking.scar | 1989 |
| Debug_TestContestedCollapse | `PlayerUI_Debug_TestContestedCollapse` | playerui/playerui_ranking.scar | 2200 |
| Debug_TestSettingsMatrix | `PlayerUI_Debug_TestSettingsMatrix` | playerui/playerui_ranking.scar | 2307 |
| Debug_TestStability | `PlayerUI_Debug_TestStability` | playerui/playerui_ranking.scar | 2092 |
| Debug_TogglePresetFull | `PlayerUI_Debug_TogglePresetFull` | debug/cba_debug_playerui_anim.scar | 145 |
| Debug_ToggleProbe | `PlayerUI_Debug_ToggleProbe` | playerui/playerui_updateui.scar | 1865 |
| DismissErrors | `PlayerUI_DismissErrors` | playerui/playerui_updateui.scar | 1068 |
| GetElapsedTimeDisplay | `PlayerUI_GetElapsedTimeDisplay` | playerui/playerui_updateui.scar | 873 |
| GetIconNameFromSquadBlueprint | `PlayerUI_GetIconNameFromSquadBlueprint` | playerui/playerui_updateui.scar | 1076 |
| GetIconNameFromUpgradeBlueprint | `PlayerUI_GetIconNameFromUpgradeBlueprint` | playerui/playerui_updateui.scar | 1080 |
| GetLimitColors | `PlayerUI_GetLimitColors` | playerui/playerui_updateui.scar | 1223 |
| GetMaxPopulationDisplay | `PlayerUI_GetMaxPopulationDisplay` | playerui/playerui_updateui.scar | 1011 |
| GetNextRewardIcon | `PlayerUI_GetNextRewardIcon` | playerui/playerui_updateui.scar | 1388 |
| GetNextRewardTitle | `PlayerUI_GetNextRewardTitle` | playerui/playerui_updateui.scar | 1359 |
| GetNormalizedRewardTitle | `PlayerUI_GetNormalizedRewardTitle` | playerui/playerui_updateui.scar | 1314 |
| GetPopulationVsMaximumPopulation | `PlayerUI_GetPopulationVsMaximumPopulation` | playerui/playerui_updateui.scar | 1001 |
| GetQueuedStuff | `PlayerUI_GetQueuedStuff` | playerui/playerui_updateui.scar | 1112 |
| GetRewardProgressBounds | `PlayerUI_GetRewardProgressBounds` | playerui/playerui_updateui.scar | 1468 |
| GetUnits | `PlayerUI_GetUnits` | playerui/playerui_updateui.scar | 1092 |
| HashSetToArray | `PlayerUI_HashSetToArray` | playerui/playerui_updateui.scar | 1137 |
| HasMilitaryIcon | `PlayerUI_HasMilitaryIcon` | playerui/playerui_updateui.scar | 1084 |
| InitializeDataContext | `PlayerUI_InitializeDataContext` | playerui/playerui_updateui.scar | 510 |
| OnInit | `PlayerUI_OnInit` | playerui/playerui.scar | 56 |
| PresetFinalize | `PlayerUI_PresetFinalize` | playerui/playerui.scar | 190 |
| Ranking_ApplyAnimatedFields | `PlayerUI_Ranking_ApplyAnimatedFields` | playerui/playerui_ranking.scar | 933 |
| Ranking_DebugForceSwap | `PlayerUI_Ranking_DebugForceSwap` | playerui/playerui_ranking.scar | 1117 |
| Ranking_DebugPrintState | `PlayerUI_Ranking_DebugPrintState` | playerui/playerui_ranking.scar | 1597 |
| Ranking_DebugSetScore | `PlayerUI_Ranking_DebugSetScore` | playerui/playerui_ranking.scar | 1648 |
| Ranking_DebugTestPredictions | `PlayerUI_Ranking_DebugTestPredictions` | playerui/playerui_ranking.scar | 1871 |
| Ranking_Init | `PlayerUI_Ranking_Init` | playerui/playerui_ranking.scar | 96 |
| Ranking_Reset | `PlayerUI_Ranking_Reset` | playerui/playerui_ranking.scar | 1104 |
| Ranking_Update | `PlayerUI_Ranking_Update` | playerui/playerui_ranking.scar | 169 |
| ReconstructCrossedThresholds | `PlayerUI_ReconstructCrossedThresholds` | playerui/playerui_updateui.scar | 1507 |
| ResetEliminationPresentationState | `PlayerUI_ResetEliminationPresentationState` | playerui/playerui_updateui.scar | 18 |
| RewardPlayback_AdvanceQueue | `PlayerUI_RewardPlayback_AdvanceQueue` | playerui/playerui_updateui.scar | 1733 |
| SetObjectivesVisible | `PlayerUI_SetObjectivesVisible` | playerui/playerui_updateui.scar | 1789 |
| SplitByIsMilitary | `PlayerUI_SplitByIsMilitary` | playerui/playerui_updateui.scar | 1166 |
| SwapResourceWithIncomePerMinute | `PlayerUI_SwapResourceWithIncomePerMinute` | playerui/playerui_updateui.scar | 1971 |
| Toggle | `PlayerUI_Toggle` | playerui/playerui_updateui.scar | 1900 |
| Toggle_TrySetObjectivesVisible | `PlayerUI_Toggle_TrySetObjectivesVisible` | playerui/playerui_updateui.scar | 1849 |
| Toggle_TrySetProperty | `PlayerUI_Toggle_TrySetProperty` | playerui/playerui_updateui.scar | 1840 |
| ToggleTrace | `PlayerUI_ToggleTrace` | playerui/playerui_updateui.scar | 1858 |
| TrySetObjectiveVisible | `PlayerUI_TrySetObjectiveVisible` | playerui/playerui_updateui.scar | 1778 |
| UpdateCivSpecifics | `PlayerUI_UpdateCivSpecifics` | playerui/playerui_updateui.scar | 1057 |
| UpdateDataContext | `PlayerUI_UpdateDataContext` | playerui/playerui_updateui.scar | 629 |
| UpdateEliminationPresentationForIndex | `PlayerUI_UpdateEliminationPresentationForIndex` | playerui/playerui_updateui.scar | 351 |
| UpdateIsUpping | `PlayerUI_UpdateIsUpping` | playerui/playerui_updateui.scar | 1048 |
| UpdateLimits | `PlayerUI_UpdateLimits` | playerui/playerui_updateui.scar | 1237 |
| UpdatePopulationComposition | `PlayerUI_UpdatePopulationComposition` | playerui/playerui_updateui.scar | 1020 |
| UpdateRelics | `PlayerUI_UpdateRelics` | playerui/playerui_updateui.scar | 1040 |
| UpdateResources | `PlayerUI_UpdateResources` | playerui/playerui_updateui.scar | 950 |
| UpdateRewardProgress | `PlayerUI_UpdateRewardProgress` | playerui/playerui_updateui.scar | 1587 |
| UpdateTeamSummaries | `PlayerUI_UpdateTeamSummaries` | playerui/playerui_updateui.scar | 892 |
| UpdateUnitsAndQueuedStuff | `PlayerUI_UpdateUnitsAndQueuedStuff` | playerui/playerui_updateui.scar | 1186 |

### Wonder

- **Registration:** wonder.scar:89
- **Delegates:** 21

| Phase | Function | File | Line |
|-------|----------|------|------|
| AddObjective1 | `Wonder_AddObjective1` | wonder.scar | 744 |
| AddObjective2 | `Wonder_AddObjective2` | wonder.scar | 767 |
| CheckVictory | `Wonder_CheckVictory` | wonder.scar | 702 |
| CreateEventCue | `Wonder_CreateEventCue` | wonder.scar | 838 |
| DiplomacyEnabled | `Wonder_DiplomacyEnabled` | wonder.scar | 96 |
| LoserPresentation | `Wonder_LoserPresentation` | wonder.scar | 892 |
| OnConstructionComplete | `Wonder_OnConstructionComplete` | wonder.scar | 254 |
| OnConstructionStart | `Wonder_OnConstructionStart` | wonder.scar | 200 |
| OnDamageReceived | `Wonder_OnDamageReceived` | wonder.scar | 449 |
| OnEntityKilled | `Wonder_OnEntityKilled` | wonder.scar | 275 |
| OnGameOver | `Wonder_OnGameOver` | wonder.scar | 179 |
| OnInit | `Wonder_OnInit` | wonder.scar | 102 |
| OnLocalPlayerChanged | `Wonder_OnLocalPlayerChanged` | wonder.scar | 520 |
| OnPlayerDefeated | `Wonder_OnPlayerDefeated` | wonder.scar | 166 |
| RemoveObjective2 | `Wonder_RemoveObjective2` | wonder.scar | 796 |
| RemoveObjectives | `Wonder_RemoveObjectives` | wonder.scar | 826 |
| Start | `Wonder_Start` | wonder.scar | 122 |
| Update | `Wonder_Update` | wonder.scar | 531 |
| UpdatePlayerStats | `Wonder_UpdatePlayerStats` | wonder.scar | 148 |
| UpdatePlayerStats | `Wonder_UpdatePlayerStats` | specials/ags_utilities.scar | 114 |
| WinnerPresentation | `Wonder_WinnerPresentation` | wonder.scar | 856 |

