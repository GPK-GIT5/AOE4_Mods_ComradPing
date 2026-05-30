# Mongol Chapter 1: Juyong Gate

## OVERVIEW

**mon_chp1_juyong** is the first Mongol campaign mission set at the Great Wall's Juyong Pass in 1213. The player controls Genghis Khan's Mongol forces (Dark Age, capped at Feudal) against the Jin Dynasty (Feudal). The mission flows through four distinct phases: (1) Scout the approach to Zhangjiakou fortress with scouts, triggering the main army's arrival; (2) Destroy Zhangjiakou's keep with cavalry, receiving reinforcements including villagers and mobile Mongol buildings; (3) Raze Yanqing and optionally destroy three outlying Jin villages to cut off reinforcement waves, while establishing an economy with Mongol-unique mobile structures; (4) Breach the Great Wall by constructing siege engines (rams/siege towers) and razing Juyong's keep. Difficulty scales wave frequency, garrison sizes, and unit counts across all four tiers. The mission features extensive use of the MissionOMatic module system for AI garrisons, roving patrols, wave spawning, and location captures.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp1_juyong.scar | core | Main mission orchestrator: player setup, recipe with all modules/locations, intro/outro sequences, wave system, restrictions, achievements, and phase transitions |
| obj_juyong_phase1.scar | objectives | Phase 1 objectives: scout approach to Zhangjiakou, spawn the Mongol army on scout death or discovery |
| obj_juyong_phase2.scar | objectives | Phase 2 objectives: destroy Zhangjiakou keep, burn/retreat fortress, spawn reinforcements with mobile buildings |
| obj_juyong_phase3.scar | objectives | Phase 3 objectives: raze Yanqing buildings, optional village destruction, burn-resource tracking, village wave management |
| obj_juyong_phase4.scar | objectives | Phase 4 objectives: breach the Great Wall, raze Juyong keep, siege construction counter, outro cinematic setup |
| training_juyong.scar | training | Tutorial goal sequences for Genghis Khan's leader aura, raiding, Ger, pasture, moving buildings, unpacking, Ovoo, improved raiding, blacksmith, siege engineer, and ram construction |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | mon_chp1_juyong.scar | Configures 4 players, ages, relationships, AI disable |
| Mission_SetupVariables | mon_chp1_juyong.scar | Inits SGroups, EGroups, leader, wave timing, all objectives |
| Mission_SetRestrictions | mon_chp1_juyong.scar | Upgrades Jin towers, gives Mongol packing speed upgrade |
| Mission_Preset | mon_chp1_juyong.scar | Buffs Zhangjiakou walls, sets audio, spawns intro units |
| Mission_Start | mon_chp1_juyong.scar | Sets resources to zero, starts Phase 1 objective |
| GetRecipe | mon_chp1_juyong.scar | Returns MissionOMatic recipe with 40+ modules and locations |
| Juyong_OnConstructionComplete | mon_chp1_juyong.scar | Tracks player siege construction for SOBJ_BuildSiege counter |
| Juyong_SpecialChecks | mon_chp1_juyong.scar | Spawns elite temple guards when temple module defeated |
| Init_Waves | mon_chp1_juyong.scar | Creates 5 Wave objects for north/south/yanqing/juyong attacks |
| Juyong_InitPlayerUnits | mon_chp1_juyong.scar | Deploys scouts, intro Khan, mangudai, fleeing villagers |
| Juyong_CheckJuyongKeepDestroyed | mon_chp1_juyong.scar | Monitors Juyong keep; triggers Mission_Complete on raze |
| Juyong_CheckTotalFailure | mon_chp1_juyong.scar | Fails mission if no non-scout units remain |
| Achievement_ScoutDiesAtFrontGate | mon_chp1_juyong.scar | Grants achievement when unit dies to Zhangjiakou tower |
| Juyong_InitObjectives_Phase1 | obj_juyong_phase1.scar | Registers OBJ_Prepare, SOBJ_Scout objectives |
| Juyong_CheckScoutsAlive | obj_juyong_phase1.scar | Spawns Mongol army when all scouts die |
| Juyong_CheckMountainRouteFound | obj_juyong_phase1.scar | Triggers intel when player finds mountain route |
| Juyong_CheckZGateFound | obj_juyong_phase1.scar | Triggers intel when player finds Zhangjiakou gate |
| Juyong_MongolPatrolFound | obj_juyong_phase1.scar | Triggers intel when player spots Jin mountain patrols |
| Juyong_SpawnMongolArmy | obj_juyong_phase1.scar | Deploys 70+ cavalry and Genghis Khan at start marker |
| Juyong_InitObjectives_Phase2 | obj_juyong_phase2.scar | Registers OBJ_Zhangjiakou battle objective |
| Juyong_BurnZhangjiakou | obj_juyong_phase2.scar | Burns fortress, removes wall buffs, converts walls |
| Juyong_CheckZhangjiakouEntered | obj_juyong_phase2.scar | Dissolves wall archers into ZhangjiakouDefend on entry |
| Juyong_RetreatZhangjiakou | obj_juyong_phase2.scar | Evacuates defenders as RovingArmies to Midfield |
| Juyong_InitObjectives_Phase3 | obj_juyong_phase3.scar | Registers Yanqing/village/raid objectives, starts waves |
| Juyong_GetBurnableList | obj_juyong_phase3.scar | Builds list of burnable Jin buildings for raid tracking |
| Juyong_IsBurnableBurning | obj_juyong_phase3.scar | Monitors burning, awards raid bounty based on upgrades |
| Juyong_RecallAllJinSoldiers | obj_juyong_phase3.scar | Retreats all remaining Jin modules to Juyong fortress |
| Juyong_SendToJuyong | obj_juyong_phase3.scar | Converts a module into retreating RovingArmy toward Juyong |
| Juyong_OnEntityDestroyed | obj_juyong_phase3.scar | Updates village/Yanqing destruction counters on building kill |
| Juyong_SendWave | obj_juyong_phase3.scar | Prepares and launches a wave targeting player's TC |
| Juyong_UpdateMonTC | obj_juyong_phase3.scar | Tracks player TC position, updates wave targets, fails if destroyed |
| Juyong_FirstVillageDestroyed | obj_juyong_phase3.scar | Triggers intel event on first village destruction |
| Juyong_InitObjectives_Phase4 | obj_juyong_phase4.scar | Registers OBJ_Juyong, SOBJ_RazeKeepJuyong, SOBJ_BuildSiege |
| Juyong_GroupWallsForObjectives | obj_juyong_phase4.scar | Filters Great Wall entities for breach detection |
| Juyong_CheckGreatWallBreached | obj_juyong_phase4.scar | Detects wall breach, destroys gate, removes Juyong wave |
| Juyong_ShowGreatWall | obj_juyong_phase4.scar | Reveals Great Wall FOW when player approaches |
| Juyong_InitOutro | obj_juyong_phase4.scar | Spawns outro cavalry procession through Juyong gate |
| Juyong_SendOutroUnits | obj_juyong_phase4.scar | Moves outro units along waypoint marker lists |
| Modify_SetUnitMaxSpeed | obj_juyong_phase4.scar | Applies speed modifier to all squads in a group |
| Joyong_CheatToObjective | obj_juyong_phase4.scar | Debug: skips to Phase 4, spawns army with rams |
| Juyong_RetreatOffMap | obj_juyong_phase3.scar | Trims excess retreated Jin units by sending off-map |
| MissionTutorial_JuyongLeaderAura | training_juyong.scar | Tutorial: select Genghis Khan and view Signal Arrow ability |
| MissionTutorial_JuyongLeaderAura_Xbox | training_juyong.scar | Xbox controller variant of leader aura tutorial |
| MissionTutorial_JuyongRaiding | training_juyong.scar | Tutorial: attack enemy buildings to set them on fire |
| MissionTutorial_JuyongGer | training_juyong.scar | Tutorial: explains Ger (Mongol house) when on screen |
| MissionTutorial_JuyongPasture_Entity | training_juyong.scar | Tutorial: explains pasture building when on screen |
| MissionTutorial_JuyongPasture_Squad | training_juyong.scar | Tutorial: explains mobile pasture squad when on screen |
| MissionTutorial_JuyongMovingBuildings | training_juyong.scar | Tutorial: pack an unpacked building to learn mobility |
| MissionTutorial_JuyongUnpackBuildings | training_juyong.scar | Tutorial: unpack buildings near Zhangjiakou |
| MissionTutorial_JuyongOvoo | training_juyong.scar | Tutorial: build Ovoo near stone deposit |
| MissionTutorial_ImprovedRaiding | training_juyong.scar | Tutorial: research Improved Raiding at outpost |
| MissionTutorial_Blacksmith | training_juyong.scar | Tutorial: build blacksmith with villager |
| MissionTutorial_SiegeEngineer | training_juyong.scar | Tutorial: research siege engineering at blacksmith |
| MissionTutorial_SiegeEngineer_Xbox | training_juyong.scar | Xbox controller variant of siege engineer tutorial |
| MissionTutorial_Ram | training_juyong.scar | Tutorial: select infantry and build a ram |

