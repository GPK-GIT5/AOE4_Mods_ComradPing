# Hundred Years War Chapter 1: Paris

## OVERVIEW

The "Paris" mission is a Hundred Years War Chapter 1 campaign scenario where the player defends Paris (French, player1) against an English siege (player2). The mission has two major phases: an **Invasion** phase where English roving armies advance along 3 lanes destroying outlying targets, and a **Siege** phase where 8 timed assault waves (with bonus flanking waves on waves 4, 6, 8) attack the city walls using rams, siege towers, and trebuchets. Both players start in Castle Age. The player must retreat outlying villagers, prepare defenses during a build-up window, then survive all 8 waves. Victory requires killing all wave units; defeat occurs if the player's landmarks are destroyed. Difficulty (Story/Easy/Normal/Hard) scales starting resources, unit counts in every composition, and siege equipment quantities.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp1_paris.scar` | core | Main mission script: imports sub-files, player setup, preset upgrades/modifiers, resource grants, starts invasion/siege timers, monitors waves, reinforcement logic, villager retreat, intro/outro choreography, UI callbacks. |
| `hun_chp1_paris_data.scar` | data | Initializes all globals: invasion/siege timers, lane tracking arrays, marker tables, SGroup creation, wave_info structs, MissionOMatic module references, and all unit composition tables (per-difficulty). |
| `hun_chp1_paris_objectives.scar` | objectives | Defines and registers OBJ_Defend, OBJ_Defeat, OBJ_Prepare, and OBJ_Retreat with fail/complete/counter logic. |
| `hun_chp1_paris_training.scar` | training | Tutorial goal sequences for researching Incendiary Arrows at the Arsenal and repairing damaged buildings. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Paris_InitData1` | data | Initializes all globals, markers, SGroups, lane arrays |
| `Paris_InitData2` | data | Resolves MissionOMatic module references for invaders/standby/defenders |
| `LoadUnitTables` | data | Defines all difficulty-scaled unit compositions for all phases |
| `GetRecipe` | data | Returns MissionOMatic recipe with all spawners and modules |
| `Paris_SetupWaves` | data | Creates Wave objects for 3 lanes with staging/assault data |
| `Mission_SetupPlayers` | core | Configures player1 (French) and player2 (English), Castle Age |
| `Mission_Preset` | core | Applies upgrades, modifiers, assigns villagers, starts intro |
| `Mission_Start` | core | Grants resources, starts objectives, adds invasion/monitor rules |
| `Paris_InvasionStart` | core | Triggers staggered 3-lane invasion with delays |
| `Paris_InvasionStartLane` | core | Activates roving army targets for a specific lane |
| `Paris_InvasionStartStone` | core | Spawns stone-resource raider module |
| `Paris_InvasionStartGold` | core | Spawns gold-resource raider module |
| `Paris_StrongerInvaders` | core | Adds 1 ram to all invader/standby compositions over time |
| `Paris_LaneHalfComplete` | core | Triggers standby spawns and defenders when lane half-cleared |
| `Paris_LaneComplete` | core | Tracks lane completion; triggers siege transition at 3/3 |
| `Paris_InvasionComplete` | core | Moves defenders/staging forward, schedules siege start |
| `Paris_StartSiege` | core | Schedules all 8 waves with prepare/launch timers |
| `Paris_Prepare` | core | Spawns and positions main wave + bonus waves at staging |
| `Paris_PrepareBonus` | core | Spawns bonus flanking wave on a secondary lane |
| `Paris_Launch` | core | Launches assault wave, adds threat arrow UI |
| `Paris_LaunchBonus` | core | Launches bonus wave on secondary lane |
| `Paris_MonitorWaves` | core | Checks wave SGroups for death, triggers intel/completion |
| `Paris_CalculateUnitsKilled` | core | Updates OBJ_Defeat progress bar from kill counts |
| `Paris_MonitorReinforcements` | core | Round-robin checks modules for reinforcement needs |
| `Paris_ReinforceFromMapEdge` | core | Spawns replacement units from map edge for a module |
| `Paris_ReinforceDynamically` | core | Reinforces invaders from standby pool or map edge |
| `MonitorDynamicReinforcements` | core | Merges reinforcements into parent module when nearby |
| `Paris_PreVictoryInvader` | core | Tracks lane victories, triggers half/standby/complete states |
| `Paris_OnCompleteInvader` | core | Switches invader to reverse patrol after targets cleared |
| `Paris_MoveUpDefenders` | core | Repositions 15 siege defenders to forward positions |
| `Paris_MoveUpStaging` | core | Advances staging modules to final siege positions |
| `Paris_MoveIntroUnits` | core | Choreographs intro unit movements to walls and gates |
| `Paris_MoveGateArchers` | core | Moves gate archers after horsemen reach destination |
| `Paris_InitOutro` | core | Spawns and positions all outro cinematic units |
| `Paris_AddWaveUI` | core | Creates threat arrow on assault wave SGroup |
| `WallsBreached` | core | Triggers intel event when walls first destroyed |
| `LandmarkUnderAttack` | core | Triggers intel event when landmark first damaged |
| `Paris_InitObjectives` | objectives | Registers OBJ_Defend, OBJ_Defeat, OBJ_Prepare, OBJ_Retreat |
| `Wallingford_RetreatDeath` | objectives | Fails OBJ_Retreat if retreat villagers die |
| `Paris_AddHintIncendiaryArrows` | training | Adds tutorial sequence for researching fire arrows |
| `Paris_AddHintToRepair` | training | Adds tutorial sequence for repairing damaged buildings |
| `ResearchFireArrowsTrigger` | training | Checks if Arsenal is on-screen to start hint |
| `BuildingIsDamaged` | training | Checks for damaged buildings near repair hint marker |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Defend` | Primary (Battle) | Defend Paris — fails if all landmarks destroyed. Top-level objective. |
| `OBJ_Defeat` | Sub-objective (Battle) | Defeat all 8 English attack waves. Progress bar tracks % units killed. Victory trigger. |
| `OBJ_Prepare` | Sub-objective (Info) | Prepare for siege — completes automatically 25s after invasion ends, then starts OBJ_Defeat. |
| `OBJ_Retreat` | Optional | Retreat outlying villagers to safety. Counter tracks villagers reaching `mkr_retreat`. Fails if any die. Awards `CE_PARISVILLAGERRETREAT` challenge event on success. |

