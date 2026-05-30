# Gameplay: Rogue System

## OVERVIEW

The Rogue system is AoE4's rogue-like survival game mode framework. Players defend a centrally-placed Wonder against escalating waves of AI-controlled enemies that travel along predefined lane pathways. The system procedurally generates wave compositions from a combinatorial template engine, scales difficulty through a polynomial resource equation (`R_0`–`R_6`), and supports medal-based progression (Bronze/Silver/Gold/Conqueror). Between waves, players interact with randomized Points of Interest (POIs), side objectives ("Nooks"), outlaw raiders, resource spots, and map-roaming enemy squads. The mode supports Conqueror difficulty with additional stressors (halved resources, roaming enemies, super rams, long-range trebuchet threats) and an Endless Mode that repeats rounds infinitely after the Gold medal threshold.

## FILE ROLES

| File | Role | Purpose |
|---|---|---|
| `rogue.scar` | core | Entry point; registers module, orchestrates init sequence, exposes public Mission API |
| `rogue_data.scar` | data | Initializes all global state: difficulty scaling, unit/archtype definitions, timing constants |
| `rogue_events.scar` | core | Event scheduler; processes time-ordered events (rounds, age-ups, lane unlocks, roamers) |
| `rogue_rounds.scar` | core | Round/Wave/Subwave lifecycle: composition calculation, spawning, Army AI launch, idle recovery |
| `rogue_wave_templates.scar` | core | Auto-generates subwave and wave templates from unit type combinatorics, assigns to lanes |
| `rogue_lanes.scar` | core | Defines lane/sublane pathways from markers, calculates travel times, handles lane selection |
| `rogue_factions.scar` | data | Player/faction setup: human, enemy wave, ally, enemy ally, raider, neutral; relationships |
| `rogue_tech_tree.scar` | core | Race-aware unit blueprint lookup, age-gated upgrades, combat upgrade grants, boss SBP resolution |
| `rogue_objectives.scar` | objectives | Primary (Defend Wonder) and 10+ side objectives with Nook-based spawning and completion logic |
| `rogue_boons.scar` | other | Post-selection boon upgrades (Golden Parachute, Cache Converters, Sticks & Stones, etc.) |
| `rogue_favors.scar` | other | Applies pre-game "Favor" upgrades (Forward Outposts, Township) with civ-specific building placement |
| `rogue_outlaws.scar` | spawns | Raider camp system: income-based unit spawning, raid timing, kidnapping, naval landings |
| `rogue_poi.scar` | spawns | Points of Interest: 30+ POI types across 2 tiers, civ-specific rewards, champion/siege units |
| `rogue_resource_spots.scar` | spawns | Weighted random resource placement (sheep, deer, boar, pickups); wolf spawning |
| `rogue_roamers.scar` | spawns | Conqueror-mode roaming enemy patrols using a node-based pathfinding network |
| `rogue_sites.scar` | spawns | Small/large enemy camp sites and relic placement along map edges |
| `rogue_misc.scar` | other | Utility functions: exponential difficulty scaling, marker helpers, debug unit counts |

## FUNCTION INDEX

