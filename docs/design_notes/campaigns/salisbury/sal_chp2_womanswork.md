# Salisbury Chapter 2: Woman's Work

## OVERVIEW

This is a **tutorial mission** in the Salisbury (Angevin) campaign where the player controls Mathilde and learns foundational economy mechanics as the French civilization. The mission progresses through a strict linear objective chain: select villagers → gather food → build economy structures (Mill, Lumber Camp) → train villagers → build houses → scout for sheep → build a Mine and Farms → set Villager Priorities → research Wheelbarrow → build a Landmark to advance to Age II. There is no combat; all restrictions are progressively unlocked as objectives complete. An extensive Xbox controller training system provides step-by-step radial-menu guidance for every action. Build times and production rates are heavily modified (2x production, 0.5x construction time) to keep the tutorial pacing fast.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `sal_chp2_womanswork.scar` | core | Mission entry point: setup, restrictions, intro NIS, variable init, build-time modifiers |
| `obj_villagers.scar` | objectives | Phase 1 objectives: select villager, gather food, build Mill/Lumber, train villagers, build houses |
| `obj_scout.scar` | objectives | Phase 2 objectives: find sheep with scout, herd them to TC, harvest sheep |
| `obj_grow.scar` | objectives | Phase 3 objectives: build Mine, build 3 Farms, assign villagers to farms, place/complete Landmark |
| `obj_officials.scar` | objectives | Phase 4 objectives: set Villager Priority preset, research Wheelbarrow upgrade |
| `training_sal_chp2_womanswork.scar` | training | Xbox controller training goal sequences for all objectives (radial menus, D-pad, SMS) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnGameSetup` | sal_chp2_womanswork | Set player1 as Mathilde, init produced_villagers counter |
| `Mission_OnInit` | sal_chp2_womanswork | Force-enable training system and tutorialized HUD widgets |
| `Mission_SetupVariables` | sal_chp2_womanswork | Init all objective tables, set build modifiers and resources |
| `Mission_SetRestrictions` | sal_chp2_womanswork | Lock all buildings/units/upgrades; progressively unlocked later |
| `Mission_Preset` | sal_chp2_womanswork | Lock music intensity, set construction phase callback |
| `Mission_Start` | sal_chp2_womanswork | Boost gold, enable partial Xbox UI, start first objective |
| `Mission_Start_WaitForSpeechToFinish` | sal_chp2_womanswork | Polls until intro NIS ends, then starts OBJ_VillagersWork |
| `ChangeBuildTimes` | sal_chp2_womanswork | Apply 0.25–0.75x build time multipliers for tutorial pacing |
| `Spawn_Intro` | sal_chp2_womanswork | Deploy William, cavalry, scout, villagers for intro NIS |
| `Intro_Parade` | sal_chp2_womanswork | Move William and cavalry off-map during intro |
| `Intro_Skip` | sal_chp2_womanswork | Warp units to destinations if intro is skipped |
| `GetRecipe` | sal_chp2_womanswork | Return MissionOMatic recipe with intro NIS and title card |
| `VillagersWork_InitObjectives` | obj_villagers | Register 8 sub-objectives for villager work phase |
| `SelectVillager_Monitor` | obj_villagers | Complete SOBJ when player selects a villager |
| `GatherFood_Monitor` | obj_villagers | Track food gathered; complete at 10 food above starting |
| `Villagers_OnSquadBuilt` | obj_villagers | Track villager production for Make2/Make5/Houses objectives |
| `BuildMill_Monitor` | obj_villagers | Complete SOBJ_BuildMill on mill construction finished |
| `BuildMillStarted_Monitor` | obj_villagers | Flag training_mill_placed on mill placement started |
| `BuildLumber_Monitor` | obj_villagers | Complete SOBJ_BuildLumber on lumber camp finished |
| `BuildHouses_Monitor` | obj_villagers | Increment house counter; complete at num_houses (2) |
| `VillagersWork_CheckForNextObjective` | obj_villagers | Skip scout phase if player already harvested sheep |
| `Make2Villagers_CheckTrainingUI` | obj_villagers | Check if 2 villagers queued/produced for training hints |
| `Make5Villagers_CheckTrainingUI` | obj_villagers | Check if 5 villagers queued/produced for training hints |
| `Scout_InitObjectives` | obj_scout | Register OBJ_Scout with 3 sub-objectives |
| `FindSheep_Monitor` | obj_scout | Complete when scout has sheep or sheep near TC |
| `HerdSheep_Monitor` | obj_scout | Complete when sheep herded to TC or 25% harvested |
| `HarvestSheep_Monitor` | obj_scout | Complete when sheep health drops below 1 |
| `Cheat_Scout` | obj_scout | Debug cheat to skip scout phase |
| `GrowTown_InitObjectives` | obj_grow | Register mine, farms, assign villager, landmark objectives |
| `BuildMine_Monitor` | obj_grow | Complete SOBJ_BuildMine on mining camp finished |
| `BuildFarms_Monitor` | obj_grow | Increment farm counter; complete at num_farms (3) |
| `AssignVillagers_Monitor` | obj_grow | Track worked farms via Entity_GetNumInteractors |
| `Salisbury3_GetWorkedFarms` | obj_grow | Count farms with active resource_worked interactors |
| `Salisbury3_StartAssign` | obj_grow | Skip assign objective if 3 farms already worked |
| `PlaceLandmark_Monitor` | obj_grow | Complete when wonder_dark_age entity placed |
| `PlacingLandmarkMonitor` | obj_grow | Track landmark placement phase for training hints |
| `WaitFinish_Monitor` | obj_grow | Complete when landmark construction finishes |
| `Cheat_Grow` | obj_grow | Debug cheat to skip grow phase |
| `CommandOfficials_InitObjectives` | obj_officials | Register VPS and research sub-objectives |
| `SetBalanced_Monitor` | obj_officials | Complete when any VPS resource weight > 0 |
| `Salisbury3_MonitorResearchObjStart` | obj_officials | Delay research objective until VPS radial closed |
| `Research_Monitor` | obj_officials | Complete when Wheelbarrow upgrade finishes |
| `Goals_SelectVillager` | training | Training sequence: select idle villager via D-pad |
| `Goals_GatherFood` | training | Training sequence: move to food, gather resources |
| `Goals_BuildMill` | training | Training sequence: open radial, select Mill, place it |
| `Goals_BuildLumber` | training | Training sequence: open radial, select Lumber Camp |
| `Goals_BuildMine` | training | Training sequence: SMS flow for placing mining camp |
| `Goals_BuildFarms` | training | Training sequence: SMS flow for placing farms near mill |
| `Goals_VillagerCommand` | training | Training sequence: select TC, open radial, queue villagers |
| `Goals_Make5Villagers` | training | Training sequence: LT queue modifier for 5 villagers |
| `Goals_BuildHouses` | training | Training sequence: housing limit awareness, place houses |
| `Goals_Scouting` | training | Training sequence: select scout, search area |
| `Goals_ScoutingHerd` | training | Training sequence: return sheep to TC |
| `Goals_ScoutingSecond` | training | Training sequence: assign villager to harvested sheep |
| `Goals_SetBalanced` | training | Training sequence: open VPS menu, set Economic preset |
| `Goals_Research` | training | Training sequence: Find Menu → select mill → research Wheelbarrow |
| `Goals_BuildLandmark` | training | Training sequence: select villager, open landmark radial |
| `Goals_WaitFinish` | training | Training sequence: wait for landmark at 70% then show tip |
| `Salisbury3_TrainingContructionCallback` | training | Log construction phase/blueprint for training predicates |
| `PickConvenientVillager` | training | Find idle on-screen villager for training goal targeting |

## KEY SYSTEMS

### Objectives

**Phase 1 — Get Villagers to Work (`OBJ_VillagersWork`)**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_VillagersWork` | Primary | Parent: complete all villager-work sub-objectives |
| `SOBJ_SelectVillager` | Sub | Select any villager from sg_starting_villagers |
| `SOBJ_GatherFood` | Sub | Gather 10 food (counter: 0/10) |
| `SOBJ_VillagerCommand` | Sub | Train 2 villagers from TC via radial menu |
| `SOBJ_BuildMill` | Sub | Build a Mill near mkr_place_mill |
| `SOBJ_BuildLumber` | Sub | Build a Lumber Camp near mkr_place_lumber_camp |
| `SOBJ_Make5Villagers` | Sub | Queue 5 villagers using LT modifier |
| `SOBJ_BuildHouses` | Sub | Build 2 houses (triggered when pop-capped) |

