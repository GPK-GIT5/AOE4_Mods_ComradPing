# Rogue Maps & UGC

## OVERVIEW

The Rogue mode maps are a set of roguelike survival scenarios in Age of Empires IV where players defend a wonder against escalating enemy waves while exploring the map for points of interest (POIs), resources, and allied units. Each map has a distinct theme—coastal/naval (Coastline), forest/bandits (Forest), Japanese feudal warfare (Daimyo), and Mongol steppe cavalry (Steppe)—but all share common infrastructure via `rogue/rogue.scar` and the MissionOMatic framework. Maps feature lane-based wave attacks, tiered POI reward systems, difficulty-scaled spawns, and secondary threats (pirates, bandits, raiders). Two additional scripts serve as test/debug harnesses: `rogue_stamps` for stamp testing and `rogue_system_test` for champion and boss unit combat testing. A separate UGC template map demonstrates a simpler objective-driven mission structure (capture town → destroy buildings) using the MissionOMatic recipe system without rogue-mode mechanics.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `rogue_coastline_data.scar` | data | Defines coastal, naval, and Byzantine POI type tables with reward values and unit compositions |
| `rogue_coastline_pirates.scar` | spawns | Naval pirate raid army initialization, ship spawning, and transport landing system |
| `rogue_coastline.scar` | core | Main coastline map setup: lanes, outlaws, POIs, naval raids, side bases, resource spots |
| `rogue_forest_data.scar` | data | Defines forest-themed POI types (lumber camp, hunting grounds) |
| `rogue_forest.scar` | core | Forest map setup: bandit camps, outlaw raids, relics, naval lockout, wolf spawns |
| `rogue_japanese_daimyo.scar` | core | Japanese Daimyo map: shinobi mechanics, day/night cycle, abandoned village trap, lane validation |
| `rogue_mongol_steppe_raiders.scar` | spawns | Steppe raider AI: horse archer economy, raid targeting, idle recovery system |
| `rogue_mongol_steppe.scar` | core | Steppe map setup: cavalry-focused waves, guard patrols, site spawning by distance |
| `rogue_stamps.scar` | other | Stamp placement test map; minimal gameplay, FOW revealed |
| `rogue_system_test_data.scar` | data | Test data for all 12 boss units and champion combat with bodyguard compositions |
| `rogue_system_test.scar` | other | System test map for spawning champions/bosses in controlled combat scenarios |
| `obj_capture_town.scar` | objectives | UGC capture-town objective with location-based sub-objectives |
| `obj_destroy_town.scar` | objectives | UGC destroy-buildings objective with kill counter UI |
| `ugc_map.scar` | core | UGC template map: 2-player setup, roving armies, recipe-based spawns, sequential objectives |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Rogue_Coastline_GetCustomUnitData` | coastline_data | Returns random unit squads scaled to budget |
| `Rogue_Coastline_InitUnitTables` | coastline_data | Initializes Byzantine mercenary unit type tables |
| `Rogue_Coastline_SetPOIData` | coastline_data | Defines coastal/naval/Byzantine POI data tables |
| `Pirates_SetNavalSpawnDelay` | coastline_pirates | Calculates ship spawn delay from difficulty |
| `Pirates_InitNavalRaidArmy` | coastline_pirates | Creates naval patrol army with 4-waypoint route |
| `Pirates_InitNavalTransports` | coastline_pirates | Starts transport ship spawning at 2x delay |
| `Pirates_SpawnShip` | coastline_pirates | Spawns combat ship if below max (2) |
| `Pirates_SpawnTransportShip` | coastline_pirates | Spawns transport for naval landing operations |
| `Pirates_TestNavalLanding` | coastline_pirates | Debug function to test naval landing system |
| `Rogue_Coastline_Poi_Precache` | coastline | Precaches warship/galleass blueprints for player civ |
| `Rogue_Coastline_StartNavalRaids` | coastline | OneShot callback to init naval raid army |
| `Rogue_Coastline_SpawnRelics` | coastline | Spawns 2 close + 3 far relics at markers |
| `Rogue_Coastline_SpawnFish` | coastline | Randomly spawns deep water fish (50% chance) |
| `Rogue_Coastline_SetupSideBases` | coastline | Initializes 4 side bases with keep upgrades |
| `Rogue_Coastline_SetupSideBase` | coastline | Spawns budget-scaled army for one side base |
| `Rogue_Coastline_CreateBaseArmy` | coastline | Creates patrol army at marker for side base |
| `Rogue_Coastline_TestCliff` | coastline | Debug army spawn for cliff attack testing |
| `Rogue_Forest_SetPOIData` | forest_data | Defines forest POIs (lumber camp, hunting grounds) |
| `Rogue_Forest_SpawnBanditCamps` | forest | Converts T1 POI spots into bandit camp entities |
| `Rogue_Forest_SpawnRelics` | forest | Spawns relics at close/far markers |
| `Rogue_Forest_DisableNaval` | forest | Removes all military naval units and upgrades |
| `Rogue_Forest_SetupSideBases` | forest | Initializes 4 HRE-themed side bases |
| `Rogue_Forest_SetupSideBase` | forest | Spawns budget-scaled army for one HRE base |
| `Rogue_Forest_CreateBaseArmy` | forest | Creates patrol army at marker for HRE base |
| `Daimyo_SpawnPickups` | japanese_daimyo | Spawns random resource pickups at marker list |
| `Daimyo_InitUniquePOIs` | japanese_daimyo | Defines Abandoned Village POI with trap mechanic |
| `InitAbandonedVillage` | japanese_daimyo | Sets up village trap: neutral houses, shinobi ambush |
| `TrackAbandonedVillageCompletion` | japanese_daimyo | Checks if shinobi killed and pickups collected |
| `_trackAbandonedVillageTrap` | japanese_daimyo | Interval rule: triggers shinobi ambush on proximity |
| `_UpdateShinobiTargets` | japanese_daimyo | Retargets shinobi army toward player villagers |
| `_Atmo_TransitionTo` | japanese_daimyo | Transitions atmosphere state (dawn/day/dusk/night) |
| `SpawnSites` | japanese_daimyo | Distributes relics, pickups, camps across tiers |
| `ValidateOnlyCavalry` | japanese_daimyo | Wave validator: only cavalry + siege units |
| `ValidateOnlyMeleeInfantry` | japanese_daimyo | Wave validator: only melee infantry + siege |
| `ValidateOnlyRangedInfantry` | japanese_daimyo | Wave validator: only ranged infantry + siege |
| `ShinobiShrine` | japanese_daimyo | Enables secret shrine that spawns shinobi on heal |
| `_monitorShinobiSecrets` | japanese_daimyo | Checks shrine health; spawns shinobi + monk at full |
| `_monitorSecretShinobi` | japanese_daimyo | Triggers shinobi blink when spotted by player |
| `Spawn_Shinobi` | japanese_daimyo | Spawns 3 enemy shinobi with spy ability at random |
| `Steppe_InitializeRaiders` | steppe_raiders | Sets up raider economy, defenders, target markers |
| `Steppe_UnpauseRaiders` | steppe_raiders | Starts raider timer rules and attack intervals |
| `Steppe_MonitorRaiders` | steppe_raiders | Accumulates raider income, spawns when affordable |
| `Steppe_SpawnRaider` | steppe_raiders | Spawns horse archer to defender or attacker pool |
| `Steppe_Attack` | steppe_raiders | Launches raider army at villager-targeted positions |
| `Steppe_GetRaidTargets` | steppe_raiders | Finds villagers near waypoints, builds target list |
| `Steppe_WarnAboutRaiders` | steppe_raiders | Shows UI warning and plays attack horn sound |
| `Steppe_MonitorRaidUI` | steppe_raiders | Tracks raider base destruction for completion |
| `Steppe_CheckForIdleRaiders` | steppe_raiders | Detects idle raiders every 15 seconds |
| `Steppe_RecoverIdleRaiders` | steppe_raiders | Reassigns stuck raiders to new army with targets |
| `Steppe_SpawnSites` | steppe | Distance-sorted site placement (close/far pickups) |
| `Steppe_DeleteSheep` | steppe | Culls sheep count to 6 near wonder |
| `Steppe_SpawnGuards` | steppe | Spawns 8 named guard patrols (a–h) |
| `Steppe_SpawnGuard` | steppe | Creates cavalry guard army on patrol/loop route |
| `Steppe_GetGuardUnits` | steppe | Budget-based guard composition (horseman/knight) |
| `ValidateContainsCavalry` | steppe | Wave validator: must include cavalry archetype |
| `RogueTest_InitChampionData` | system_test_data | Sets up English test army (50 mixed squads) |
| `RogueTest_InitBossData` | system_test_data | Defines 12 boss units with faction-matched bodyguards |
| `RogueTest_SpawnChampions` | system_test | Spawns two champion armies for combat testing |
| `Capture_EnemiesTownInit` | obj_capture_town | Registers capture objective with location sub-objs |
| `CaptureTown_OnComplete` | obj_capture_town | Triggers transition to destroy buildings objective |
| `DestroyTown_InitObjectives` | obj_destroy_town | Registers destroy-buildings objective with counter |
| `DestroyBuildings_UI` | obj_destroy_town | Sets building kill counter in objective UI |
| `DefeatBuildings_OnEntityKilled` | obj_destroy_town | Increments counter on building kill event |
| `MissionCompleteDelayed` | obj_destroy_town | Awards player victory after 3-second delay |

## KEY SYSTEMS

### Objectives

| Constant | Map | Purpose |
|----------|-----|---------|
| `OBJ_DESTROY_BUILDINGS` | japanese_daimyo | Registered from rogue system; destroy enemy structures |
| `OBJ_DUMMY_INFORMATION` | steppe_raiders | UI-only objective to show raider camp location |
| `OBJ_CaptureEnemiesTown` | ugc_map | Primary: capture the French city location |
| `SOBJ_DefeatTownRebels` | ugc_map | Sub-objective: defeat rebels at town |
| `SOBJ_LocationTown` | ugc_map | Sub-objective: capture the town location marker |
| `OBJ_DestroyBuildings` | ugc_map | Sequential: destroy all French city buildings |

### Difficulty Scaling

| Parameter | Map | What It Scales |
|-----------|-----|---------------|
| `Util_DifVar({0,1,1,2,2,3,3})` | coastline_data | Minor naval unit count at POIs |
| `Rogue_DifVar({0,0,10,35,50,65,80,100})` | forest, daimyo | Wolf spawn chance percentage |
| `Rogue_DifVar({2100,1500,1000,900,800,600,450,300})` | coastline | Naval raid start delay (seconds) |
| `naval_raid_spawn_delay = 300 - (difficulty * 15)` | coastline_pirates | Ship respawn interval (seconds) |
| `GetIntegerInExponentialRange(600, 200)` | steppe_raiders | Raid start time (inversely scaled) |
| `GetIntegerInExponentialRange(450, 150)` | steppe_raiders | Raid frequency interval |
| `GetFloatInExponentialRange(1.0, 4.0)` | steppe_raiders | Raider income accumulation rate |
| `GetIntegerInExponentialRange(3, 9)` | steppe_raiders | Defender count at raider base |
| `rogue_wave_strength` | all rogue maps | Global wave power multiplier (0.85–1.0) |
| `WAVE_STAGING_DURATION` | daimyo (1), steppe (5) | Seconds waves idle before attacking |
| Outpost upgrade tier | steppe_raiders | Scales with `Game_GetSPDifficulty()` (arrowslits→cannon) |

### Spawns & Waves

**Lane System**: All rogue maps use `Rogue_AddLane(name, is_side, [validator], [boss_sbp])` to define attack corridors. Waves arrive via `Rogue_UseDefaultSchedule(enabled, has_naval, strength_multiplier)`.

**Coastline**: 3 lanes (west/north/east). Byzantine side bases with springald keeps. Pirate naval raids with 2 combat ships max on 4-waypoint patrol. Transport ships for naval landings on separate timer. Pirate unit types: pirate, pirate_archer, manatarms, crossbowman, handcannon (tiered).

**Forest**: 3 lanes (west/north/east), `rogue_wave_strength = 0.85`. 5 bandit camps converted from T1 POI spots. Outlaws use bandit unit types (common, axeman, swordsman, horseman) with exponential income scaling (150–450). Naval units fully disabled.

**Daimyo**: 3 lanes each with unit-type validators and unique bosses:
- North: ranged infantry only → Oda Nobunaga boss
- East: melee infantry only → Hojo Ujinao boss
- West: cavalry only → Takeda Shingen boss
- Shinobi roamers as secondary threat. Japanese HA/SEN faction units for POI enemies.

**Steppe**: 3 lanes requiring cavalry in composition (`ValidateContainsCavalry`), `rogue_wave_strength = 0.9`. Horse archer raiders with economy-based spawning. 8 guard patrols (a–h) using cavalry/knight units on patrol/loop routes. Mongol faction units for POI enemies.

### POI System

All maps use `Rogue_POI_Init(enemy_player, unit_types, extra_pois, [count], [tier2_count])` and `Rogue_POI_Spawn(marker_prefix, types, min_tier, max_count)`.

**Coastline POIs** (3 categories):
- Coastal (9 types): wreck, ship, hoard, dock, 2× champion, merchant, ruins, random siege
- Naval (4 types): fishing boats, carrack, combat ship, shipwreck
- Byzantine (6 types): 3× mercenary tiers, elephant, elephant tower, mercenary champion

**Forest POIs** (2 types): lumber camp (villagers + lumber camp building), hunting grounds (villagers + gristmill)

**Daimyo POIs**: Standard types via Japanese unit table + Abandoned Village (unique trap: neutral houses spring shinobi ambush on player proximity; 2× speed shinobi with blink ability)

**Steppe POIs**: Generated dynamically using Mongol unit types; distance-sorted into close T1 and far T2 categories

### AI & Patrols

- **Coastline**: Naval raid army uses `TARGET_ORDER_PATROL` across 4 naval waypoints. Side base armies patrol at spawn position. Outlaws use camp-based raiding with target markers.
- **Forest**: Outlaws with camp targets split by proximity (west vs east TC). Bandit camps with `Outlaws_InitRaiding()` on unpause.
- **Daimyo**: Enemy shinobi use `shinobi_spy_jpn` ability, patrol at spawn with `leashRange = 50`. Abandoned Village trap creates `Army_Init` with victim-tracking targets and `onDeathDissolve`.
- **Steppe**: Raiders accumulate income → spawn horse archers → fill defender pool → overflow to attacker pool → attack villager positions. Idle recovery system checks every 15s, reassigns broken squads after 10s confirmation. Guard patrols use `WALK_SPEED` via `Modify_UnitSpeedWhenNotInCombat`.
- **UGC**: Two `RovingArmy` modules with `ARMY_TARGETING_REVERSE`, `combatRange = 20`, `leashRange = 40`. AI personality set to `default_campaign`.

### Timers

| Rule | Timing | Map | Purpose |
|------|--------|-----|---------|
| `Pirates_SpawnShip` | `Interval(naval_raid_spawn_delay)` | coastline | Spawn combat ships (285–300s) |
| `Pirates_SpawnTransportShip` | `Interval(delay × 2)` | coastline | Spawn transport ships |
| `Rogue_Coastline_StartNavalRaids` | `OneShot(300–2100s)` | coastline | Difficulty-scaled naval raid start |
| `Pirates_InitNavalTransports` | `OneShot(start × 0.5)` | coastline | Transport spawn start (half of raid delay) |
| `_Atmo_TransitionTo` | `OneShot(60/1440/2040/2640)` | daimyo | Day→dusk→night→dawn cycle transitions |
| `_trackAbandonedVillageTrap` | `Interval(0.5)` | daimyo | Proximity check for village ambush |
| `_monitorShinobiSecrets` | `Interval(1)` | daimyo | Shrine health check for shinobi reward |
| `_monitorSecretShinobi` | `Interval(1)` | daimyo | Visibility check for hidden shinobi |
| `Steppe_WarnAboutRaiders` | `OneShot(60)` | steppe | Early warning about raider camp |
| `Steppe_MonitorRaiders` | `IntervalWithDelay(start_gathering, 1)` | steppe | Income accumulation and unit spawning |
| `Steppe_Attack` | `IntervalWithDelay(start, interval)` | steppe | Launch raid attacks (difficulty > 0) |
| `Steppe_CheckForIdleRaiders` | `IntervalWithDelay(start, 15)` | steppe | Idle raider detection |
| `Steppe_RecoverIdleRaiders` | `OneShot(10)` | steppe | Reassign confirmed-idle raiders |
| `Steppe_RegroupRaidAttackers` | `OneShot(1)` | steppe | Regroup attackers at spawn |
| `Steppe_RegroupRaidDefenders` | `OneShot(1)` | steppe | Regroup defenders at defend marker |
| `ObjectiveCompleteNow` | `OneShot(3)` | ugc_map | Delayed objective transition |
| `MissionCompleteDelayed` | `OneShot(3)` | ugc_map | Delayed victory award |
| `KillUnitsNearWonder` | `Interval (default)` | system_test | Continuously kill enemies near wonder |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| All rogue maps | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| coastline | `rogue/rogue.scar`, `rogue_coastline_data.scar`, `rogue_coastline_pirates.scar` |
| forest | `rogue/rogue.scar`, `rogue_forest_data.scar` |
| japanese_daimyo | `rogue/rogue.scar`, `rogue/rogue_data.scar` |
| mongol_steppe | `rogue/rogue.scar`, `rogue_mongol_steppe_raiders.scar` |
| steppe_raiders | `rogue/rogue_misc.scar` |
| stamps | `rogue/rogue_objectives.scar` |
| system_test | `rogue/rogue.scar`, `rogue_system_test_data.scar` |
| ugc_map | `obj_capture_town.scar`, `obj_destroy_town.scar` |

### Shared Rogue Globals

- `ROGUE_HUMAN_PLAYERS` / `ROGUE_ENEMY_WAVE_PLAYER` / `ROGUE_ENEMY_ALLY_PLAYER` / `ROGUE_ENEMY_RAIDER_PLAYER` / `ROGUE_NEUTRAL_PLAYER` / `ROGUE_ALLY_PLAYER` — player slot constants set by `Rogue_SetupPlayers_A/B/C`
- `rogue_wave_strength` — per-map wave power scalar (0.85–1.0)
- `WAVE_STAGING_DURATION` — wave idle time override
- `content_pack = CONTENT_PACK_ROGUE` — content pack identifier
- `t_poi_types_def` — shared defensive POI types (referenced but defined in rogue system)
- `chosen_objectives` — objective tracking table (daimyo appends `OBJ_DESTROY_BUILDINGS`)
- `pickup_ebps` — shared resource pickup blueprint table
- `wonder_position` / `mkr_wonder` — wonder location marker (steppe, system_test)
- `sg_temp` / `sg_blah` — reusable scratch SGroups

### Shared Rogue API Functions (from rogue.scar / rogue system)

- `Rogue_SetupPlayers_A/B/C`, `Rogue_AddHumanPlayer`, `Rogue_AddEnemyWavePlayer`, `Rogue_AddAllyPlayer`, `Rogue_AddEnemyAllyPlayer`, `Rogue_AddEnemyRaiderPlayer`, `Rogue_AddNeutralPlayer`
- `Rogue_AddLane`, `Rogue_UseDefaultSchedule`, `Rogue_SimulateEvents`, `Rogue_DifVar`
- `Rogue_POI_Init`, `Rogue_POI_Spawn`, `Rogue_POI_SetRadii`, `Rogue_POI_GetUnitData`, `Rogue_POI_GetRandomChampion`, `Rogue_POI_GetFavoredChampion`, `Rogue_POI_GetChampionByName`, `Rogue_POI_GetFavoredNaval`, `Rogue_POI_GetRandomSiege`, `Rogue_POI_GetRandomDirection`, `Rogue_POI_GetAllyUnitsByValue`
- `Outlaws_InitData`, `Outlaws_SetUnitTypes`, `Outlaws_SetDefaultDifficultyTuning`, `Outlaws_SetIncome`, `Outlaws_FinalizeData`, `Outlaws_SetCampTargets`, `Outlaws_SetLandingRoute`, `Outlaws_InitRaiding`, `Outlaws_StartRaids`, `Outlaws_GetUnitDataSplit`, `Outlaws_LaunchNavalLanding`
- `ResourceSpots_InitData`, `ResourceSpots_Init`, `ResourceSpots_SpawnWolves`
- `Sites_Init`, `Sites_CreateRelics`, `Site_CreatePickup`, `Site_CreateRelic`, `Site_CreateCampSmall`, `Site_CreateCampLarge`, `Sites_Debug`
- `Army_Init`, `Army_AddSGroup`, `Army_SetTarget`, `Army_SetTargets`, `Army_FindArmyFromSquad`, `Army_Dissolve`
- `EventCues_CallToAction`, `Rogue_StartSideObjective`, `Rogue_IsSquadIdle`
- `GetIntegerInExponentialRange`, `GetFloatInExponentialRange`, `Cardinal_ConvertTypeToSquadBlueprint`, `Cardinal_ConvertTypeToEntityBlueprint`

### Inter-File Calls

- `rogue_coastline.scar` calls `Rogue_Coastline_SetPOIData()` (from data), `Pirates_InitNavalRaidArmy()` / `Pirates_SetNavalSpawnDelay()` / `Pirates_InitNavalTransports()` (from pirates)
- `rogue_forest.scar` calls `Rogue_Forest_SetPOIData()` (from data)
- `rogue_mongol_steppe.scar` calls `Steppe_InitializeRaiders()` / `Steppe_UnpauseRaiders()` (from raiders)
- `rogue_system_test.scar` calls `RogueTest_InitChampionData()` / `RogueTest_InitBossData()` (from data)
- `ugc_map.scar` calls `Capture_EnemiesTownInit()` (from obj_capture_town), `DestroyTown_InitObjectives()` (from obj_destroy_town)

### Boss Units (from system_test_data)

| Boss | Faction | SBP Name |
|------|---------|----------|
| Cataphract | Byzantine | `unit_cataphract_byz_boss_rogue` |
| Man-at-Arms | Byzantine | `unit_manatarms_byz_boss_rogue` |
| Fire Ram | Byzantine | `unit_ram_fire_byz_boss_rogue` |
| Dragonite Archer | HRE | `unit_dragonite_archer_hre_boss_rogue` |
| Landshark | HRE | `unit_landshark_hre_boss_rogue` |
| The Shield | HRE | `unit_the_shield_hre_boss_rogue` |
| Eagle Storm | Mongol | `unit_eagle_storm_boss_rogue` |
| Khan | Mongol | `unit_khan_boss_rogue` |
| Salgin Hunter | Mongol | `unit_salgin_hunter_boss_rogue` |
| Hojo Ujinao | Japanese | `unit_hojo_ujinao_boss_rogue` |
| Oda Nobunaga | Japanese | `unit_oda_nobunaga_boss_rogue` |
| Takeda Shingen | Japanese | `unit_takeda_shingen_boss_rogue` |