| Function | File | Purpose |
|---|---|---|
| `Rogue_OnInit()` | rogue | Master init: data, factions, tech tree, lanes, boons, objectives |
| `Rogue_SimulateEvents()` | rogue | Pre-simulates all rounds/events to plan wave schedule |
| `Rogue_Start()` | rogue | Begins gameplay; applies Conqueror stressors; starts idle monitor |
| `Rogue_Unpause()` | rogue | Begins event clock and starts objectives after boon selection |
| `Rogue_UseDefaultSchedule()` | rogue | Configures standard round/lane/age-up/roamer timeline |
| `Rogue_AddLane()` | rogue | Registers a lane for enemy wave pathfinding |
| `Rogue_AddRoundAt()` | rogue | Schedules a single wave round at a given time |
| `Rogue_AddRoundsAtDecreasingIntervals()` | rogue | Schedules accelerating rounds from initial to final interval |
| `Rogue_AddRepeatingRoundAt()` | rogue | Schedules infinite repeating rounds for endless mode |
| `Rogue_AgeUpAt()` | rogue | Schedules enemy age advancement |
| `Rogue_GrantUpgrades()` | rogue | Schedules combat upgrade grants at time for age |
| `Rogue_AddBossWaveBefore()` | rogue | Marks a round before given time as boss round |
| `Rogue_SpawnRoamers()` | rogue | Schedules roamer spawn event |
| `Rogue_ApplyConquerorModeStressors()` | rogue | Halves all gaia resource deposits |
| `Rogue_CheckForIdleAttackers()` | rogue_rounds | Detects and recovers stuck wave units every 30s |
| `RogueData_Init()` | rogue_data | Sets all constants, polynomial coefficients, unit/archtype tables |
| `RogueData_GenerateScalingDifficultyScores()` | rogue_data | Generates 8-tier exponential difficulty value array |
| `Events_OnSecond()` | rogue_events | Core tick: resource accumulation, event processing, medal checks |
| `Events_ProcessEvent()` | rogue_events | Dispatches events by type to handler functions |
| `Round_Init()` | rogue_rounds | Creates round data structure with arrival time and reserve usage |
| `Round_Arrive()` | rogue_rounds | Simulates round: allocates resources, picks lanes, creates waves |
| `Round_Spawn()` | rogue_rounds | Game-time spawning: applies unit threshold ratio, super rams |
| `Wave_Init()` | rogue_rounds | Creates wave for a lane: selects template, creates subwaves |
| `Subwave_Init()` | rogue_rounds | Creates subwave: calculates unit counts, travel time, combat ranges |
| `Subwave_Launch()` | rogue_rounds | Sends staged subwave toward targets via Army system |
| `Subwave_Spawn()` | rogue_rounds | Instantiates subwave units via Army_Init |
| `SpawnManager_Update()` | rogue_rounds | Processes spawn queue one entry per frame |
| `WaveTemplates_Init()` | rogue_wave_templates | Generates all valid subwave/wave template combinations |
| `WaveTemplate_Choose()` | rogue_wave_templates | Selects weighted template matching lane, age, and value |
| `SubwaveTemplate_Init()` | rogue_wave_templates | Builds subwave template from unit name list |
| `Lane_Init()` | rogue_lanes | Creates lane with 3 sublanes from marker sequences |
| `Sublane_Init()` | rogue_lanes | Reads marker positions, calculates distance and travel time |
| `Lanes_Choose()` | rogue_lanes | Selects lanes for a round respecting locks and priorities |
| `TechTree_Init()` | rogue_tech_tree | Builds race-unit-age SBP lookup tables and boss registry |
| `TechTree_GetSBP()` | rogue_tech_tree | Returns SBP for unit name at current sim age |
| `TechTree_GrantCombatUpgrades()` | rogue_tech_tree | Grants military upgrades per age to event-driven factions |
| `TechTree_GetUpgrades()` | rogue_tech_tree | Queries upgrades by type/age/race with include/exclude filters |
| `TechTree_GetRoamerUnits()` | rogue_tech_tree | Returns unit table for roamer squads based on value budget |
| `Rogue_InitObjectives()` | rogue_objectives | Registers primary and all side objectives |
| `Rogue_ChooseObjectives()` | rogue_objectives | Randomly selects side objectives and assigns Nook markers |
| `Rogue_StartObjectives()` | rogue_objectives | Starts primary objective and queues side objective reveals |
| `Boons_OnInit()` | rogue_boons | Registers upgrade listener and starts boon selection monitor |
| `Boons_OnUpgradeComplete()` | rogue_boons | Dispatches boon effects based on completed upgrade BP |
| `Favors_ApplyFavors()` | rogue_favors | Places pre-game buildings (outposts, houses, mills) by tier |
| `Outlaws_InitData()` | rogue_outlaws | Configures raider camps, kidnapping, income parameters |
| `Outlaws_FinalizeData()` | rogue_outlaws | Creates camp data, starts income/raid monitoring rules |
| `Outlaws_CheckRaidCamps()` | rogue_outlaws | Per-second raid camp state machine (wait/raid/retreat/end) |
| `Outlaws_LaunchNavalLanding()` | rogue_outlaws | Sends raiders via transport ship to coastal landing sites |
| `Rogue_POI_Init()` | rogue_poi | Spawns randomized POIs at tier 1/2 markers |
| `Rogue_POI_Spawn()` | rogue_poi | Creates POI entities, guards, allies, and pickups |
| `ResourceSpots_Init()` | rogue_resource_spots | Places weighted random resources at marker positions |
| `ResourceSpots_SpawnWolves()` | rogue_resource_spots | Spawns wolves at markers with probability check |
| `Roamers_Init()` | rogue_roamers | Builds pathfinding network for Conqueror roamers |
| `Roamer_Spawn()` | rogue_roamers | Creates roamer squad at least-used network spawner |
| `Roamer_Monitor()` | rogue_roamers | Updates roamer navigation: node arrival, enemy detection, detours |
| `Network_Init()` | rogue_roamers | Constructs node graph with neighbor links by proximity |
| `Sites_Init()` | rogue_sites | Configures site camp unit types and pickup blueprints |
| `Nook_Init()` | rogue_objectives | Creates nook instance from marker for side objective placement |
| `Nook_SpawnArmy()` | rogue_objectives | Spawns defending army at nook with target waypoints |

