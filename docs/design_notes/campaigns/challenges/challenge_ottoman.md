# Challenge Mission: Ottoman

## OVERVIEW

Challenge Mission: Ottoman is an "Art of War" survival-defense scenario where the player controls an Ottoman (Imperial Age) force defending a town center against escalating enemy waves approaching from three lanes (west, north, east), each with three sub-lanes (left, mid, right). Before waves begin, the player selects a Vizier Bonus to unlock specialized units; villagers then spawn to gather resources while military schools produce units automatically. Medal benchmarks are time-based survival thresholds (PC: Bronze ≥10 min, Silver ≥15 min, Gold ≥21 min; Xbox: Bronze ≥8, Silver ≥12, Gold ≥16). Enemy waves use a 30-round scripted roster with computed arrival/launch times based on lane distance and unit move speed, wrapping the final rounds to create an endless loop of increasing pressure across all three lanes simultaneously.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_ottoman.scar` | core | Main mission logic: player setup, upgrades, wave spawning, medal tracking, victory/defeat, unpause flow |
| `challenge_mission_ottoman_data.scar` | data | Lane/sub-lane definitions, 30-round wave compositions, unit costs/speeds, medal constants, arrival time math |
| `challenge_mission_ottoman_objectives.scar` | objectives | Objective registration: Vizier Bonus, Defend, Survive, Bronze/Silver/Gold medal sub-objectives |
| `challenge_mission_ottoman_automated.scar` | automated | Automated test harness: AI-driven play, checkpoint registration, RovingArmy defenders per lane |
| `training_ottoman.scar` | training | Placeholder training file with commented-out sell-resources tutorial hints |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | ottoman | Init player1/player2 as Ottoman Imperial Age |
| `Mission_SetupVariables` | ottoman | Call Ottoman_InitData1 for wave/lane data |
| `Mission_Preset` | ottoman | Grant upgrades, restrict buildings, init objectives/autotest |
| `Mission_PreStart` | ottoman | Zero resources, set Vizier level to 60 |
| `Mission_Start` | ottoman | Start objectives, intel, unpause check, FOW reveal |
| `CheckForAkinji` | ottoman | Grant horse archer upgrades after Vizier unlock |
| `CheckForUnpause` | ottoman | Detect Vizier spend; start defend/survive objectives |
| `Mission_Unpause` | ottoman | Spawn villagers, mehter, spearmen; enable production; start timer |
| `GetRecipe` | ottoman | Return MissionOMatic recipe with victory message |
| `PerTic` | ottoman | Check TC landmark death for win/loss condition |
| `PerSecond` | ottoman | Main tick: advance clock, spawn waves, award medals |
| `SpawnAttack` | ottoman | Spawn round units at sub-lane; create minimap blip |
| `LaunchAttack` | ottoman | Create RovingArmy assault module from spawned units |
| `LaunchAttackUI` | ottoman | Trigger FirstAttackers intel on first wave |
| `MonitorAttack` | ottoman | Remove attack icon when wave nears base |
| `GetPlayerReport` | ottoman | Count villagers, traders, military, military cost |
| `SpawnVillagersAndAssign` | ottoman | Spawn villagers at markers and assign gather task |
| `Ottoman_InitData1` | data | Define lanes, rounds, costs, speeds, medal thresholds |
| `Ottoman_InitData2` | data | Empty placeholder for secondary data init |
| `CreateAssaultModule` | data | Create RovingArmy with attack-move style per round |
| `GetRoundCost` | data | Sum unit costs for a round from unitTypeCosts |
| `CalculateArrivalTime` | data | Compute cumulative arrival time with decaying increment |
| `GetMetaRoundString` | data | Format meta-round info string for debug prints |
| `GetSlowestUnitSpeed` | data | Find slowest unit move speed in a unit table |
| `GetUnitTypeFromUnitRow` | data | Extract scar unit type string from unit row |
| `Ottoman_InitObjectives` | objectives | Register all OBJ/SOBJ constants and medal chain |
| `AutoTest_OnInit` | automated | Detect CampaignAutoTest flag; enable AI; register checkpoints |
| `AutomatedOttoman_RegisterCheckpoints` | automated | Register PlayStart, Bronze, Silver, Gold checkpoints |
| `AutoTest_SkipAndStart` | automated | Skip intro event and start automated mission |
| `AutoTest_PlayIntro` | automated | Play intro then start automated mission |
| `AutomatedMission_Start` | automated | Reveal FOW; create 3 RovingArmy defenders per lane |
| `AutomatedOttoman_AfterStart` | automated | Set rally point; zero food resource |
| `AutomatedOttoman_MonitorDefenders` | automated | Reinforce defenders when squads drop below 50 |
| `AutomatedOttoman_MonitorReinforcements` | automated | Transfer reinforcers into defender modules on arrival |
| `AutomatedOttoman_Phase0_CheckPlayStart` | automated | Pass PlayStart checkpoint when Bronze objective starts |
| `AutomatedOttoman_Phase1_Setup/Monitor` | automated | Track Bronze medal completion checkpoint |
| `AutomatedOttoman_Phase2_Setup/Monitor` | automated | Track Silver medal completion checkpoint |
| `AutomatedOttoman_Phase3_Setup/Monitor` | automated | Track Gold medal completion checkpoint |

## KEY SYSTEMS

### Objectives

| Constant/Key | Type | Purpose |
|--------------|------|---------|
| `OBJ_VizierBonus` | Primary | Choose a Vizier Bonus before waves begin |
| `OBJ_Defend` | Primary | Defend your town center |
| `OBJ_Survive` | Primary | Survive as long as you can (count-up timer) |
| `SOBJ_AttackNotice` | Battle (secret) | Hidden objective for attack wave UI indicators |
| `SOBJ_BronzeMedal` | Bonus | Survive 10 minutes (8 min Xbox); chains to Silver |
| `SOBJ_SilverMedal` | Bonus | Survive 15 minutes (12 min Xbox); chains to Gold |
| `SOBJ_GoldMedal` | Bonus | Survive 21 minutes (16 min Xbox); sends `CE_OTTOMANSARTGOLD` |

### Difficulty

No `Util_DifVar` scaling is used. Difficulty is effectively fixed:
- **Player**: Ottoman, Imperial Age, full tier-4 unit/econ/military upgrades granted automatically
- **Enemy**: Abbasid-blueprint units at tier 4, move speed normalized to `MOVE_SPEED_IN_METERS` (4.48 m/s)
- **Xbox adjustments**: Medal time thresholds reduced (8/12/16 min vs PC 10/15/21 min)
- **Wave timing**: First arrival at 120s; subsequent waves spaced by a decaying increment starting at 75s, decreasing by 2s per meta-round down to minimum 45s
- **Building restrictions**: Player cannot build town centers, walls, palisades, gates, towers, or docks; siege engineers upgrade removed
- **Starting upgrades**: Janissary guns, villager health, scout upgrades, university techs (biology, incendiary, architecture, silk string), siege techs (roller trigger, adjustable crossbar, weapon speed, mathematics, ram scaling)
- **Vizier system**: Imperial council level set to 60 with 1 total Vizier point; spending it triggers mission unpause
- **Enemy walls/towers**: Set invulnerable and untargetable

### Spawns

**Player starting forces** (spawned at `Mission_Unpause`):
- Villagers assigned to wood, stone, food (berries), and gold gathering (marker groups)
- 1× Mehter (at `mkr_spawn_mehter`)
- 3× Spearman (at `mkr_spawn_spearmen`)
- Military schools enabled for auto-production after unpause

**Enemy wave structure** — 30 scripted rounds across 3 lanes × 3 sub-lanes:

| Rounds | Primary Lane(s) | Key Units | Escalation |
|--------|----------------|-----------|------------|
| 1–2 | North mid | Horsemen (4), Spearmen (10) | Single sub-lane only |
| 3 | West mid + right | MAA (6), Ram (1), Horsemen (3) | First multi-group round |
| 4–6 | North multi + West | MAA (10), Archers (10), Horsemen (21), Rams, Crossbowmen | Multi-sub-lane attacks begin |
| 7 | West mid | MAA (24) + Mangonel (1) | First siege support |
| 8–10 | North + East | Rams (2), Spearmen (15–20), Archers (21), Mangonels, Trebuchet, Culverin | Artillery introduced |
| 11–14 | East + North + West | MAA (16) + Mangonels (3), Handcannoneers, Bombards (2), Knights | Heavy siege (bombards) |
| 15–18 | All three lanes | Rams (3), Knights (16), Archers (20), Trebuchets, Bombards (3) | Full 3-lane simultaneous pressure |
| 19–22 | All three lanes | Multi-sub-lane with horsemen (12), handcannoneers (14), culverins, mangonels (4) | Maximum sub-lane coverage |
| 23–25 | All three lanes | Trebuchets + Bombards on all lanes, MAA/Spearmen (14), Mangonels (3) | Peak siege density |
| 26–28 | All three lanes | Bombards + Culverins + Horsemen/MAA all 9 sub-lanes simultaneously | Overwhelming all positions |
| 29–30 | All three lanes | Horsemen (12×3), Rams (2) + MAA (8) + Mangonels, Bombards (3) + Spearmen (15) | Final rounds before wrap |

**Wave wrapping**: After round 30, time wraps back to `WRAP_TIME_START` (arrival time of round 30 − `ROUNDS_REPEATED`=3), replaying the last 3 rounds indefinitely.

**Unit move speeds** (tiles/s): Horseman 1.88, Knight 1.62, all infantry/siege normalized to 1.12, Trader 1.0.

**Unit costs** (budget): Spearman/Archer 80, MAA/Crossbow/Horseman 120, Handcannon/Knight 240, Springald 500, Ram 300, Mangonel 600, Trebuchet 750, Bombard/Culverin 1000.

### AI

- **No `AI_Enable` calls in gameplay** — all enemy behavior is scripted via `CreateAssaultModule` (RovingArmy)
- **RovingArmy assault modules**: Each round spawns units at sub-lane spawn marker, stages briefly, then launches as a RovingArmy with waypoint targets; `attackBuildings` flag determines whether units attack-move everything or ignore buildings en route
- **On-complete behavior**: When a RovingArmy reaches its final target, `onCompleteFunction` redirects it to `mkr_final_target_center` with `attackMoveStyle_attackEverything`
- **Automated test AI**: `AutoTest_OnInit` enables `AI_Enable(player1, true)` for the human player; creates 3 defender RovingArmies (50 knights each) and 3 reinforcer modules that replenish losses
- **Sub-lane targeting**: Each lane has left/mid/right sub-lanes converging on final targets (north, center, south, east, west) creating flanking pressure
- **Horn alert**: First round in each meta-round triggers `sfx_campaign_scripted_attack_horn_under_attack_high`

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `PerSecond` | 1s | Main clock: advance time, spawn waves at spawnTime, award medals |
| `PerTic` | every tick | Check TC landmark_active state for win/loss |
| `CheckForUnpause` | interval | Detect Vizier point spent (food=0) to start mission |
| `CheckForAkinji` | interval | Grant horse archer upgrades when Vizier unlocks Timariots |
| `LaunchAttack` | OneShot (per round) | Create RovingArmy assault module after `launchDelay` seconds |
| `LaunchAttackUI` | OneShot 14s | Trigger FirstAttackers intel event on first wave arrival |
| `MonitorAttack` | per-tick rule | Remove minimap blip when wave enters `mkr_remove_icon` range |
| `AutomatedOttoman_MonitorDefenders` | 1s | Check defender counts; spawn reinforcement knights |
| `AutomatedOttoman_MonitorReinforcements` | per-tick rule | Transfer reinforcer sgroup into defender module on arrival |
| `AutomatedOttoman_Phase0–3` | 1s | Monitor medal objective completion for autotest checkpoints |
| `AutoTest_SkipAndStart` / `AutoTest_PlayIntro` | 1s | Wait for intro event to complete before starting autotest |
| `AutomatedOttoman_AfterStart` | OneShot 2s | Set military school rally point and zero food |
| Challenge timer event | at 18 min | Send `CE_OTTOMANSARTTIMER` custom challenge event |

**Arrival time calculation**: `CalculateArrivalTime(isNextRound)` — starts at `FIRST_ARRIVAL_TIME`=120s. Each new meta-round adds a decrementing increment (starts 75s, −2s per round, min 45s). Sub-waves within the same meta-round share the same arrival time. `spawnTime` is computed as earliest launch time across the meta-round; `launchDelay` = 12 + individual launch offset.

## CROSS-REFERENCES

### Imports
- `cardinal.scar` — core game framework
- `MissionOMatic/MissionOMatic.scar` — modular mission system
- `MissionOMatic/MissionOMatic_utility.scar` — MissionOMatic utility functions
- `missionomatic/missionomatic_artofwar.scar` — Art of War challenge framework
- `missionomatic/modules/module_rovingarmy.scar` — RovingArmy module (automated file)
- `challenge_mission_ottoman_objectives.scar` — imported by core for objective definitions
- `challenge_mission_ottoman_data.scar` — imported by core for wave/lane data
- `challenge_mission_ottoman_automated.scar` — imported by core for autotest harness
- `challenge_mission_ottoman.events` — narration event definitions (PreStart, Start, Unpause, FirstAttackers, BronzeMedal, SilverMedal, GoldMedal)
- `training/coretraininggoals.scar` — base training system
- `training/campaigntraininggoals.scar` — campaign training (training file)
- `training/coretrainingconditions.scar` — training condition helpers (training file)
- `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar` — standard engine imports (automated file)
- `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` — test framework (conditionally imported in automated)

### Shared Globals
- `player1` / `player2` — Ottoman player and Abbasid-blueprint enemy
- `mission_seconds` — table wrapping elapsed seconds `{-1}` (starts at −1, incremented each second)
- `mission_seconds_string` — formatted time string for debug output
- `mission_seconds_wrapped` — wrapping counter for endless wave replay
- `metaRoundIndex` — current meta-round counter
- `rounds` — 30-entry wave definition table with lane, sub-lane, units, timing, sgroup, RovingArmy refs
- `metaRounds` — grouped rounds sharing same arrival time (aggregated cost, lanes, sub-lanes)
- `lanes` — west/north/east lane definitions with sub-lane spawn/staging/target markers
- `unitTypeCosts` / `unitTypeMoveSpeeds` — lookup tables for cost budgeting and move time calculation
- `OBJ_Defend` / `OBJ_Survive` / `OBJ_VizierBonus` — primary objective references
- `SOBJ_BronzeMedal` / `SOBJ_SilverMedal` / `SOBJ_GoldMedal` — medal objective chain
- `SOBJ_AttackNotice` — hidden battle objective for attack wave UI
- `OBJ_CurrentMedal` — pointer to next medal to award (chains Bronze→Silver→Gold→nil)
- `missionCompleteEvent` — event to play on TC death if medal earned
- `playerResources` — stored pre-unpause resource snapshot
- `objective_started` / `mission_unpaused` / `mission_has_started` — flow control flags
- `first_attack_has_triggered` — ensures FirstAttackers intel plays once
- `EVENTS` — narration event table (PreStart, Start, Unpause, FirstAttackers, medal events)
- `content_pack` — set to `CONTENT_PACK_ART_OF_WAR`
- `WRAP_TIME_END` / `WRAP_TIME_START` — wave-wrap boundaries for endless mode
- `INCREMENT_MAX`=75 / `INCREMENT_MIN`=45 / `INCREMENT_DELTA`=2 / `ROUNDS_REPEATED`=3 / `FIRST_ARRIVAL_TIME`=120 — timing constants
- `CHALLENGE_TIMER_MINUTES`=18 / `CHALLENGE_TIMER_SECONDS`=1080 — custom event timer
- `eg_starting_military_schools` / `eg_starting_outposts` / `eg_player_tc` — pre-placed entity groups
- `statusTable` — autotest checkpoint status enum (NotRun/InProgress/Pass/Fail)
- `AutomatedOttoman_Defenders` / `AutomatedOttoman_Reinforcers` — autotest RovingArmy arrays

### Inter-File Function Calls
- Core → data: `Ottoman_InitData1()`, `Ottoman_InitData2()`, `CreateAssaultModule()`
- Core → objectives: `Ottoman_InitObjectives()`
- Core → automated: `AutoTest_OnInit()`
- Data → data: `CalculateArrivalTime()`, `GetRoundCost()`, `GetSlowestUnitSpeed()`, `GetUnitTypeFromUnitRow()`, `GetMetaRoundString()`
- Automated → core objectives: reads `SOBJ_BronzeMedal`, `SOBJ_SilverMedal`, `SOBJ_GoldMedal` for checkpoint monitoring
- Automated → data: uses `mkr_test_defender_*`, `mkr_test_spawn_*` markers for RovingArmy setup
- Automated → RovingArmy module: `RovingArmy_Init()`, `RovingArmy_AddSGroup()`, `RovingArmy_Reset()`, `RovingArmy_GetTarget()`, `RovingArmy_SetTarget()`, `TransferModuleIntoModule()`

### Blueprint References
- **Player (Ottoman)**: `BUILDING_TOWN_CENTER_OTT`, `BUILDING_DEFENSE_PALISADE_OTT`, `BUILDING_DEFENSE_PALISADE_GATE_OTT`, `BUILDING_DEFENSE_WALL_OTT`, `BUILDING_DEFENSE_WALL_GATE_OTT`, `BUILDING_DEFENSE_TOWER_OTT`, `BUILDING_UNIT_NAVAL_OTT`
- **Enemy (Abbasid blueprints)**: `UNIT_ARCHER_4_ABB`, `UNIT_CROSSBOWMAN_4_ABB`, `UNIT_HANDCANNON_4_ABB`, `UNIT_MANATARMS_4_ABB`, `UNIT_SPEARMAN_4_ABB`, `UNIT_RAM_3_ABB`, `UNIT_MANGONEL_3_ABB`, `UNIT_TREBUCHET_4_CW_ABB`, `UNIT_BOMBARD_4_ABB`, `UNIT_CULVERIN_4_ABB`
- **Upgrades (Ottoman)**: `UPGRADE_UNIT_HORSEARCHER_3_OTT`, `UPGRADE_UNIT_HORSEARCHER_4_OTT`, `UPGRADE_RANGED_JANISSARY_GUNS_OTT`, `UPGRADE_TIMARIOTS_OTT`
- **Upgrades (Common)**: `UPGRADE_VILLAGER_HEALTH`, `UPGRADE_SCOUT_FORESTER`, `UPGRADE_SCOUT_LOS_INCREASE`, `UPGRADE_UNIT_RELIGIOUS_HERBAL_MEDICINE_4`, `UPGRADE_UNIT_RELIGIOUS_PIETY_4`, `UPGRADE_MANATARMS_ELITE_ARMY_TACTICS`, `UPGRADE_RANGED_INCENDIARY`, `UPGRADE_TECH_UNIVERSITY_BIOLOGY`, `UPGRADE_SIEGE_WORKS`, `UPGRADE_SIEGE_CHEMISTRY`, `UPGRADE_TECH_UNIVERSITY_ARCHITECTURE_4`, `UPGRADE_RANGED_ARCHER_SILKSTRING`, `UPGRADE_SIEGE_ROLLER_TRIGGER`, `UPGRADE_SIEGE_ADJUSTABLE_CROSSBAR`, `UPGRADE_SIEGE_WEAPON_SPEED`, `UPGRADE_SIEGE_MATHEMATICS`, `UPGRADE_RAM_SCALING`, `UPGRADE_OUTPOST_SPRINGALD`, `UPGRADE_OUTPOST_STONE`, `UPGRADE_SIEGE_ENGINEERS`
- **Scar unit types (waves)**: `scar_spearman`, `scar_manatarms`, `scar_archer`, `scar_crossbowman`, `scar_handcannon`, `scar_horseman`, `scar_knight`, `scar_springald`, `scar_ram`, `scar_mangonel`, `scar_trebuchet`, `scar_bombard`, `scar_culverin`, `scar_villager`, `scar_trader`, `scar_scout`, `scar_mehter`
