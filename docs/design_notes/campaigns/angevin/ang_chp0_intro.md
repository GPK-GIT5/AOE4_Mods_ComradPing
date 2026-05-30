# Angevin Chapter 0: Intro

## OVERVIEW

Angevin Chapter 0 is a comprehensive tutorial mission where the player controls the English (player1) against the French (player2) with a neutral ally (player3). The mission walks the player through the full RTS learning curve: gathering resources, building an economy (Dark Age), exploring and mining gold, aging up to Feudal, training military units (spearmen, horsemen, longbowmen), and destroying three sequential French encampments (cavalry, archery, infantry). Nearly all buildings, units, and abilities start ITEM_REMOVED and are progressively unlocked as objectives complete. Build times are halved via `ChangeBuildTimes()`, and an extensive training-hint system (`training_missionzero.scar`) provides interactive step-by-step UI overlays for every mechanic. The mission ends when the player constructs a Castle Age landmark (White Tower).

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp0_intro.scar` | core | Main mission file: player setup, restrictions, recipe, variable init, construction watchers, cheat functions |
| `obj_economy_darkage.scar` | objectives | Dark Age economy chain: gather food, produce villagers, build mill/lumber camp/houses/farms |
| `obj_explore_darkage.scar` | objectives | Dark Age exploration chain: produce scout, find gold, build mining camp, gather gold |
| `obj_progress_feudalage.scar` | objectives | Feudal Age progression: age-up monitoring, landmark construction/cancellation handling |
| `obj_military_feudal.scar` | objectives | Feudal military intro: build barracks, produce 10 spearmen, destroy palisade |
| `obj_attackenemycavalry.scar` | objectives | Cavalry encampment attack: learn attack-move, kill 6 horsemen, destroy stables |
| `obj_attack_enemyarchery.scar` | objectives | Archery encampment attack: build 2 stables, produce 15 horsemen, kill archers, destroy buildings |
| `obj_attack_enemyinfantry.scar` | objectives | Infantry encampment attack: build 3 archery ranges, produce 20 longbowmen, cliff setup, kill spearmen |
| `obj_progress_castleage.scar` | objectives | Castle Age progression: build White Tower landmark to complete mission |
| `obj_tip_darkage.scar` | objectives | Dark Age tip objectives (gather food, build mill, houses, farms, mining camp, age up) |
| `obj_tip_feudal.scar` | objectives | Feudal Age tip objectives (barracks, spearmen, stables, horsemen, archery, attack-move, combat tips) |
| `training_missionzero.scar` | training | Interactive tutorial hint system: goal sequences for every action (select, click, build, produce, control groups) |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_SetupPlayers` | ang_chp0_intro | Configure 3 players, ages, relationships |
| `Mission_SetupVariables` | ang_chp0_intro | Init all globals, counters, flags, training markers |
| `Mission_SetRestrictions` | ang_chp0_intro | (empty) placeholder for restrictions |
| `Mission_Preset` | ang_chp0_intro | Lock all buildings/units/abilities, init objectives, halve build times |
| `Mission_Start` | ang_chp0_intro | Set resources, disable core tutorials, start economy obj |
| `GetRecipe` | ang_chp0_intro | Define MissionOMatic recipe: spawners, defenders, roving armies |
| `Villagers_StartingUnits` | ang_chp0_intro | Deploy 3 starting villagers at player town |
| `EconDarkAge_OnConstructionComplete` | ang_chp0_intro | GE_ConstructionComplete handler tracking farms/mills/houses/mines |
| `MilitaryFeudal_OnConstructionComplete` | ang_chp0_intro | GE_ConstructionComplete handler for barracks/stables/archery ranges |
| `ChangeBuildTimes` | ang_chp0_intro | Halve build times for all English buildings and units |
| `FindGoldDeposit_Monitor` | ang_chp0_intro | Check player proximity to gold deposits, add hint |
| `ApproachingMaxPop_Monitor` | ang_chp0_intro | Re-enable death ability at 180 pop |
| `Cheat_Explore_DarkAge` | ang_chp0_intro | Skip to explore phase with pre-built economy |
| `Cheat_Progress_Feudalage` | ang_chp0_intro | Skip to feudal age-up phase |
| `Cheat_FeudalMilitary` | ang_chp0_intro | Skip to feudal military phase with landmark |
| `Cheat_AttackCavalry` | ang_chp0_intro | Skip to cavalry encampment attack |
| `Cheat_AttackArchery` | ang_chp0_intro | Skip to archery encampment attack |
| `Cheat_AttackInfantry` | ang_chp0_intro | Skip to infantry encampment attack |
| `Cheat_Progress_Castleage` | ang_chp0_intro | Skip to castle age-up phase |
| `IntroEconomyDarkAge_InitObjectives` | obj_economy_darkage | Register all Dark Age economy objectives |
| `GatherFood_Monitor` | obj_economy_darkage | Track food gathered vs target (50) |
| `ProduceVillagers_Monitor` | obj_economy_darkage | Track villagers produced vs target (5) |
| `GatherWood_Monitor` | obj_economy_darkage | Track wood gathered vs target (50) |
| `MonitorNumberFarms` | obj_economy_darkage | Track farm count and assign hint points |
| `IntroExploreDarkAge_InitObjectives` | obj_explore_darkage | Register exploration objectives |
| `ProduceScout_Monitor` | obj_explore_darkage | Track scout production vs target (1) |
| `GatherGold_Monitor` | obj_explore_darkage | Track gold gathered vs target (50) |
| `IntroProgressFeudalAge_InitObjectives` | obj_progress_feudalage | Register feudal age-up objectives |
| `AgeUpFeudal_Monitor` | obj_progress_feudalage | Poll player age, complete on AGE_FEUDAL |
| `MonitorFood` | obj_progress_feudalage | Show/hide "not enough food" tip based on rate |
| `MonitorWood` | obj_progress_feudalage | Show/hide "not enough wood" tip based on rate |
| `ProgressAgeFeudal_OnConstructionStart` | obj_progress_feudalage | Track landmark placement, prevent duplicates |
| `ProgressAgeFeudal_OnConstructionCancelled` | obj_progress_feudalage | Re-unlock landmark on cancel |
| `IntroLearnSpearman_InitObjectives` | obj_military_feudal | Register spearman training objectives |
| `ProduceSpearmen_Monitor` | obj_military_feudal | Track spearmen produced vs target (10) |
| `DestroyPallisade_EntityKill` | obj_military_feudal | GE_EntityKilled handler for palisade destruction |
| `IntroAttackCavalry_InitObjectives` | obj_attackenemycavalry | Register cavalry encampment objectives |
| `AttackMove_Monitor` | obj_attackenemycavalry | Detect player using attack-move command |
| `LonelyUnit_Monitor` | obj_attackenemycavalry | Respawn sentry horseman if killed before attack-move |
| `SpawnAnotherLonelyUnit` | obj_attackenemycavalry | Deploy non-selectable French horseman for attack-move lesson |
| `CavalryEncampmentDeathEvent` | obj_attackenemycavalry | GE_SquadKilled handler counting horseman kills |
| `Horsemen_CompletionMonitor` | obj_attackenemycavalry | Fallback completion check for horsemen objective |
| `DestroyTheStables_Monitor` | obj_attackenemycavalry | Poll eg_CavalryEncampment for destruction |
| `IntroAttackArchery_InitObjectives` | obj_attack_enemyarchery | Register archery encampment objectives |
| `ProduceHorsemen_Monitor` | obj_attack_enemyarchery | Track horsemen produced vs target (15) |
| `EnemyKilledArcheryEncampment` | obj_attack_enemyarchery | GE_SquadKilled handler counting archer kills |
| `DestroyTheArcheryRange_Monitor` | obj_attack_enemyarchery | Poll eg_archery_encampment for destruction |
| `IntroAttackInfantry_InitObjectives` | obj_attack_enemyinfantry | Register infantry encampment objectives |
| `ProduceArchers_Monitor` | obj_attack_enemyinfantry | Track longbowmen produced vs target (20) |
| `LongbowmenOnCliff_Monitor` | obj_attack_enemyinfantry | Check 18+ archers near clifftop marker |
| `SpearmanDeadMonitor` | obj_attack_enemyinfantry | Check if all enemy spearmen killed |
| `BarrackDestroyedMonitor` | obj_attack_enemyinfantry | Check if enemy barracks destroyed |
| `EnemyKilledSpearmanEncampment` | obj_attack_enemyinfantry | GE_SquadKilled handler counting spearman kills |
| `SendSpearmanToAttackPlayer` | obj_attack_enemyinfantry | Dissolve defenders into roving army module |
| `MissionZero_ForceVillagersToFlee` | obj_attack_enemyinfantry | Speed-boost enemy villagers and flee to marker |
| `IntroProgressCastleAge_InitObjectives` | obj_progress_castleage | Register castle age-up objectives |
| `AgeUpCastle_Monitor` | obj_progress_castleage | Poll landmark health, complete at >95% |
| `IntroProgressToCastleAge_OnComplete` | obj_progress_castleage | Call Mission_Complete() to end mission |
| `ProgressAgeCastle_OnConstructionStart` | obj_progress_castleage | Track Castle landmark placement |
| `ProgressAgeCastle_OnConstructionCancelled` | obj_progress_castleage | Re-unlock Castle landmark on cancel |
| `Disable_CoreTutorials_MinusExceptions` | training_missionzero | Disable most core training, keep select/move/pan |
| `Tutorials_MissionZero_GatherFood` | training_missionzero | Goal sequence: select villager → right-click food |
| `Tutorials_MissionZero_SelectDragUnits` | training_missionzero | Goal sequence: bandbox multi-select |
| `Tutorials_MissionZero_HighlightVillagers` | training_missionzero | Goal sequence: select TC → click villager icon |
| `Tutorials_MissionZero_IdleVillagers` | training_missionzero | Goal sequence: click idle button → assign work |
| `Tutorials_MissionZero_HighlightMill` | training_missionzero | Goal sequence: select villager → mill icon → place |
| `Tutorials_MissionZero_GatherWood` | training_missionzero | Goal sequence: select villager → right-click trees |
| `Tutorials_MissionZero_HighlightLumberCamp` | training_missionzero | Goal sequence: select → lumber camp icon → place |
| `Tutorials_MissionZero_HighlightHouses` | training_missionzero | Goal sequence: select → house icon → place |
| `Tutorials_MissionZero_HighlightFarm` | training_missionzero | Goal sequence: select → farm icon → place |
| `Tutorials_MissionZero_BuildHouseIncreasePopCap` | training_missionzero | Goal sequence: build house when pop ≥90% |
| `Tutorials_MissionZero_HighlightScout` | training_missionzero | Goal sequence: select TC → scout icon |
| `Tutorials_MissionZero_HighlightMine` | training_missionzero | Goal sequence: select → mine icon → place near gold |
| `Tutorials_MissionZero_GatherGold` | training_missionzero | Goal sequence: select villager → right-click gold |
| `Tutorials_MissionZero_HighlightAgeUp` | training_missionzero | Goal sequence: select → age-up icon → place landmark |
| `Tutorials_MissionZero_HighlightBarracks` | training_missionzero | Goal sequence: select villager → barracks icon |
| `Tutorials_MissionZero_HighlightSpearman` | training_missionzero | Goal sequence: select barracks → spearman icon |
| `Tutorials_MissionZero_ControlGroups` | training_missionzero | Goal sequence: select spearmen → Ctrl+1 → press 1 |
| `Tutorials_MissionZero_AttackMove` | training_missionzero | Goal sequence: select spearmen → A-click ground |
| `Tutorials_MissionZero_HighlightStables` | training_missionzero | Goal sequence: select villager → stable icon |
| `Tutorials_MissionZero_BuildCavalry` | training_missionzero | Goal sequence: select stables → rally → queue horsemen |
| `Tutorials_MissionZero_HighlightArcheryRange` | training_missionzero | Goal sequence: select villager → archery range icon |
| `Tutorials_MissionZero_Highlightlongbowmen` | training_missionzero | Goal sequence: select archery range → longbowman icon |
| `Tutorials_MissionZero_HighlightAgeUpCastle` | training_missionzero | Goal sequence: select villager → age III icon |
| `MissionZero_TrainingContructionCallback` | training_missionzero | Modal construction phase logger for training predicates |
| `MissionZero_PickConvenientVillager` | training_missionzero | Find idle/on-screen villager for training hints |
| `Entity_IsSelected` | training_missionzero | Check if entity of type/instance is selected |
| `Squad_IsSelected` | training_missionzero | Check if squad of type/instance is selected |
| `Player_IsConstructingEntity` | training_missionzero | Check if player has entity type under construction |
| `Player_IsProducingSquad` | training_missionzero | Check if player is producing squad of type |