## KEY SYSTEMS

### Objectives

| Constant | Purpose |
|---|---|
| `OBJ_PROTECT_WONDER` | Primary: Defend Wonder; completes at survival time, fails if wonder destroyed early |
| `SOBJ_BRONZE` | Sub-objective: survive 25 minutes |
| `SOBJ_SILVER` | Sub-objective: survive 35 minutes |
| `SOBJ_GOLD` | Sub-objective: survive 45 minutes; triggers endless mode stinger |
| `SOBJ_CONQUEROR` | Sub-objective: survive 45 minutes in Conqueror mode |
| `OBJ_DESTROY_MERCENARY` | Side: capture mercenary base by defeating guards |
| `OBJ_SAVE_ALLY` | Side: rescue allied landmark from torching enemies |
| `OBJ_HARVEST_METEORITE` | Side: mine meteorite resource deposit |
| `OBJ_BUILD_BONFIRE` | Side: repair bonfire to full health |
| `OBJ_TRAIN_UNITS` | Side: liberate military college to train elite units |
| `OBJ_CAPTURE_SIEGECAMP` | Side: capture siege workshop for trebuchet access |
| `OBJ_DEFEAT_CHAMPION` | Side: defeat hero unit, gain grenadier hero |
| `OBJ_RELIC_CART` | Side: clear enemies to claim relic cart |
| `OBJ_ENEMY_TREBUCHETS` | Conqueror threat: destroy long-range bombarding trebuchet |
| `OBJ_DESTROY_BUILDINGS` | Side: raid enemy buildings for resource rewards |
| `OBJ_RescueVillagers` | Dynamic: rescue kidnapped villagers from outlaw camps |
| `OBJ_DUMMY` / `OBJ_DUMMY_DIAMOND` / `OBJ_DUMMY_INFORMATION` | Hidden UI anchors for minimap/timer elements |

### Difficulty

Difficulty uses 8-tier exponential scaling via `Rogue_DifVar()` (indices 1–8: Easiest→Absurd).

| Parameter | What it scales |
|---|---|
| `R_0`–`R_6` polynomial coefficients | AI resource income curve (6th-degree polynomial over time) |
| `rogue_wave_strength` | Global multiplier on all wave resource budgets |
| `GetIntegerInExponentialRange(easy, hard)` | Per-difficulty exponential interpolation for any tuning value |
| `DEFENDER_DIFFICULTY_VALUE` | Defender garrison strength at POIs/sites |
| `OBJECTIVE_HOSTILES_SIZE_MODIFIER` | Side objective enemy army scaling |
| Outlaw kidnap goal | `{0,1,1,2,3,4,5,6}` — villagers captured per raid |
| Outlaw raid start time | `{-1,900,500,250,200,150,100,50}` seconds |
| Outlaw raid delay | `{900,900,750,500,400,300,250,200}` seconds between raids |
| Outlaw raid unit count min/max | Scales from `{0,2}` to `{4,14}` |
| Trebuchet shot delay | Max: `{3600→60}`, Min: `{3600→30}` — accelerates over 35min |
| `REWARD_PER_BUILDING_DESTROYED` | `{25,25,25,20,20,15,15,10}` resources per building killed |
| Conqueror resource reduction | All gaia deposits × 0.5 |
| Boss health scaling | `1.333 ^ difficulty` multiplier on boss HP |

### Spawns / Waves