## KEY SYSTEMS

### Objectives

| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Prepare | Primary | 1 | Plan attack — complete when scouts find forest post or keep |
| SOBJ_Scout | Primary (sub) | 1 | Scout the approach to Zhangjiakou |
| OBJ_Zhangjiakou | Battle | 2 | Destroy the keep at Zhangjiakou fortress |
| OBJ_Yanqing | Battle | 3 | Raze Yanqing — complete when all buildings destroyed |
| SOBJ_YanqingBuildings | Battle (sub) | 3 | Destroy buildings in Yanqing (progress bar) |
| OBJ_RaidBuildings | Optional | 3 | Collect 2000 resources by burning Jin buildings |
| OBJ_DestroyVillages | Optional | 3 | Destroy 3 outlying Jin villages (counter 0/3) |
| SOBJ_Village_1 | Optional (sub) | 3 | Destroy Western Village (6 buildings) |
| SOBJ_Village_2 | Optional (sub) | 3 | Destroy Southern Village (8 buildings) |
| SOBJ_Village_3 | Optional (sub) | 3 | Destroy Northern Village (9 buildings) |
| OBJ_Juyong | Primary | 4 | Breach the Great Wall |
| SOBJ_RazeKeepJuyong | Primary (sub) | 4 | Raze Juyong's keep to win the mission |
| SOBJ_BuildSiege | Primary (sub) | 4 | Construct 4 siege engines (rams or siege towers) |
| OBJ_DebugComplete | Primary | — | Debug: force-completes by destroying Great Wall gate |