## KEY SYSTEMS

### Objectives

**Primary Objectives (sequential chain):**

| Constant | Purpose |
|----------|---------|
| `OBJ_DevelopEconomy` | Dark Age economy: gather food, produce villagers, build econ buildings |
| `SOBJ_GatherFood` | Gather 50 additional food |
| `SOBJ_ProduceVillagers` | Produce 5 villagers |
| `SOBJ_BuildMill` | Build 1 mill |
| `SOBJ_GatherWood` | Gather 50 additional wood |
| `SOBJ_BuildLumberCamp` | Build 1 lumber camp |
| `SOBJ_BuildHouses` | Build 3 houses |
| `SOBJ_BuildFarms` | Build 3 farms |
| `OBJ_ExploreTheMap` | Exploration: produce scout, find/mine gold |
| `SOBJ_ProduceScouts` | Produce 1 scout |
| `SOBJ_FindGoldDeposit` | Scout near a gold deposit |
| `SOBJ_BuildMine` | Build 1 mining camp |
| `SOBJ_GatherGold` | Gather 50 additional gold |
| `OBJ_ProgressFeudalAge` | Age up to Feudal via Abbey of Kings landmark |
| `SOBJ_AgeUpFeudal` | Build and complete the landmark |
| `OBJ_LearnSpearman` | Build barracks, produce spearmen, destroy palisade |
| `SOBJ_BuildBarrack` | Build 1 barracks |
| `SOBJ_ProduceSpearmen` | Produce 10 spearmen |
| `SOBJ_DestroyThePallisade` | Destroy French palisade wall |
| `OBJ_AttackCavalryEncampment` | Attack-move tutorial + destroy cavalry encampment |
| `SOBJ_AttackMove` | Use attack-move on a roving horseman |
| `SOBJ_KillHorsemen` | Kill 6 horsemen at cavalry village |
| `SOBJ_DestroyTheStables` | Destroy all cavalry encampment buildings |
| `OBJ_AttackArchersEncampment` | Build stables, produce horsemen, destroy archery encampment |
| `SOBJ_BuildStables` | Build 2 stables near designated area |
| `SOBJ_ProduceHorsemen` | Produce 15 horsemen |
| `SOBJ_KillArchers` | Kill all archers (progress bar) |
| `SOBJ_DestroyTheArcheryEncampment` | Destroy archery encampment buildings |
| `OBJ_AttackInfantryEncampment` | Build archery ranges, produce longbowmen, defeat spearmen |
| `SOBJ_BuildArcheryRange` | Build 3 archery ranges near designated area |
| `SOBJ_ProduceArchers` | Produce 20 longbowmen |
| `SOBJ_SetupLongbowmenOnCliff` | Position 18+ longbowmen on clifftop |
| `SOBJ_KillSpearman` | Kill enemy spearmen (progress bar) |
| `OBJ_ProgressCastleAge` | Build White Tower landmark to win |
| `SOBJ_AgeUpCastle` | Construct Castle Age landmark |