### Difficulty

All values are `Util_DifVar({Story, Easy, Normal, Hard})`:

| Parameter | Story | Easy | Normal | Hard | What it scales |
|-----------|-------|------|--------|------|---------------|
| Starting resources (each) | 400 | 300 | 200 | 100 | Food/Wood/Stone/Gold |
| Invader MAA per lane | 11 | 13 | 18 | 26 | Initial invasion force size |
| Standby MAA (lane 1/3) | 15 | 18 | 27 | 39 | Standby reinforcement pool |
| Standby MAA (lane 2) | 10 | 12 | 18 | 26 | Standby reinforcement pool |
| Stone/Gold raider MAA | 6 | 7 | 10 | 14 | Resource-denial raider group |
| Fort defenders (MAA) | 6 | 7 | 10 | 14 | Siege camp garrison MAA |
| Fort defenders (xbow) | 6 | 7 | 10 | 14 | Siege camp garrison crossbowmen |
| Fort defenders (springald) | 1 | 2 | 3 | 4 | Siege camp garrison springalds |
| Siege defenders (archer) | 5 | 6 | 8 | 10 | Field defender archers |
| Siege defenders (spearman) | 5 | 6 | 8 | 10 | Field defender spearmen |
| Ram passenger count | 10 | 10 | 10 | 10 | Troops loaded in rams |
| Siege tower passenger count | 3 | 4 | 6 | 8 | Troops loaded in siege towers |
| Gold villagers (extra) | 4 | 2 | 1 | 0 | Player starting gold villagers |
| Stone villagers (extra) | 4 | 2 | 1 | 0 | Player starting stone villagers |
| Wood villagers (extra) | 5 | 2 | 1 | 0 | Player starting wood villagers |
| Wave compositions | Smallest | Small | Medium | Large | Total units per wave (see Spawns) |

### Spawns