**Win condition:** Raze Juyong keep (SOBJ_RazeKeepJuyong complete) → `Mission_Complete()`.
**Lose conditions:** All non-scout units lost (`Juyong_CheckTotalFailure`) OR player TC destroyed (`Juyong_UpdateMonTC`) → `Mission_Fail()`.

### Difficulty

| Parameter | Easy → Expert | What it scales |
|-----------|---------------|----------------|
| yanqingWavePeriod | 570 → 270s | Interval between Yanqing attack waves |
| northWavePeriod | 570 → 270s | Interval between North village attack waves |
| south1WavePeriod | 570 → 270s | Interval between South1 village attack waves |
| south2WavePeriod | 570 → 270s | Interval between South2 village attack waves |
| juyongWavePeriod | 570 → 270s | Interval between Juyong sortie waves |
| wave_north units | 3 → 5+6 spearmen | North wave base squad count per spawn |
| wave_south1 units | 3 → 5+6 archers | South1 wave base squad count per spawn |
| wave_south2 units | 3 → 5+6 spearmen | South2 wave base squad count per spawn |
| wave_yanqing units | 2+3 → 4+5+5+5 spear/archer | Yanqing wave mixed composition |
| wave_juyong units | 3+4 → 6+8+5+5 spear/xbow | Juyong wave mixed composition |
| Reinforcement villagers | 14 → 10 | Fewer villagers on harder difficulties |
| YanqingPatrol extra | 0 → +5+5 | Extra spear/archer squads at Hard/Expert |
| SouthPatrol extra | 0 → +4+4+5+5 | Extra horseman/spear squads at Hard/Expert |
| NorthPatrol extra | 0 → +3+3+5+5 | Extra spear/archer squads at Hard/Expert |
| ZhangjiakouDefend extra | 0 → +3+2+3+3 | Extra spear/archer squads at Hard/Expert |
| Wall archer garrisons | 3 → 3+1+1 | Extra archers per wall section at Hard/Expert |
| JinYanqing4/5 xbows | 2+2 → +2+2+2+2 | Extra repeater crossbow/archers at Yanqing |
| JinJuyong manatarms | 6 → +4+4 | Extra men-at-arms and crossbows at Juyong |
| Yanqing waves skip | Story mode | Yanqing waves disabled on Easy/Story difficulty |