**Tip Objectives (Dark Age):** `OBJ_Tip_GatherFood`, `OBJ_Tip_ProduceVillagers`, `OBJ_Tip_BuildMill`, `OBJ_Tip_GatherWood`, `OBJ_Tip_BuildFarms`, `OBJ_Tip_BuildHouses`, `OBJ_Tip_BuildLumberCamp`, `OBJ_Tip_ProduceScout`, `OBJ_Tip_FindGoldDeposit`, `OBJ_Tip_BuildMine`, `OBJ_Tip_GatherGold`, `OBJ_Tip_AgeUpFeudal`, `OBJ_Tip_AgeUpFeudalMoreVillagers`

**Tip Objectives (Feudal):** `OBJ_Tip_NotEnoughFood`, `OBJ_Tip_NotEnoughWood`, `OBJ_Tip_MakeMoreVillagers`, `OBJ_Tip_doubleclickunits`, `OBJ_Tip_Attack`, `OBJ_Tip_BuildBarracks`, `OBJ_Tip_ProduceSpearmen`, `OBJ_Tip_BuildMultipleStables`, `OBJ_Tip_AttackMove`, `OBJ_Tip_BuildStables`, `OBJ_Tip_ProduceHorsemen`, `OBJ_Tip_CombatVsCavalry`, `OBJ_Tip_CombatVsArchery`, `OBJ_TipBuildArcheryRange`, `OBJ_Tip_ProduceArchers`, `OBJ_Tip_SetupArchers`, `OBJ_Tip_CombatVsInfantry`, `OBJ_Tip_AgeUpCastle`