**Invasion Phase (3-lane):**
- 3 `RovingArmy` invader modules attack along marker chains (5-6 targets per lane)
- 3 `RovingArmy` standby modules reinforce invaders after lane half-completion
- 2 resource raiders (`invader_stone`, `invader_gold`) spawn when their associated lane reaches half
- Invaders get +1 ram added to all compositions at 200s, 400s, and 600s via `Paris_StrongerInvaders`
- Lane completion requires clearing all invader targets (6/5/5 per lane = 16 total)
- After all 3 lanes complete, 50s delay before siege begins

**Siege Phase (8 waves + bonus):**
- 8 main waves on cumulative timers: 0, 105, 210, 345, 450, 555, 690, 795 seconds
- Waves 1-3 pre-positioned during invasion; waves 4-8 prepared 180s before launch
- 3 Wave objects (one per lane), waves assigned to shuffled lane order
- Each wave uses staging → assault pipeline via `Wave_Prepare` / `Wave_Launch`
- Bonus waves on waves 4, 6, 8 attack secondary lanes simultaneously

**Wave compositions (Normal difficulty example):**

| Wave | Main Units | Siege |
|------|-----------|-------|
| 1 | 15 spearmen + 15 MAA | 1 ram |
| 2 | 12 MAA | 1 siege tower |
| 3 | 18 MAA | 2 siege towers |
| 4 | 12 archers + 12 spearmen | 1 trebuchet + 1 springald |
| 5 | 12 knights + 24 MAA | 3 rams |
| 6 | 15 spearmen + 15 crossbowmen | 3 rams |
| 7 | 16 archers + 16 spearmen | 3 trebuchets |
| 8 | 16 spearmen + 16 archers | 3 rams |

### AI

- **No AI_Enable calls** — all enemy behavior is scripted via MissionOMatic modules
- **3 UnitSpawner** modules (`spawn_1/2/3`) at map edges with `spawnRate = 0.25`, `onlyRespondToTargetedRequests = true`
- **3 Defend** modules (`siege_camp_1-3_defend`) garrison siege camps with `fort_defender_units`, self-reinforce at 100% threshold
- **3 RovingArmy invaders** (`invader_1/2/3`) with `preVictoryFunction` tracking lane progress; switch to reverse patrol on target completion
- **3 RovingArmy standby** (`standby_1/2/3`) reinforce from map edge; act as reserve pool for dynamic reinforcement
- **15 RovingArmy siege defenders** (`siege_defend_1-15`, 5 per lane) with `leashRange = 45`, `attackMoveAtTarget = attackEverything`, reinforce at 80% threshold
- **2 resource raiders** (`invader_stone`, `invader_gold`) attack player resource locations, reverse patrol on completion
- **Reinforcement system**: round-robin `Paris_MonitorReinforcements` (1s interval) checks each module; `Paris_ReinforceDynamically` pulls from standby pool first, falls back to map-edge spawning; `Paris_ReinforceFromMapEdge` spawns missing units as new RovingArmy that merges into parent
- **Modifiers applied to player2**: trebuchet range ×0.8, archer speed ×1.13, siege weapon speed upgrade pre-completed

### Timers

| Timer | Type | Delay | Purpose |
|-------|------|-------|---------|
| `Paris_MoveIntroUnits` | OneShot | 0.25s | Choreograph intro unit positioning |
| `Paris_InvasionStart` | OneShot | 20s | Begin 3-lane invasion |
| `Paris_InvasionStartLane` (lane 1) | OneShot | 20s (INVASION_DELAY_1) | Start lane 1 invaders |
| `Paris_InvasionStartLane` (lane 2) | OneShot | 0s (INVASION_DELAY_2) | Start lane 2 invaders |
| `Paris_InvasionStartLane` (lane 3) | OneShot | 10s (INVASION_DELAY_3) | Start lane 3 invaders |
| `Paris_StrongerInvaders` | OneShot | 200s, 400s, 600s | Add rams to all invader compositions |
| `Paris_StartNewObjective` | OneShot | 25s (post-invasion) | Complete OBJ_Prepare |
| `Paris_StartSiege` | OneShot | 50s (post-invasion) | Begin siege wave scheduling |
| `Paris_MainLoop` | Interval | 1s | Increment mission clock counter |
| `Paris_MonitorReinforcements` | Interval | 1s | Round-robin reinforce check |
| `Paris_MonitorWaves` | Interval | 1s | Check wave death / update progress |
| `Paris_MoveGateArchers` | Interval | 0.5s | Move gate archers when horsemen arrive |
| `MonitorDynamicReinforcements` | Interval | 4s | Check reinforcement proximity to merge |
| `Paris_AutoSave` | OneShot | 6s (after wave 4 & 7 launch) | Trigger autosave at key moments |
| `WAVE_INTERVALS[1-8]` | OneShot (siege-relative) | 0/105/210/345/450/555/690/795s | Launch each siege wave |
| `PREPARE_TIME` | Offset | 180s before launch | Spawn wave units before assault |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (RovingArmy, Wave, UnitSpawner, Defend modules)
- `training.scar` — base training/tutorial system
- `training/campaigntraininggoals.scar` — shared campaign training utilities (e.g., `CampaignTraining_TimeoutIgnorePredicate`, `AShortPeriodOfTimeHasPassed`)
- `hun_chp1_paris_data.scar` — data file (imported by core)
- `hun_chp1_paris_objectives.scar` — objectives file (imported by core)
- `hun_chp1_paris_training.scar` — training file (imported by core)

