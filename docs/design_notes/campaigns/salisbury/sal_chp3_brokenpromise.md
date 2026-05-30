# Salisbury Chapter 3: Broken Promise

## OVERVIEW

This is a **tutorial-style campaign mission** in the Salisbury (Angevin) campaign where the player controls Duke William (Guillaume de Normandie) as the French civilization preparing and executing a naval invasion of England. The mission flows through a multi-phase linear objective chain: build a fleet (docks + transport ships) → gather resources (food/wood/gold) → age up to Feudal → build military infrastructure (barracks/archery/stables) → train an invasion army (40 spearmen, 30 horsemen, 30 archers) → load troops onto transport ships → sail across the Channel → disembark at Pevensey beach → repel a beach ambush → capture Pevensey castle → scout and locate Hastings → destroy the Hastings Town Center. Heavy Xbox controller training sequences guide the player through dock construction, transport ship production, troop loading/unloading, minimap navigation, and combat. Production rates are doubled and build times halved to maintain tutorial pacing. No difficulty scaling is implemented (`Mission_SetDifficulty` is empty).

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `sal_chp3_brokenpromise.scar` | core | Mission entry point: player/relationship setup, restrictions, variable init, intro/outro cinematics, enemy spawning, production modifiers, Defend module initialization for Pevensey and Hastings garrisons |
| `obj_gather.scar` | objectives | Resource gathering objectives: collect 400 food, 400 wood, 200 gold, then age up to Feudal |
| `obj_build.scar` | objectives | Military buildup objectives: build 2 barracks/archery/stables, then train 40 spearmen, 30 horsemen, 30 archers |
| `obj_fleet.scar` | objectives | Fleet and transport objectives: build 2 docks, build 3 transport ships, load 48+ troops onto ships |
| `obj_invade.scar` | objectives | Invasion phase objectives: sail to Pevensey, disembark, repel beach ambush, capture Pevensey, locate Hastings, destroy Town Center |
| `training_sal_chp3_brokenpromise.scar` | training | Xbox controller training goal sequences for dock building, transport ship production, troop loading, minimap usage, unloading, ambush panic-select, and scouting |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnGameSetup` | sal_chp3_brokenpromise | Set player names: William, Anglo-Saxons, Neutral |
| `Mission_OnInit` | sal_chp3_brokenpromise | Set ages, enable training, configure alliances and colors |
| `Mission_SetupVariables` | sal_chp3_brokenpromise | Init SGroups, EGroups, build-time modifiers, register objectives |
| `Mission_SetDifficulty` | sal_chp3_brokenpromise | Empty — no difficulty scaling |
| `Mission_SetRestrictions` | sal_chp3_brokenpromise | Lock most units/buildings/upgrades for tutorial progression |
| `Mission_PreStart` | sal_chp3_brokenpromise | Spawn villagers, enemies, give 1500 resources, breach walls |
| `Mission_Start` | sal_chp3_brokenpromise | Enable Xbox HUD elements, init training, reveal FOW |
| `Mission_Start_WaitForSpeechToFinish` | sal_chp3_brokenpromise | Poll until intro NIS ends, then start OBJ_BuildFleet |
| `SpawnEnemies` | sal_chp3_brokenpromise | Deploy 5 spearmen at Hastings for player2 |
| `SpawnLandingAmbush` | sal_chp3_brokenpromise | Spawn 15 men-at-arms at 3 beach markers |
| `GetTroopsEmbarked` | sal_chp3_brokenpromise | Count squads garrisoned inside transport ships |
| `MonitorPlayerShips` | sal_chp3_brokenpromise | Track new transport ships, boost speed, remove death |
| `Init_PevenseyDefenders` | sal_chp3_brokenpromise | Init 5 Defend modules for Pevensey garrison |
| `Init_HastingsDefenders` | sal_chp3_brokenpromise | Init 15 Defend modules for Hastings garrison |
| `ProduceBuildingsObjectiveTracker` | sal_chp3_brokenpromise | Generic tracker: monitor building count for objective |
| `ProduceBuildings_Monitor` | sal_chp3_brokenpromise | Poll player buildings, complete objective at threshold |
| `ProduceUnitsObjectiveTracker` | sal_chp3_brokenpromise | Generic tracker: monitor unit count for objective |
| `ProduceUnits_Monitor` | sal_chp3_brokenpromise | Poll player units, complete objective at threshold |
| `Spawn_Intro` | sal_chp3_brokenpromise | Deploy William, scouts, cavalry, spearmen, archers for intro |
| `Reset_Intro` | sal_chp3_brokenpromise | Restore unit speeds after intro cinematic |
| `Skip_Intro` | sal_chp3_brokenpromise | Warp all intro units to destinations on skip |
| `GetRecipe` | sal_chp3_brokenpromise | Return MissionOMatic recipe with intro/outro NIS, title card |
| `Spawn_Outro` | sal_chp3_brokenpromise | Deploy villagers, army, cheerers for outro cinematic |
| `WilliamMove_Outro` | sal_chp3_brokenpromise | William horseback parade through Hastings via Util_UnitParade |
| `RestoreHastings_Outro` | sal_chp3_brokenpromise | Give wood, accelerate build, reconstruct Hastings buildings |
| `Gather_InitObjectives` | obj_gather | Register OBJ_Gather + 3 resource sub-objectives + OBJ_AgeUp |
| `GatherFood_Start` | obj_gather | Start villager automation training, monitor food |
| `GatherFood_Monitor` | obj_gather | Complete SOBJ_GatherFood at 400 food |
| `GatherWood_Monitor` | obj_gather | Complete SOBJ_GatherWood at 400 wood |
| `GatherGold_Monitor` | obj_gather | Complete SOBJ_GatherGold at 200 gold |
| `BuildInvasionForce_InitObjectives` | obj_build | Register build + army sub-objectives (6 SOBJs) |
| `Build2Barracks_Start` | obj_build | Track barracks via ProduceBuildingsObjectiveTracker |
| `Make40Spearmen_Start` | obj_build | Track spearmen via ProduceUnitsObjectiveTracker |
| `BuildFleet_InitObjectives` | obj_fleet | Register OBJ_BuildFleet, dock/transport/load objectives |
| `Build2Docks_PreStart` | obj_fleet | Unlock dock construction for player1 |
| `Build3TransportShips_Start` | obj_fleet | Track transport ships, start training goals |
| `LoadTroops_Monitor` | obj_fleet | Complete OBJ_LoadTroops when 48+ troops embarked |
| `BeginInvasion_InitObjectives` | obj_invade | Register invasion, sail, unload, ambush, Pevensey, Hastings objectives |
| `SetSail_Monitor` | obj_invade | Complete when ships near Pevensey landing marker |
| `UnloadArmy_PreStart` | obj_invade | Unlock unload ability, set disembark tracking |
| `UnloadArmy_Monitor` | obj_invade | Track disembark progress, complete when all unloaded |
| `ShipsMaintainPosition_Monitor` | obj_invade | Force ships to stay near Pevensey landing |
| `BeachAmbush_StartSurviveAmbush` | obj_invade | Launch ambush attack-move, start survival monitor |
| `BeachAmbush_Monitor` | obj_invade | Complete when all ambush enemies killed |
| `TakePevensey_Start` | obj_invade | Aggregate 5 garrison groups, monitor kills |
| `TakePevensey_Monitor` | obj_invade | Progress bar tracking Pevensey garrison elimination |
| `LocateHastings_Start` | obj_invade | Spawn scout if needed, aggregate 16 garrison groups |
| `LocateHastings_Monitor` | obj_invade | Complete when player unit near Hastings proximity marker |
| `Spawn_HastingsReinforcement` | obj_invade | Deploy 15 spearmen, 10 archers, 10 horsemen reinforcements |
| `DestroyTC_Start` | obj_invade | Monitor enemy TC destruction, listen for gate kill event |
| `DestroyTC_Monitor` | obj_invade | Complete SOBJ_DestroyTC when eg_enemy_tc count is 0 |
| `ApplyProductionPromptMarkers` | obj_invade | Add HintPoints to captured Pevensey production buildings |
| `MissionTutorial_Init` | training | Init construction/ability phase callbacks for training |
| `Goals_Docks` | training | Training sequence: select villager → military menu → dock → place |
| `Goals_TransportShips` | training | Training sequence: select docks → open menu → produce ships |
| `Goals_LoadTroops` | training | Training sequence: select army → board ship → repeat |
| `Goals_Minimap` | training | Training sequence: select ships → open minimap → move → close |
| `Goals_UnloadTroops` | training | Training sequence: open radial → unload ability → target beach |
| `Goals_SurviveAmbush` | training | Training: panic-select all units on screen during ambush |
| `Goals_MarchHastings` | training | Training: select scout → set waypoints into fog of war |
| `LoadTroops_GetNonFullShip` | training | Find first transport ship with remaining hold slots |
| `Docks_IgnorePredicate` | training | Remove dock training when 2 docks built |
| `TransportShips_IgnorePredicate` | training | Remove ship training when ships produced or queued |
| `Minimap_IgnorePredicate` | training | Remove minimap training when sail objective complete |

## KEY SYSTEMS

### Objectives

**Resource Phase:**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Gather` | Primary | Parent: gather resources for invasion |
| `SOBJ_GatherFood` | Sub | Gather 400 food (progress bar) |
| `SOBJ_GatherWood` | Sub | Gather 400 wood (progress bar) |
| `SOBJ_GatherGold` | Sub | Gather 200 gold (progress bar) |
| `OBJ_AgeUp` | Primary | Advance to Age II (Feudal) |