### Difficulty

No `Util_DifVar` calls — this is a fixed-difficulty tutorial mission. All parameters are hardcoded constants (e.g., 10 spearmen, 15 horsemen, 20 longbowmen).

### Spawns

| Module Type | Descriptor | Units | Behavior |
|-------------|-----------|-------|----------|
| UnitSpawner | `Enemy_Horseman_guards` | 6 horsemen (player2) | Static at cavalry village |
| UnitSpawner | `Enemy_Archer_guards` | 15 archers (player2) | Static at archery village |
| Defend | `Enemy_spearman_guards` | 12 spearmen (5+5+2, player2) | Defend spearman village, combatRange=60, leash=85 |
| RovingArmy | `Cavalry_AttackMove_Scout` | 1 horseman (player2) | Patrol between two markers (attack-move lesson target) |
| RovingArmy | `Spearman_village_attack_roving` | Dissolved from defenders | Roving patrol 4 waypoints + clifftop |
| Runtime spawn | `SpawnAnotherLonelyUnit` | 1 horseman (non-selectable) | Respawned if killed before attack-move completes |
| Runtime deploy | `Villagers_StartingUnits` | 3 villagers (player1) | Deployed at mission start |
| CTA deploy | Stables/Archery joiners | 3 villagers each | Deployed when stables/archery obj starts |