### Shared Globals
- `player1`, `player2` — set in `Mission_SetupPlayers`, used across all files
- `eg_landmarks` — entity group for player landmarks (fail condition)
- `eg_paris_walls` — entity group for walls (breach detection)
- `wave_info[1-8]` — wave state tracking structs shared between data init and core monitoring
- `paris_waves[1-3]` — Wave objects used in prepare/launch/monitor pipeline
- `assault_lane_order` — shuffled lane assignment, re-shuffled per wave tier
- `invader_modules[1-3]`, `standby_modules[1-3]` — MissionOMatic module references
- `retreat_count`, `retreat_count_max`, `sg_retreat` — villager retreat tracking for OBJ_Retreat
- All unit composition tables (`invader_units`, `standby_units`, `wave_units`, `wave_units_bonus`, etc.)

### Inter-File Function Calls
- `core` → `data`: `Paris_InitData1()`, `Paris_InitData2()`, `Paris_SetupWaves()`, `LoadUnitTables()` (called within InitData1)
- `core` → `objectives`: `Paris_InitObjectives()`
- `core` → `training`: `Paris_AddHintToRepair()` (from `Mission_Start`), `Paris_AddHintIncendiaryArrows()` (likely from objectives/intel)
- `objectives` → `core`: references `Paris_CalculateUnitsKilled()` in OBJ_Defeat.SetupUI
- `data` → `core`: `GetRecipe()` references `Paris_PreVictoryInvader`, `Paris_OnCompleteInvader`, `Paris_OnCompleteStone`, `Paris_OnCompleteGold`, `Paris_OnCompleteStaging`, `Paris_GetDefenderTargets` as callback functions

### MissionOMatic Module Dependencies
- `Wave_New`, `Wave_Prepare`, `Wave_Launch`, `Wave_SetUnits`, `Wave_FindWave` — wave pipeline system
- `RovingArmy_Init`, `RovingArmy_SetTargets`, `RovingArmy_AddTarget`, `RovingArmy_AddTargets`, `RovingArmy_SetTarget`, `RovingArmy_RemoveSGroup`, `RovingArmy_AddSGroup` — army management
- `SpawnUnitsToModule`, `DissolveModuleIntoModule`, `Reinforcement_SetIdealComposition` — unit lifecycle helpers
- `UnitTable_CountUnits`, `UnitTable_AddUnitsByType`, `UnitTable_RemoveUnits`, `UnitTable_GenerateFromSGroup`, `UnitTable_CountUnitsOfType` — composition utilities
- `MissionOMatic_FindModule` — runtime module lookup by descriptor string

### Notable Events Referenced
- `EVENTS.Intro`, `EVENTS.Victory`, `EVENTS.ManTheWalls`, `EVENTS.EnglishAppear`, `EVENTS.EnglishSlowed`, `EVENTS.Village_Destroyed`, `EVENTS.Village_Remains`, `EVENTS.FirstAssault`, `EVENTS.Wave1_Complete`, `EVENTS.Wave4_Complete`, `EVENTS.Wave6_Complete`, `EVENTS.WallsBreached`, `EVENTS.LandmarkAttack`, `EVENTS.DefendParis`