**Build Phase:**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_BuildInvasionForce` | Primary | Parent: build military production buildings |
| `SOBJ_Build2Barracks` | Sub | Build 2 barracks (counter 0/2) |
| `SOBJ_Build2Archery` | Sub | Build 2 archery ranges (counter 0/2) |
| `SOBJ_Build2Stables` | Sub | Build 2 stables (counter 0/2) |
| `OBJ_BuildInvasionArmy` | Primary | Parent: train invasion force |
| `SOBJ_Make40Spearmen` | Sub | Train 40 spearmen (counter 0/40) |
| `SOBJ_Make30Horsemen` | Sub | Train 30 horsemen (counter 0/30) |
| `SOBJ_Make30Archers` | Sub | Train 30 archers (counter 0/30) |

**Fleet Phase:**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_BuildFleet` | Primary | Parent: build naval fleet |
| `SOBJ_Build2Docks` | Sub | Build 2 docks (counter 0/2) |
| `SOBJ_Build3TransportShips` | Sub | Build 3 transport ships (counter 0/3) |
| `OBJ_LoadTroops` | Primary | Board 48+ troops onto transport ships |

**Invasion Phase:**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_BeginInvasion` | Primary | Parent: execute invasion of England |
| `SOBJ_SetSail` | Sub | Sail ships to Pevensey landing marker |
| `SOBJ_UnloadArmy` | Sub | Disembark all troops (progress bar) |
| `SOBJ_BeachAmbush` | Sub | Repel 15 men-at-arms beach ambush |
| `SOBJ_TakePevensey` | Sub | Eliminate all Pevensey garrison defenders (progress bar) |
| `OBJ_LocateHastings` | Primary | Scout into fog of war to find Hastings |
| `OBJ_TakeHastings` | Primary | Parent: conquer Hastings |
| `SOBJ_DestroyTC` | Sub | Destroy the enemy Town Center |

**Objective Flow:**
`OBJ_BuildFleet` → `OBJ_BuildInvasionArmy` → `OBJ_BuildFleet(docks→ships→load)` → `OBJ_BeginInvasion(sail→unload→ambush→Pevensey)` → `OBJ_LocateHastings` → `OBJ_TakeHastings` → `Mission_Complete()`

*Note: The actual start order begins with `OBJ_BuildFleet` (docks/ships/load), which on completion of loading triggers the invasion phase. The gather/build/army objectives are registered but their start trigger chain is: gather → age up → build buildings → build army → build fleet.*

### Difficulty

No difficulty scaling is implemented. `Mission_SetDifficulty()` is empty. No `Util_DifVar` calls are present.

### Spawns

**Player Starting Forces (Intro):**
- 1 Duke William (hero, invulnerable min cap 75%)
- 2 scouts
- 10 horsemen (5 groups × 2)
- 20 spearmen (7 groups × 2-3)
- 15 archers (5 groups × 3)
- 5 villagers

**Enemy Pre-placed:**
- Hastings: 5 spearmen (spawned during `Mission_PreStart`)

**Beach Ambush (dynamic spawn on disembark):**
- 15 men-at-arms across 3 markers (5 per marker)

**Pevensey Garrison (5 Defend modules):**
- 8 men-at-arms (2 groups × 4), 9 spearmen (3 groups × 3) — combat range 55, leash 60

**Hastings Garrison (15 Defend modules):**
- 25 spearmen (5 groups × 5), 21 horsemen (3 groups × 7), 24 archers (6 groups × 4), 5 men-at-arms (1 group) — combat range 50, leash 65

**Reinforcements (on Hastings discovery):**
- 15 spearmen, 10 archers, 10 horsemen (Feudal-age units) deployed at Pevensey and marched forward

### AI

- No `AI_Enable` calls — enemies use the **Defend module** (`Defend_Init`) exclusively
- Pevensey: 5 Defend groups anchored to `mkr_pevensey_castle`, combat range 55, leash 60
- Hastings: 15 Defend groups distributed across `mkr_hastings_lower`, `mkr_hastings_upper`, `mkr_hastings_center` with combat range 50, leash 65
- Beach ambush uses simple `Cmd_AttackMove` toward the beach — no AI plan
- `PlayerNearTarget` function triggers Hastings garrison to attack-move when player approaches `mkr_hastings_cavalry_03`

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `Mission_Start_WaitForSpeechToFinish` | 1s interval | Wait for intro NIS to finish before starting objectives |
| `MonitorPlayerShips` | 1s interval | Track new transport ships, apply speed boost (1.2x) |
| `ShipsMaintainPosition_Monitor` | 1s interval | Force ships to stay within 50 units of landing marker |
| `LocateHastings_Monitor` | 1s interval | Check player proximity (175 units) to Hastings |
| `GatherFood/Wood/Gold_Monitor` | every frame (Rule_Add) | Poll resource amounts against thresholds |
| `ProduceBuildings_Monitor` | every frame (Rule_Add) | Poll building count for objective completion |
| `ProduceUnits_Monitor` | every frame (Rule_Add) | Poll unit count for objective completion |
| `SetSail_Monitor` | every frame (Rule_Add) | Check ship proximity to Pevensey landing |
| `UnloadArmy_Monitor` | every frame (Rule_Add) | Track disembark progress bar |
| `BeachAmbush_Monitor` | every frame (Rule_Add) | Check if all ambush enemies eliminated |
| `TakePevensey_Monitor` | every frame (Rule_Add) | Track Pevensey garrison elimination progress |
| `DestroyTC_Monitor` | every frame (Rule_Add) | Check if enemy TC destroyed |
| `LoadTroops_Monitor` | every frame (Rule_Add) | Check if 48+ troops embarked |

### Production Modifiers

- `Modify_PlayerProductionRate(player1, 2)` — 2x production speed
- `Modify_EntityBuildTime` at 0.5x for: docks, spearmen (tier 1+2), archers (tier 2), horsemen (tier 2)

### Interaction Stages

- **Stage 0**: Initial (Normandy preparation phase)
- **Stage 1**: Set after troops loaded — triggers Pevensey defender initialization
- **Stage 2**: Set after Pevensey captured — Pevensey structures transferred to player

### FOW Reveals

- Starting area: `mkr_starting_fow_reveal`
- Beach (13 markers): `mkr_beach_fow_reveal_01` through `_13` on ship arrival
- Pevensey (4 markers): revealed on SetSail objective completion
- Hastings (3 markers): revealed when player approaches Hastings

## CROSS-REFERENCES

### Imports
| File | Imports |
|------|---------|
| `sal_chp3_brokenpromise.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar`, `obj_gather.scar`, `obj_build.scar`, `obj_fleet.scar`, `obj_invade.scar`, `training_sal_chp3_brokenpromise.scar` |
| `obj_fleet.scar` | `cardinal.scar`, `sal_chp3_brokenpromise.scar` |
| `obj_invade.scar` | `cardinal.scar`, `sal_chp3_brokenpromise.scar` |
| `training_sal_chp3_brokenpromise.scar` | `training.scar`, `cardinal.scar` |

### Shared Globals (cross-file)
- `sg_ships` — created in `MonitorPlayerShips` (core), read by training (LoadTroops, Minimap, UnloadTroops sequences) and obj_fleet (`LoadTroops_Monitor`)
- `sg_army` — created in `Build2Docks_Start` (obj_fleet), read by training (`SelectMilitary_CompletePredicate`, `SurviveAmbush_IgnorePredicate`)
- `sg_william` — created in core, used in obj_fleet (`Build2Docks_Start`) and invasion sequences
- `sg_embarked` — created in `GetTroopsEmbarked` (core), set selectable in `UnloadArmy_PreStart` (obj_invade)
- `sg_startVillagers` — created in `Mission_PreStart` (core), used in training (`Goals_Docks`)
- `sg_scouts` — created in core, used in `LocateHastings_Start`/`Goals_MarchHastings` (obj_invade/training)
- `sg_landingAmbush` — created in `SpawnLandingAmbush` (core), used in `BeachAmbush_Monitor` (obj_invade)
- `disembarkedPevensey` — set in `UnloadArmy_PreStart` (obj_invade), read by training `UnloadTroops_IgnorePredicate`
- `minimapDone` — set in training `CloseMinimap_CompletePredicate`, read by `Minimap_IgnorePredicate`
- `eg_docks` — created in training, referenced in `TransportShips_IgnorePredicate`
- `EVENTS.*` — event table referenced across all files for intel/NIS triggers
- `player1`, `player2`, `player3` — set in core `Mission_OnGameSetup`, used globally
- `eg_pevensey_structures` — used in core (targeting/burn protection) and obj_invade (ownership transfer)

### Inter-file Function Calls
- `obj_fleet.scar` → `Goals_Docks()`, `Goals_TransportShips()`, `Goals_LoadTroops()` (training file)
- `obj_invade.scar` → `Goals_Minimap()`, `Goals_UnloadTroops()`, `Goals_SurviveAmbush()`, `Goals_MarchHastings()` (training file)
- `obj_invade.scar` → `Init_PevenseyDefenders()`, `Init_HastingsDefenders()`, `SpawnLandingAmbush()`, `Spawn_HastingsReinforcement()` (core file)
- `obj_invade.scar` → `GetTroopsEmbarked()`, `MonitorPlayerShips()` (core file)
- `obj_build.scar` / `obj_fleet.scar` → `ProduceBuildingsObjectiveTracker()`, `ProduceUnitsObjectiveTracker()` (core file)
- `obj_gather.scar` → `Goals_VillagerAutomation()` (training file — referenced but not defined in provided batches)
- `obj_build.scar` → `Goals_MultiSelectionReminder()` (training file — referenced but not defined in provided batches)
- `obj_invade.scar` → `ApplyProductionPromptMarkers()` (self, called on Pevensey capture)

### Blueprint References
- `SBP.CAMPAIGN.UNIT_DUKE_WILLIAM_CMP_SAL` — hero unit
- `SBP.FRENCH.UNIT_NAVAL_TRANSPORT_SHIP_2_FRE` — transport ships
- `EBP.FRENCH.BUILDING_UNIT_NAVAL_FRE` — docks
- `BP_GetAbilityBlueprint("naval_hold_unload")` — ship unload ability
- French military: `UNIT_SPEARMAN_1/2_FRE`, `UNIT_HORSEMAN_2_FRE`, `UNIT_ARCHER_2_FRE`, `UNIT_SCOUT_1_FRE`, `UNIT_VILLAGER_1_FRE`
- English units removed from captured buildings: `UNIT_ARCHER_2_ENG`, `UNIT_MANATARMS_1_ENG`, `UNIT_KNIGHT_3_ENG`