### AI

- **No `AI_Enable` calls** — enemy player2 units are entirely scripted via MissionOMatic modules (Defend, RovingArmy, UnitSpawner).
- Cavalry scout is set non-selectable (`SGroup_SetSelectable(false)`) and given HoldPosition after moving to destination.
- `DissolveModuleIntoModule("Enemy_spearman_guards", "Spearman_village_attack_roving")` transfers defenders to roving patrol when combat begins.
- Enemy villagers use `MissionZero_ForceVillagersToFlee()` with 1.15x speed modifier and walla fear audio.

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `FindGoldDeposit_Monitor` | `Rule_AddInterval(..., 1)` | Check player proximity to gold veins every 1s |
| `ApproachingMaxPop_Monitor` | `Rule_AddInterval(..., 5)` | Re-enable death ability at 180 pop, every 5s |
| `AgeUpFeudal_Monitor` | `Rule_AddInterval(..., 2)` | Poll `Player_GetCurrentAge` every 2s |
| `AgeUpCastle_Monitor` | `Rule_AddInterval(..., 0.25)` | Poll landmark health every 0.25s |
| `MonitorFood` / `MonitorWood` | `Rule_AddInterval(..., 3)` | Check resource rates every 3s for tips |
| `SpearmanDeadMonitor` | `Rule_AddInterval(..., 1)` | Check spearman count every 1s |
| `BarrackDestroyedMonitor` | `Rule_AddInterval(..., 1.5)` | Check barracks existence every 1.5s |
| `LonelyUnit_Monitor` | `Rule_AddInterval(..., 1)` | Respawn attack-move target if killed early |
| `Horsemen_CompletionMonitor` | `Rule_AddInterval(..., 1)` | Fallback horseman kill check every 1s |
| All `Rule_AddOneShot(..., 3)` tips | 3s delay | Short delay before showing tip objectives |
| `WaitBeforeStartNextAttackObj` | `Rule_AddOneShot(..., 1)` | 1s delay between spearman and cavalry obj |
| `StartDelayedObjArcheryBuildings` | `Rule_AddOneShot(..., 2)` | 2s delay before archery destroy obj |
| `g_training_timers.very_short` | 1s | PopCap trigger delay |
| `g_training_timers.short` | 5s | Most training lesson triggers |
| `g_training_timers.mid` | 10s | Idle villager, scout, mine, gold lessons |
| `g_training_timers.normal` | 15s | Attack palisade lesson trigger |

## CROSS-REFERENCES

### Imports