- **Resource equation**: `R(t) = R_0 + R_1*t + R_2*t² + R_3*t³ + R_4*t⁴ + R_5*t⁵ + R_6*t⁶` accumulates "virtual income" each second
- **Rounds** consume a `reserve_usage` fraction (default 0.5, boss: 0.75) of accumulated resources
- **Waves** are split across 1–3 lanes, each lane gets `desired_value / lane_count`
- **Wave templates** are auto-generated combinatorially from subwave templates (unit pairs); scored/weighted by unit type proportion balancing
- **Subwaves** travel through sublane waypoints (left/center/right) using `Army_Init()` with configurable combat/leash ranges
- **Unit threshold**: spawns are ratio-scaled when active wave units exceed 800–1100 cap (`WAVE_UNIT_THRESHOLD_MIN/MAX`)
- **Boss waves**: one per boss round time, chosen from race-specific boss archtypes (infantry/cavalry/siege)
- **Super rams**: Conqueror-only, spawned every `SUPER_RAM_INTERVAL` seconds starting at 900s
- **Staging**: subwaves spawn `WAVE_STAGING_DURATION` (10s) before their launch time
- **Infinite rounds**: after `ROUNDS_REPEAT_START` (45min), rounds repeat 9 times at final interval
- **Idle recovery**: every 30s, checks for stuck wave units and re-assigns them to direct-to-Wonder army

### Unit Types & Archtypes

- **Archtypes**: infantry (35 max formation), cavalry (21), siege (4), ram (4)
- **Wave roles**: tank, dps, support, none — used for template validity checks
- **20 unit types**: militia, spearman, horseman, manatarms, landsknecht, knight, onna_bugeisha, kanabo, archer, crossbowman, horsearcher, handcannon, ozutsu, shinobi, mangonel, springald, trebuchet, bombard, ribauldequin, ram
- **`damage_to_buildings`** rating (1–3) affects template selection and building targeting behavior

### Outlaws / Raiders

- Income-based spawning: `total_income` ÷ camps, incremented every 5 minutes
- Camp state machine: `wait` → `raid` → `retreat` / `quick_retreat` → `wait` / `end`
- Kidnapping: captures villagers on kill event, transfers to neutral player, creates rescue objective
- Naval landings: garrisons raiders in transport, routes through waypoints, unloads at best landing site
- Camp destruction: killing defenders + destroying spawn building eliminates camp permanently

### Roamers (Conqueror)

- Node-based pathfinding network built from `mkr_roamer` / `mkr_roamer_spawn` markers
- Roamers travel between least-visited nodes, detour to attack nearby player units/buildings
- Aggro distance from node marker proximity radius; 5-second wait at each node
- Additional road nodes added at difficulty > 4/5/6 on "Watch Your Steppe" map
- Spawned at intervals (`roamer_interval`) with increasing value (`roamer_value_increment`)

### Points of Interest

- 30+ POI types across tier 1 and tier 2 with weighted random selection
- Civ-specific configurations for 20+ civilizations: favored unit types, champions, siege, naval units
- 12 champion types and 4 special siege types available as rewards
- POIs include: villages, mines, allied camps, monasteries, keeps, siege workshops, wolf dens, caravans, relics
- Defensive POI subtypes: outposts, barracks, stables, archery ranges, keeps

### Timers

| Rule | Interval | Purpose |
|---|---|---|
| `Events_OnSecond` | 1s | Core game clock; resource accumulation and event dispatch |
| `Boons_Monitor` | per-frame | Polls `Game_TickBoonEvent()` for boon selection completion |
| `Outlaws_CheckRaidCamps` | 1s | Raid camp state machine processing |
| `Outlaws_IncrementIncome` | 300s | Increases raider income by `income_increment` |
| `Roamers_Monitor` | 0.5s | Round-robin roamer navigation update |
| `Rogue_CheckForIdleAttackers` | 30s (delay 30s) | Detects and recovers idle wave squads |
| `SpawnManager_Update` | per-frame | Dequeues one spawn per tick to avoid frame spikes |
| `Rogue_Init_Delayed` | 0.25s one-shot | Applies favors and Ottoman vizier fix |
| `Rogue_StartObjectives` | 1.125s one-shot | Starts primary objective and timer |
| `Rogue_StartSideObjective` | 6s one-shot (chains 0.75s) | Sequentially reveals side objectives |
| `SaveAlly_Monitor` | 1s | Monitors allied army reinforcement needs |
| `College_Countdown` | per-frame | Updates military college training progress bar |

## CROSS-REFERENCES

### Imports

- `cardinal.scar` — base engine API (used by all files)
- `missionomatic/missionomatic.scar` — mission framework: `Objective_Register`, `Objective_Start`, `Objective_Complete`, `Mission_Complete`, `Mission_Fail`
- `missionomatic/missionomatic_utility.scar` — `Util_GetPosition`, `Util_GetDistance`, `AllMarkers_FromName`
- `missionomatic/missionomatic_upgrades.scar` — upgrade type matching
- `ai/army.scar` — `Army_Init`, `Army_AddTargets`, `Army_Dissolve`, `Army_AddSGroup`, `Army_FindArmyFromSquad`
- `gameplay/event_cues.scar` — `EventCues_CallToAction`, `UI_CreateEventCue`