### Spawns

**Intro Sequence:** 2 scouts deployed at separate markers, Genghis Khan (intro player) and 2 mangudai ride along waypoints, 3 groups of Jin villagers flee toward Zhangjiakou. Intro cleans up after 23 seconds.

**Mongol Army (Phase 1→2):** On scout death or discovery, spawns 20 knights, 20 horsemen, 30 horse archers, and Genghis Khan at `start_mongol`.

**Reinforcements (Phase 2→3):** On Zhangjiakou keep destruction, spawns 10-14 villagers (difficulty-scaled), 16 archers, 16 spearmen, plus mobile Mongol buildings (TC, house, infantry barracks, 2 pastures).

**Village Waves (Phase 3):** Five wave sources — North (spearmen), South1 (archers), South2 (spearmen), Yanqing (mixed spear/archer), Juyong (spear + repeater crossbow). Waves start on staggered delays (210s–660s) and repeat at difficulty-scaled intervals (270–570s). Each wave stages at its village's defend module, then launches as a RovingArmy targeting the player's TC position. Village destruction stops that source's waves.

**Juyong Sortie (Phase 4):** After Yanqing completion, Juyong spawns periodic waves (spear + repeater crossbow) targeting Yanqing.

**Outro:** 10 knight squads, 6 horseman squads, 4 horse archer squads, archers, spearmen, and villagers deployed along Juyong road markers at speed 6.

### AI

- `AI_Enable(g_playerNeutral, false)` — neutral holder player has no AI
- **Jin AI is entirely module-driven** via MissionOMatic:
  - **Defend modules (20+):** JinForestPost, JinPostZhangjiakou1, ZhangjiakouRetreaters, ZhangjiakouDefend, 8× wall archer garrisons (North/South 1-4), NorthDefend (1-3), South1/2Defend, MidfieldDefend (1-3), JinYanqing (1-5), JinJuyong (1-3), JinJuyongWallNorth/South, JinJuyongExternal (1-4), JinJuyongReinforce, TempleGuards
  - **RovingArmy patrols (7):** YanqingPatrol, SouthPatrol, NorthPatrol, FieldPatrol1, FieldPatrol3, MountainPatrol1, MountainPatrol2
  - **Withdraw behavior:** Forest post defenders withdraw to Zhangjiakou on sight; road posts 1-2 withdraw to Juyong; mountain/north patrols fall back to Juyong
  - **Dynamic retreat:** On Zhangjiakou capture, all remaining Defend modules are converted to RovingArmy modules and sent to Midfield; on Yanqing completion, `Juyong_RecallAllJinSoldiers()` sends all surviving modules to Juyong via `Juyong_SendToJuyong()`
  - **Overflow management:** `Juyong_RetreatOffMap()` thins retreated Juyong garrison above 30 squads
- **TownLife modules:** ZhangjiakouFortressTownlife, YanquingTownLife (zero population)
- **VillagerLife instances:** 8 instances (north, south1-4, yan, zhang, midfield) stopped during cheat skip