| Import | Used In |
|--------|---------|
| `MissionOMatic/MissionOMatic.scar` | ang_chp0_intro (brings Cardinal scripts) |
| `obj_economy_darkage.scar` | ang_chp0_intro |
| `obj_explore_darkage.scar` | ang_chp0_intro |
| `obj_progress_feudalage.scar` | ang_chp0_intro |
| `obj_tip_darkage.scar` | ang_chp0_intro |
| `obj_military_feudal.scar` | ang_chp0_intro |
| `obj_attackenemycavalry.scar` | ang_chp0_intro |
| `obj_attack_enemyarchery.scar` | ang_chp0_intro |
| `obj_attack_enemyinfantry.scar` | ang_chp0_intro |
| `obj_progress_castleage.scar` | ang_chp0_intro |
| `obj_tip_feudal.scar` | ang_chp0_intro |
| `training_missionzero.scar` | ang_chp0_intro |
| `training.scar` | training_missionzero |
| `training/campaigntraininggoals.scar` | training_missionzero |
| `training/coretraininggoals.scar` | training_missionzero |

### Shared Globals

- **Players:** `player1`, `player2`, `player3` — set in core, used everywhere
- **Counters:** `i_desiredSpearmen`, `i_amount_horsemen_produce`, `i_amount_longbowman_produce`, `i_desired_Farms`, `i_desired_Houses`, `i_amount_stables`, `i_amount_archeryranges`, resource amounts — set in core, read in objective files
- **Flags:** `b_barracks_built`, `b_stables_built`, `b_archeryRange_built`, `b_attackMoving`, `feudalAgeStartedConstruction`, `castleAgeStartedConstruction`, `killedSpearmanObj`, `destroyedBarracksObj`, `longbowmanCliffObjCompleted`
- **SGroups/EGroups:** `sg_villagers_player`, `sg_horsemanVillage_horseman`, `sg_archerVillage_archers`, `sg_spearmanVillage_spearman`, `sg_fre_attackMove_scout`, `eg_CastleLandmark`, `eg_stablesForTutorial`, `eg_landmarkForTutorial`, `sg_spearmenForTutorial`, `sg_eng_villagers_stables`, `sg_eng_villagers_archeryrange`
- **Training globals:** `g_training_log`, `g_training_timers`, `g_training_markers`, `g_GoalVillagerSelectedHidden`, `control_group_1_has_spearmen`, `user_has_selected_control_group_1`
- **Map-placed EGroups:** `eg_allied_palisade`, `eg_enemy_village1`, `eg_enemy_village2`, `eg_CavalryEncampment`, `eg_archery_encampment`, `eg_spearman_encampment`

### Key Inter-File Calls

- Core → Objective files: `IntroEconomyDarkAge_InitObjectives()`, `IntroExploreDarkAge_InitObjectives()`, `IntroProgressFeudalAge_InitObjectives()`, `IntroLearnSpearman_InitObjectives()`, `IntroAttackCavalry_InitObjectives()`, `IntroAttackArchery_InitObjectives()`, `IntroAttackInfantry_InitObjectives()`, `IntroProgressCastleAge_InitObjectives()`, `IntroTipsDarkAge_InitObjectives()`, `IntroTipsFeudal_InitObjectives()`
- Core → Training: `Disable_CoreTutorials_MinusExceptions()`, `UI_SetModalConstructionPhaseCallback(MissionZero_TrainingContructionCallback)`
- Objective files → Training: `Tutorials_MissionZero_*()` calls (GatherFood, HighlightVillagers, HighlightMill, HighlightBarracks, HighlightSpearman, ControlGroups, AttackMove, HighlightStables, BuildCavalry, HighlightArcheryRange, Highlightlongbowmen, HighlightAgeUp, HighlightAgeUpCastle, etc.)
- Objective files → Core: construction complete handlers (`EconDarkAge_OnConstructionComplete`, `MilitaryFeudal_OnConstructionComplete`) registered via `Rule_AddGlobalEvent` from objective PreStart callbacks
- Objective chain: `IntroEconomy_OnComplete` → `OBJ_ExploreTheMap` → `OBJ_ProgressFeudalAge` → `OBJ_LearnSpearman` → `OBJ_AttackCavalryEncampment` → `OBJ_AttackArchersEncampment` → `OBJ_AttackInfantryEncampment` → `OBJ_ProgressCastleAge` → `Mission_Complete()`
- Infantry file → MissionOMatic: `DissolveModuleIntoModule("Enemy_spearman_guards", "Spearman_village_attack_roving")`
- Infantry file uses `villagerlife_spearmantown` / `villagerlife_spearmantown_02` (map-placed data) via `MissionZero_ForceVillagersToFlee()`
- `World_SetInteractionStage()` gates: 0→1 (palisade destroyed), 1→2 (cavalry attack), 2→3 (horsemen produced), 3→4 (archers produced)