**Phase 2 — Scout for Sheep (`OBJ_Scout`)** *(skipped if player already harvested 50%+ sheep)*
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Scout` | Primary | Parent: find, herd, harvest sheep |
| `SOBJ_FindSheep` | Sub | Scout locates sheep on map |
| `SOBJ_HerdSheep` | Sub | Bring sheep near TC (within 15 range) |
| `SOBJ_HarvestSheep` | Sub | Kill/harvest at least one sheep |

**Phase 3 — Grow the Town (`OBJ_GrowTown`)**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_GrowTown` | Primary | Parent: mine, farms, assign workers |
| `SOBJ_BuildMine` | Sub | Build a Mining Camp near gold |
| `SOBJ_BuildFarms` | Sub | Build 3 Farms near Mill (counter: 0/3) |
| `SOBJ_AssignVillagers` | Sub | Assign villagers to work 3 farms |

**Phase 4 — Command Officials (`OBJ_CommandOfficials`)**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_CommandOfficials` | Primary | Parent: VPS and research |
| `SOBJ_SetBalanced` | Sub | Choose Economic VPS preset (UI_GetGovernmentRadialWeights) |
| `SOBJ_Research` | Sub | Research Wheelbarrow at Mill/TC |

**Phase 5 — Build Landmark (`OBJ_BuildLandmark`)**
| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_BuildLandmark` | Primary | Parent: place and finish landmark |
| `SOBJ_PlaceLandmark` | Sub | Place Casernes Centrales landmark |
| `SOBJ_WaitFinish` | Sub | Wait for landmark construction to complete → Mission_Complete |