### Timers

| Timer/Rule | Delay/Interval | Purpose |
|------------|----------------|---------|
| Rule_AddOneShot(Juyong_SendIntroUnits, 10s) | 10s | Move scouts to waypoint 2 |
| Rule_AddOneShot(Juyong_SendIntroUnits, 14-18s) | 14-18s | Move Khan/mangudai along intro path |
| Rule_AddOneShot(Juyong_CleanUpIntro, 23s) | 23s | Destroy intro units |
| Rule_AddInterval(Juyong_CheckJuyongKeepDestroyed, 1s) | 1s | Early mission complete check |
| Rule_AddInterval(Juyong_CheckScoutsAlive, 1s) | 1s | Detect all scouts dying |
| Rule_AddInterval(Juyong_CheckMountainRouteFound, 2s) | 2s | Scout proximity to mountain route |
| Rule_AddInterval(Juyong_CheckZGateFound, 2s) | 2s | Scout proximity to Zhangjiakou gate |
| Rule_AddInterval(Juyong_MongolPatrolFound, 2s) | 2s | Detect Jin mountain patrol sighting |
| Rule_AddInterval(Juyong_ShowGreatWall, 2s) | 2s | FOW reveal when player nears Great Wall |
| Rule_AddInterval(Juyong_ApproachGreatWall, 2s) | 2s | Play music stinger on approach |
| Rule_AddInterval(Juyong_CheckGreatWallBreached, 2s) | 2s | Detect wall destruction and trigger breach |
| Rule_AddInterval(Juyong_CheckZhangjiakouEntered, 2s) | 2s | Dissolve wall modules when player enters fortress |
| Rule_AddInterval(Juyong_CheckMongolTCDestroyed, 5s) | 5s | Monitor player TC; fail if destroyed |
| Rule_AddInterval(Juyong_CheckPlayerApproachYanqing, 5s) | 5s | Start Yanqing building sub-objective on proximity |
| Rule_AddInterval(Juyong_CheckPlayerApproachVillage 1/2/3, 5s) | 5s | Start village sub-objectives on proximity |
| Rule_AddOneShot(Juyong_StartYanqingWaves, 210s) | 210s | Begin Yanqing wave spawning |
| Rule_AddOneShot(Juyong_StartSouth1Waves, 360s) | 360s | Begin South1 village wave spawning |
| Rule_AddOneShot(Juyong_StartNorthWaves, 540s) | 540s | Begin North village wave spawning |
| Rule_AddOneShot(Juyong_StartSouth2Waves, 660s) | 660s | Begin South2 village wave spawning |
| Rule_AddInterval(Juyong_*Wave, 270-570s) | varies | Repeated wave dispatch per difficulty |
| Rule_AddInterval(Juyong_JuyongWave, 270-570s) | varies | Post-Yanqing Juyong sortie waves |
| Rule_AddInterval(Juyong_IsBurnableBurning, 0.125s) | 125ms | Fast poll for burning buildings (raid resources) |
| Rule_AddInterval(Juyong_MoveBuildingsHint, 45s) | 45s | Prompt player to move mobile buildings after Yanqing |
| Rule_AddInterval(Juyong_RetreatOffMap, 10s) | 10s | Trim excess Jin units at Juyong above 30 |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (locations, modules, objectives, waves)
- `obj_juyong_phase1.scar` → imports `obj_juyong_phase2.scar` → imports `obj_juyong_phase3.scar` → imports `obj_juyong_phase4.scar` (chained)
- `training_juyong.scar` — imported by main script
- `training/campaigntraininggoals.scar` — base training goal predicates and utilities