### Shared Globals

| Global | Set in | Used by |
|---|---|---|
| `ROGUE_HUMAN_PLAYERS` | rogue_factions | All files — player reference list |
| `ROGUE_ENEMY_WAVE_PLAYER` | rogue_factions | rogue_data, rogue_rounds, rogue_tech_tree, rogue_resource_spots |
| `ROGUE_ENEMY_ALLY_PLAYER` | rogue_factions | rogue_objectives, rogue_poi, rogue_sites, rogue_outlaws |
| `ROGUE_ALLY_PLAYER` | rogue_factions | rogue_objectives (ally army), rogue_poi |
| `ROGUE_NEUTRAL_PLAYER` | rogue_factions | rogue_objectives, rogue_poi (neutral entities) |
| `states.sim` / `states.game` | rogue_data | rogue_events, rogue_rounds, rogue_tech_tree — dual-state sim/game |
| `lanes` | rogue_lanes | rogue_rounds, rogue_wave_templates |
| `rounds` | rogue_rounds | rogue_objectives (wave warning), rogue_events |
| `factions` | rogue_factions | rogue_tech_tree, rogue_misc |
| `wave_race_unit_types` | rogue_tech_tree | rogue_rounds, rogue_wave_templates, rogue_sites |
| `wave_race_boss_unit_types` | rogue_tech_tree | rogue_rounds |
| `unit_types` / `unit_names` | rogue_data → rogue_tech_tree | rogue_wave_templates, rogue_lanes |
| `archtypes` / `boss_archtypes` | rogue_data → rogue_tech_tree | rogue_wave_templates, rogue_rounds |
| `conqueror_is_enabled` | rogue_data | rogue, rogue_events, rogue_rounds, rogue_objectives |
| `mission_name` | mission script | rogue_objectives, rogue_sites, rogue_roamers |
| `mkr_wonder` / `wonder_position` | rogue_data | rogue_objectives, rogue_lanes, rogue_rounds |
| `rogue_difficulty` | rogue_data | rogue_misc (`Rogue_DifVar`) |
| `ally_lane` | rogue_lanes | rogue_objectives (ally army pathing) |
| `sg_wave_units` | rogue_data | rogue_rounds — tracks active wave squad count |
| `ROGUE_ALL_WAVE_SQUADS_SGROUP` | rogue | rogue_rounds — idle detection |

### Inter-file Call Flow

```
Mission Script → Rogue_OnInit()
  → RogueData_Init()          [rogue_data]
  → Factions_Init()            [rogue_factions]
  → TechTree_Init()            [rogue_tech_tree]
  → Lanes_Init() + Lane_Init() [rogue_lanes]
  → Boons_OnInit()             [rogue_boons]
  → Rogue_InitObjectives()     [rogue_objectives]
  → Roamers_Init()             [rogue_roamers] (Conqueror only)

Mission Script → Rogue_UseDefaultSchedule()
  → Rogue_StartGatheringAt()   → Event_InitStartGathering()  [rogue_events]
  → Rogue_AddRoundsAtDecreasingIntervals()
    → Rogue_AddRoundAt()       → Round_Init() + Event_InitRoundArrive() [rogue_rounds/events]
  → Rogue_AgeUpAt()            → Event_InitAgeUp()            [rogue_events]
  → Rogue_GrantUpgrades()      → Event_InitGrantCombatUpgrades() [rogue_events]
  → Rogue_UnlockLane()         → Event_InitUnlockLane()       [rogue_events]
  → Rogue_SpawnRoamers()       → Event_InitSpawnRoamers()     [rogue_events]

Mission Script → Rogue_SimulateEvents()
  → WaveTemplates_Init()       [rogue_wave_templates]
  → Events_OnSecond() loop     [rogue_events]
    → Round_Arrive()           [rogue_rounds]
      → Wave_Init()            → WaveTemplate_Choose() [rogue_wave_templates]
        → Subwave_Init()       → TechTree_GetSBP()    [rogue_tech_tree]

Mission Script → Rogue_Start()
  → Rogue_Unpause()            → Events_OnSecond() interval starts [rogue_events]
    → Round_Spawn()             [rogue_rounds]
      → Wave_Spawn()           → Subwave_Spawn() → Army_Init()  [ai/army]
        → Subwave_Launch()     → Army_AddTargets()
```