### Objective Flow

```
OBJ_VillagersWork → [if sheep < 50% harvested] OBJ_Scout → OBJ_GrowTown → OBJ_CommandOfficials → OBJ_BuildLandmark → Mission_Complete
                  → [if sheep >= 50% harvested] OBJ_GrowTown (skip scout)
```

### Difficulty

No `Util_DifVar` usage. This is a tutorial with fixed parameters:
- `num_houses = 2`
- `num_farms = 3`
- Production rate: `2x` via `Modify_PlayerProductionRate`
- Construction time multipliers: `0.5x` for most buildings, `0.75x` for farms, `0.25x` for landmark
- Food gather rate: `2x` for starting villagers
- Berry deposit amount: set to 75 per bush
- Starting resources: +300 wood, +140 food, +200 gold (gold added in Mission_Start)
- Research speed: `2x` for Wheelbarrow

### Spawns

No wave/combat spawns. Intro NIS spawns only:
- **Duke William**: 1x `UNIT_DUKE_WILLIAM_CMP_SAL` at mkr_william_intro_spawn
- **Cavalry escort**: 14x `UNIT_HORSEMAN_2_FRE` split into sg_intro_cavalry_a (7) and sg_intro_cavalry_b (7)
- **Scout**: 1x `UNIT_SCOUT_1_FRE` at mkr_scout_intro_spawn
- **Villagers**: 8x `UNIT_VILLAGER_1_FRE` at spawn markers 01–08
- All intro units despawn/destroy after parade sequence

### AI

No AI players. No `AI_Enable`, no encounter plans, no patrol logic. Single-player tutorial only.

### Timers

| Timer Call | Delay | Purpose |
|-----------|-------|---------|
| `Rule_AddOneShot(Salisbury3_StartAssign, 1)` | 1s | Delay after farms built to check if villagers already assigned |
| `Rule_AddInterval(AssignVillagers_Monitor)` | default | Poll worked-farm count until 3 farms staffed |
| `Rule_AddInterval(Mission_Start_WaitForSpeechToFinish, 0.5)` | 0.5s | Wait for intro NIS to finish before starting objectives |
| `Rule_Add(SelectVillager_Monitor)` | per-frame | Check if player selected a villager |
| `Rule_Add(GatherFood_Monitor)` | per-frame | Track food accumulation to 10 |
| `Rule_Add(FindSheep_Monitor)` | per-frame | Check sheep proximity / interactors |
| `Rule_Add(HerdSheep_Monitor)` | per-frame | Check sheep herded to TC area |
| `Rule_Add(HarvestSheep_Monitor)` | per-frame | Check sheep health < 1 |
| `Rule_Add(SetBalanced_Monitor)` | per-frame | Check VPS radial weights changed |
| `Rule_Add(Salisbury3_MonitorResearchObjStart)` | per-frame | Wait for VPS radial closed before starting research |
| `Rule_Add(PlaceLandmark_Monitor)` | per-frame | Detect wonder_dark_age entity placed |
| `Rule_Add(WaitFinish_Monitor)` | per-frame | Detect landmark construction complete |

### Training System

The training file implements **15 goal sequences** for Xbox controller guidance using the `Training_Goal` / `Training_GoalSequence` API. Each sequence:
- Targets specific UI elements (D-pad buttons, radial menus, HUD widgets)
- Uses `CompletePredicate` functions to advance through steps
- Uses `IgnorePredicate` to remove sequences when objectives complete
- Tracks construction phases via `g_training_log` table updated by `Salisbury3_TrainingContructionCallback`
- SMS (Site Menu System) flows for Mine and Farms: deselect → hover resource → open SMS → choose building → place

Key training state flags: `training_mill_placed`, `training_lumber_placed`, `training_mine_placed`, `training_farms_placed`, `training_houses_started`, `training_placing_landmark`, `training_research_started`, `training_mill_selected`.

### Restrictions