### Shared Globals
- `g_playerMongol`, `g_playerJin`, `g_playerNeutral`, `g_playerIntro` — player handles used across all files
- `g_leaderGenghisKhan` — leader unit initialized via `Missionomatic_InitializeLeader()`, used in training and combat
- `sg_allsquads`, `eg_allentities` — MissionOMatic scratch groups used by `Player_GetAll()`
- `eg_zhangjiakou_keep`, `eg_juyong_keep`, `eg_yanqing`, `eg_village_1/2/3` — EGroups shared for objective completion checks
- `assaultWaveList` — table of active wave assault modules, updated by `Juyong_SendWave()` and `Juyong_UpdateMonTC()`
- `mon_tc_position` — dynamically tracked player TC position, target for all attack waves
- `burnResourcesClaimed` — running total of raid bounty, shared between `Juyong_IsBurnableBurning` and objective counter
- `scout_phase_complete`, `scouts_dead` — phase transition flags shared between Phase 1 objectives and failure check

### Inter-File Function Calls
- Main script calls `Juyong_InitObjectives_Phase1/2/3/4()` from `Mission_SetupVariables()`
- Phase 1 `OnComplete` → starts `OBJ_Zhangjiakou` (Phase 2)
- Phase 2 `OnComplete` → starts `OBJ_Yanqing` (Phase 3) via intel event
- Phase 3 `OnComplete` → starts `OBJ_Juyong` (Phase 4), calls `Juyong_RecallAllJinSoldiers()`
- Phase 4 `OnStart` → calls `MissionTutorial_Blacksmith()`, `MissionTutorial_SiegeEngineer()`, `MissionTutorial_Ram()` from training file
- Phase 2 `OnStart` → calls `MissionTutorial_JuyongLeaderAura()`, `MissionTutorial_JuyongRaiding()` from training file
- Phase 3 `OnStart` → calls `MissionTutorial_JuyongGer()`, `MissionTutorial_JuyongPasture_*()`, `MissionTutorial_JuyongUnpackBuildings()`, `MissionTutorial_ImprovedRaiding()` from training file
- `Juyong_GroupWallsForObjectives()` in Phase 4 file, called from `Mission_Preset()` in main
- `Juyong_CheckTotalFailure()` in main, referenced as `IsFailed` callback across all phase objectives
- `Wave_New()`, `Wave_Prepare()`, `Wave_OverrideUnitBuildTime()` — MissionOMatic wave system
- `RovingArmy_Init()`, `TransferModuleIntoModule()`, `DissolveModuleIntoModule()` — MissionOMatic module management
- `Missionomatic_SetGateLock()`, `Location_Capture()`, `Capture_Location()` — MissionOMatic location system

### Blueprint References
- `EBP.CHINESE.BUILDING_DEFENSE_TOWER_CHI` — Jin tower filter
- `EBP.CHINESE.BUILDING_DEFENSE_OUTPOST_CHI` — Jin outpost filter
- `EBP.CHINESE.BUILDING_DEFENSE_GREATWALL_GATE_CMP_CHI` — Great Wall gate (debug)
- `EBP.MONGOL.BUILDING_HOUSE_MON` — Ger (training tutorial)
- `EBP.MONGOL.BUILDING_PASTURE_MON` / `BUILDING_PASTURE_MOVING_MON` — Pasture (training)
- `EBP.MONGOL.BUILDING_STONE_DEPOSIT_OVOO_MON` — Ovoo (training)
- `EBP.MONGOL.BUILDING_TECH_UNIT_INFANTRY_MON` — Blacksmith (training)
- `UPG.MONGOL.UPGRADE_RAID_BOUNTY_MON` / `UPGRADE_RAID_BOUNTY_IMPROVED_MON` — Raid bounty tiers (50→150→175 per building ×3)
- `UPG.MONGOL.UPGRADE_IMPROVED_SIEGE_ENGINEERS_MON` — removed from player initially, granted in cheat
- `UPG.COMMON.UPGRADE_TOWER_CANNON` — instant upgrade on Jin towers
- `UPG.COMMON.UPGRADE_TECH_UNIVERSITY_MURDER_HOLES_4` — Jin murder holes
- `unit_genghis_khan_cmp_mon` — campaign Genghis Khan squad blueprint
- `leader_improved_armor_maneuver_arrow` — Genghis Khan's Signal Arrow ability