All buildings, units, and upgrades start as `ITEM_REMOVED` and are progressively unlocked:
- **SOBJ_SelectVillager PreStart**: Quick commands enabled, site menu disabled
- **SOBJ_VillagerCommand PreStart**: Villager production unlocked
- **SOBJ_BuildMill PreStart**: Mill unlocked
- **SOBJ_BuildLumber PreStart**: Lumber Camp unlocked
- **SOBJ_BuildHouses PreStart**: House unlocked
- **SOBJ_BuildMine PreStart**: Mining Camp unlocked, site menu enabled
- **SOBJ_BuildFarms PreStart**: Farm unlocked
- **SOBJ_SetBalanced PreStart**: VPS widget shown
- **SOBJ_Research PreStart**: Wheelbarrow unlocked, Find Menu shown
- **SOBJ_PlaceLandmark PreStart**: Landmark (Casernes Centrales) unlocked

Construction menu pages `fre_age2` through `fre_age4` and all wonder pages are permanently removed.

## CROSS-REFERENCES

### Imports
| File | Imports |
|------|---------|
| `sal_chp2_womanswork.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar`, `training_sal_chp2_womanswork.scar`, `obj_villagers.scar`, `obj_grow.scar`, `obj_officials.scar`, `obj_scout.scar` |
| `obj_grow.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `obj_officials.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `obj_scout.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `obj_villagers.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `training_sal_chp2_womanswork.scar` | `training.scar`, `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |

### Shared Globals (cross-file)

| Global | Set In | Used In |
|--------|--------|---------|
| `player1` | sal_chp2_womanswork | all files |
| `produced_villagers` | sal_chp2_womanswork (init), obj_villagers (increment) | obj_villagers |
| `eg_mill` | obj_villagers (created on build) | obj_grow, training |
| `eg_lumber` | obj_villagers (created on build) | training |
| `eg_player_tc` | world (prefab) | obj_villagers, training, sal_chp2_womanswork |
| `eg_landmark` | obj_grow (created on place) | training |
| `sg_sheep` | world (prefab) | obj_scout, sal_chp2_womanswork |
| `sg_intro_scout` | sal_chp2_womanswork | obj_scout, training |
| `sg_starting_villagers` | sal_chp2_womanswork | obj_villagers, sal_chp2_womanswork |
| `sg_herded` | sal_chp2_womanswork (init) | obj_scout, training |
| `num_farms` | sal_chp2_womanswork | obj_grow |
| `num_houses` | sal_chp2_womanswork | obj_villagers |
| `starting_sheep` | sal_chp2_womanswork | obj_scout, obj_villagers |
| `g_training_log` | sal_chp2_womanswork (init), training (updated) | training |
| `training_mill_placed` | obj_villagers | training |
| `training_lumber_placed` | obj_villagers | training |
| `training_mine_placed` | obj_grow | training |
| `training_farms_placed` | obj_grow | training |
| `training_houses_started` | obj_villagers | training |
| `training_placing_landmark` | obj_grow | training |
| `training_research_started` | training | training |

### Inter-File Function Calls

- `sal_chp2_womanswork.scar` calls: `VillagersWork_InitObjectives()`, `GrowTown_InitObjectives()`, `CommandOfficials_InitObjectives()`, `Scout_InitObjectives()`, `Salisbury3_TrainingContructionCallback()`, `ChangeBuildTimes()`
- `obj_villagers.scar` calls: `Goals_SelectVillager()`, `Goals_GatherFood()`, `Goals_VillagerCommand()`, `Goals_BuildMill()`, `Goals_BuildLumber()`, `Goals_Make5Villagers()`, `Goals_BuildHouses()` (all in training file)
- `obj_scout.scar` calls: `Goals_Scouting()`, `Goals_ScoutingHerd()`, `Goals_ScoutingSecond()` (all in training file)
- `obj_grow.scar` calls: `Goals_BuildMine()`, `Goals_BuildFarms()`, `Goals_BuildLandmark()`, `Goals_WaitFinish()` (all in training file)
- `obj_officials.scar` calls: `Goals_SetBalanced()`, `Goals_Research()` (all in training file)

### Blueprint References

- **French Buildings**: `BUILDING_ECON_FOOD_CONTROL_FRE` (Mill), `BUILDING_ECON_WOOD_CONTROL_FRE` (Lumber Camp), `BUILDING_ECON_MINING_CAMP_CONTROL_FRE` (Mining Camp), `BUILDING_RESOURCE_FARM_FRE` (Farm), `BUILDING_HOUSE_CONTROL_FRE` (House), `BUILDING_LANDMARK_AGE1_CASERNES_CENTRALES_FRE` (Landmark)
- **French Units**: `UNIT_VILLAGER_1_FRE`, `UNIT_SCOUT_1_FRE`, `UNIT_HORSEMAN_2_FRE`
- **Campaign Units**: `UNIT_DUKE_WILLIAM_CMP_SAL`
- **Gaia**: `GAIA_HERDABLE_SHEEP`
- **Upgrades**: `UPGRADE_UNIT_TOWN_CENTER_WHEELBARROW_1`
