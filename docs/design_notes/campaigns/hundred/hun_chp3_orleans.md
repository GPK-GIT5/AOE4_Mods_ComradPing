# Hundred Years War Chapter 3: Orleans

## OVERVIEW

The Siege of Orleans (1429) is a large-scale defensive campaign mission where the player controls France (player1) against England (player2), with Joan of Arc as a named leader hero. The player must defend the city of Orleans from escalating English assault waves launched from four northern forts (St. Laurent, London, Paris, St. Loup) while simultaneously protecting periodic trade convoys that cross the map for gold income. The mission features a sophisticated power-scaling wave composition system that dynamically selects unit types and quantities based on elapsed time, a trade/ambush cycle with cavalry raiders, and multiple fort-destruction milestones that slow enemy waves. Victory requires destroying the English keep at Les Tourelles on the south side of the river after clearing surrounding fortifications.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp3_orleans_data.scar` | data | Defines all difficulty-scaled constants, unit compositions, fort/assault target tables, wave timing, trade intervals, unit power/weight tables, MissionOMatic module lookups, and the full recipe with all spawner/RovingArmy/Defend/patrol modules. |
| `hun_chp3_orleans_objectives.scar` | objectives | Registers OBJ_Keep (defend Orleans landmark), OBJ_Les_Tourelles (destroy enemy keep), OBJ_Trade (protect supply convoy), SOBJ_NextConvoy (countdown timer), and OBJ_DebugComplete. |
| `hun_chp3_orleans_training.scar` | training | Provides tutorial goal sequences teaching the player to select Joan of Arc and discover her healing ability, with separate PC and Xbox controller flows. |
| `hun_chp3_orleans.scar` | core | Main mission script: imports sub-files, sets up players/relationships, initializes leader Joan, configures difficulty-based resources/upgrades, manages wave preparation/launch cycle, trade convoy system, fort destruction tracking, intro cinematics, and all interval rules. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Orleans_InitData1` | data | Initializes all constants, unit tables, fort data structures |
| `Orleans_InitData2` | data | Finds MissionOMatic modules for siege/staging/assault/intro |
| `GetRecipe` | data | Returns full MissionOMatic recipe with all modules |
| `Orleans_SetupWaves` | data | Creates Wave objects for 4 lanes + 2 ambush waves |
| `Orleans_InitObjectives` | objectives | Registers all objectives: Keep, Tourelles, Trade, NextConvoy |
| `Orleans_AddJoanAbilityHint` | training | PC tutorial teaching Joan selection and healing ability |
| `Orleans_AddJoanAbilityHint_Xbox` | training | Xbox tutorial with radial menu for Joan's ability |
| `UserHasSelectedJoan` | training | Predicate: checks if player has Joan selected |
| `Predicate_UserHasLookedAtJoansAbility` | training | Predicate: checks if player hovered over healing ability |
| `Predicate_JoanIsAlive` | training | Predicate: Joan alive and on screen |
| `Mission_SetupPlayers` | core | Configures 4 players, alliances, colors, AI disables |
| `Mission_SetupVariables` | core | Initializes leader Joan and calls InitData1 |
| `Mission_Preset` | core | Runs InitData2, SetupWaves, objectives, upgrades, villager tasks |
| `Mission_Start` | core | Sets resources, starts objectives, schedules waves/trades/rules |
| `Orleans_MainLoop` | core | Increments mission elapsed seconds counter every 1s |
| `Orleans_ManualWaveLaunch` | core | Launches pre-built assault wave on specified lane |
| `Orleans_StartObjectiveTourelles` | core | Starts OBJ_Les_Tourelles after 60s delay |
| `Orleans_TryWavePrepare` | core | Selects lane, generates units, prepares next wave |
| `Orleans_PrepareLane` | core | Sets units on wave and calls Wave_Prepare |
| `Orleans_ChooseLane` | core | Picks lane weighted by spawnable categories, avoids repeats |
| `Orleans_StartTradeCycle` | core | Begins repeating trade convoy cycle at intervals |
| `Orleans_PrepareRaidAndQueueTraders` | core | Prepares ambush horsemen, queues next trade objective |
| `Orleans_StartObjectiveTrade` | core | Starts or restarts OBJ_Trade objective |
| `Orleans_PrepareTradeAmbush` | core | Reinforces ambush_1 module with horsemen via wave system |
| `Orleans_SpawnTradeCart` | core | Spawns one trade cart and commands path to destination |
| `Orleans_AmbushDead` | core | Tracks ambush kills, triggers intel on first kill |
| `Orleans_CheckDespawn` | core | Checks trade cart arrival, awards gold, handles timeout |
| `Orleans_TradersGoHome` | core | Sends remaining trade carts back to spawn on timeout |
| `Orleans_CheckNorthForts` | core | Detects north fort destruction, increases wave interval |
| `Orleans_CheckSouthForts` | core | Detects south fort destruction, triggers intel events |
| `Orleans_CheckTourelles` | core | Triggers reveal intel when player approaches Tourelles |
| `Orleans_CheckBridge` | core | Triggers bridge fact intel when player reaches bridge |
| `Orleans_KeepUnderAttack` | core | Fires keep-under-attack intel on first damage event |
| `Orleans_MoveIntroUnits` | core | Orchestrates intro unit movements and crossbow positioning |
| `Orleans_GetPower` | core | Calculates wave power budget from elapsed time formula |
| `Orleans_GetWaveUnits` | core | Generates wave unit composition from power budget |
| `Orleans_PickUnitType` | core | Weighted random unit type selection within power cap |
| `Orleans_OnLaunch` | core | Callback logging wave launch count and lane |
| `Orleans_GetWaveInterval` | core | Returns next wave interval with cycling variation |
| `Orleans_Autosave` | core | Triggers autosave every 600s |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Keep` | Primary | Defend Orleans — fails mission if `eg_landmarks` count reaches 0 |
| `OBJ_Les_Tourelles` | Battle | Destroy the keep at Les Tourelles — completes mission on success |
| `OBJ_Trade` | Battle (Optional) | Protect supply convoy — repeating objective each trade cycle |
| `SOBJ_NextConvoy` | Information | Countdown timer (60s) until next trade ambush launches |
| `OBJ_DebugComplete` | Primary (hidden) | Debug cheat to force mission complete |

### Difficulty

All difficulty values use `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| `Orleans_SiegeTowerPassengerCount` | 3 | 4 | 6 | 8 | Passengers loaded into siege towers |
| `PREPARE_TIME` | 60 | 70 | 90 | 120 | Seconds for wave to build before auto-launch |
| `intro_units_1/1a/1b/2/2a` | 4 | 5 | 7 | 10 | Men-at-arms per intro assault group |
| `siege_defense_units_a–d` | 6 | 7 | 10 | 14 | Spearman/MAA/archer/crossbow per siege defend group |
| `rear_defense_units_a` | 8 | 10 | 14 | 20 | Men-at-arms per rear defend post |
| `rear_defense_units_b` | 11 | 13 | 17 | 25 | Archers per rear defend post |
| `rear_defense_units_c` | 9 | 11 | 15 | 23 | Horsemen per rear defend post |
| Fort defenders (various) | 3–10 | 4–12 | 6–16 | 9–24 | Units per fort defend module |
| Enemy longbow spawners 1–6 | 2 | 2 | 3 | 4 | Archers per longbow position |
| Enemy longbow spawners 7–8 | 6 | 7 | 10 | 15 | Archers per large longbow position |
| Patrol units (various) | 3–6 | 4–7 | 6–10 | 9–14 | Units per patrol route |
| Ambush reinforcement count | 3 | 4 | 8 | 14 | Horsemen in trade route ambush |
| Player wood/gold/stone villagers | 6/3/3 | 4/2/2 | 4/2/2 | 4/2/2 | Starting villager counts |
| Player crossbow spawners | 4 | 3 | 3 | 3 | Crossbowmen per wall group |
| Starting resources | 400 | 300 | 200 | 100 | Each resource type (food/wood/stone/gold) |
| Wave power multiplier | 0.8 | 1.0 | 1.4 | 2.0 | Scales `Orleans_GetPower()` output |
| Ram damage (Easy only) | 0.8x | — | — | — | Weapon damage modifier for rams |

### Spawns

**Wave System:**
- 4 assault lanes originating from forts: St. Laurent (lane 1), London (lane 2), Paris (lane 3), St. Loup (lane 4)
- Each lane has a staging area → waypoint → assault target → Orleans fallback targets
- Power budget formula: `1500 + 15*min(minutes,71) + (1/15000)*min(minutes,71)^4`, scaled by difficulty multiplier
- Waves split 80% regular units / 20% anti-wall siege (rams, siege towers, trebuchets)
- Regular unit types: horseman (80), knight (160), spearman (80), MAA (120), crossbow (120), archer (80), springald (400), mangonel (750) — parenthetical values are power costs
- Anti-wall types: ram (400), siege tower (350), trebuchet (900)
- Units selected via weighted random from `unit_type_weights_regular` / `unit_type_weights_anti_wall`
- Build times overridden: infantry/ranged/cavalry = 4s, siege = 8s
- Lane selection avoids last 2 prepared lanes; weighted by spawnable category count

**Wave Timing:**
- Wave 1: manual launch at 80s (lane 3)
- Wave 2: manual launch at 200s (lane 1)
- Wave 3+: automated cycle starting at `WAVE_3_LAUNCH - PREPARE_TIME` (335s minus prep time)
- Base `WAVE_INTERVAL` = 120s, increases by 20s per destroyed north fort
- Variation cycles between +0s and +30s

**Intro Assaults:** 5 RovingArmy groups (intro_assault_1/1a/1b/2/2a) attack immediately with MAA

**Static Defenses:**
- 12 siege_defend patrols (RovingArmy, TARGETING_RANDOM, aggressive) cycling between 3 markers each
- 10 rear_defend positions (Defend modules) with MAA, archers, or horsemen
- 9 fort defend modules at named fortifications with mixed compositions
- 8 enemy longbow spawner positions

**Patrols:** 8 patrol routes using TARGETING_REVERSE or TARGETING_CYCLE with MAA, knights, archers, spearmen, or horsemen

### Trade Convoy System

- First convoy at 270s (`TRADE_FIRST`), then every 270s (`TRADE_INTERVAL`)
- 60s before each convoy: ambush horsemen prepared from west or east fort spawns
- 5 trade carts spawned (player3) at 3s intervals, follow spline path through `trader_spline` markers
- Successful arrival: +100 gold per cart despawned at destination
- Timeout: 180s (`TRADE_TIMEOUT`) — remaining carts sent home
- Ambush module (`ambush_1`): leash range 200, on death triggers `Orleans_AmbushDead` intel
- `OBJ_Trade` completes on first cart arrival, fails if none arrive before timeout

### AI

- `AI_Enable(player3, false)` — trade cart player (France ally), no AI
- `AI_Enable(player4, false)` — neutral Joan holder, no AI
- Player2 (England) uses MissionOMatic modules with `attackMoveStyle_aggressive` and `attackMoveStyle_ignorePassive`
- `PlayerUpgrades_Auto(player2, false, {silkstring, incendiary})` — auto-upgrades disabled except specified
- Enemy outposts pre-upgraded with stone + arrowslits

### Timers

| Timer | Delay | Type | Purpose |
|-------|-------|------|---------|
| `Orleans_AddJoanAbilityHint` | 80s | OneShot | Show Joan healing ability tutorial |
| `Orleans_StartObjectiveTourelles` | 60s | OneShot | Start Les Tourelles destroy objective |
| `Orleans_ManualWaveLaunch` (wave 1) | 80s | OneShot | First manual assault on lane 3 |
| `Orleans_ManualWaveLaunch` (wave 2) | 200s | OneShot | Second manual assault on lane 1 |
| `Orleans_TryWavePrepare` | 335s - PREPARE_TIME | OneShot | Begin automated wave cycle |
| `Orleans_StartTradeCycle` | 210s (270-60) | OneShot | Start repeating trade convoy system |
| `Orleans_PrepareRaidAndQueueTraders` | 270s | Interval | Prepare ambush + queue next trade |
| `Orleans_MainLoop` | 1s | Interval | Increment mission clock |
| `Orleans_CheckBridge` | 1s | Interval | Detect player at bridge |
| `Orleans_CheckNorthForts` | 1s | Interval | Monitor north fort destruction |
| `Orleans_CheckSouthForts` | 1s | Interval | Monitor south fort destruction |
| `Orleans_CheckTourelles` | 1s | Interval | Detect player near Tourelles |
| `Orleans_Autosave` | 600s | Interval | Periodic autosave |
| `Orleans_SpawnTradeCart` | 1/4/7/10/13s | OneShot (x5) | Stagger trade cart spawns |
| `Orleans_CheckDespawn` | 1s | Interval | Monitor trade cart arrival/timeout |
| `Orleans_ClearMarkerPath` | 30s | OneShot | Remove trade route UI path icons |

## CROSS-REFERENCES

### Imports

| Import | Used In | Purpose |
|--------|---------|---------|
| `MissionOMatic/MissionOMatic.scar` | core | Mission framework: recipe, modules, Wave_*, RovingArmy_* |
| `hun_chp3_orleans_objectives.scar` | core | Objective definitions |
| `hun_chp3_orleans_data.scar` | core | Data constants and recipe |
| `hun_chp3_orleans_training.scar` | core | Tutorial goal sequences |
| `training.scar` | training | Base training system |
| `training/campaigntraininggoals.scar` | training | Campaign-specific training predicates and helpers |

### Shared Globals

- `leaderJoan` — initialized via `Missionomatic_InitializeLeader()`, used across core/training/objectives
- `player1`–`player4` — set in `Mission_SetupPlayers`, used everywhere
- `orleans_seconds` — mission clock table, used in core wave/trade logic
- `waves_prepared`, `waves_launched` — wave counters shared between data prep and core launch
- `trade_convoys_sent`, `trade_convoys_succeeded`, `ambushes_killed` — trade system state
- `north_forts`, `south_forts` — fort data tables defined in data, checked in core
- `wave_1` through `wave_4`, `wave_ambush_west`, `wave_ambush_east` — Wave objects
- `sg_trade_carts`, `sg_temp` — shared SGroups

### Inter-File Function Calls

- Core calls `Orleans_InitData1()`, `Orleans_InitData2()`, `Orleans_SetupWaves()` from data file
- Core calls `Orleans_InitObjectives()` from objectives file
- Core calls `Orleans_AddJoanAbilityHint()` / `Orleans_AddJoanAbilityHint_Xbox()` from training file
- Data file's `GetRecipe()` references globally-initialized variables from `Orleans_InitData1()`
- Objectives file references `eg_landmarks`, `eg_victory`, `sg_trade_carts`, `leaderJoan`, `orleans_seconds` from core/data

### MissionOMatic Module Types Used

- `UnitSpawner` — player units (Joan, knights, crossbowmen, villagers) and enemy longbow positions
- `RovingArmy` — staging areas, assault waves, intro assaults, siege defend patrols, patrols, ambush
- `Defend` — fort defenders, rear defenders, Tourelles defenders
- `Wave_New` / `Wave_Prepare` / `Wave_SetUnits` — dynamic wave composition system

### Key Events Referenced

- `EVENTS.Orleans_Intro`, `EVENTS.Victory` — intro/outro NIS
- `EVENTS.StLaurent_Destroyed`, `EVENTS.FortLondon_Destroyed`, `EVENTS.FortParis_Destroyed`, `EVENTS.StLoup_Destroyed` — north fort milestones
- `EVENTS.NorthForts_Destroyed`, `EVENTS.SouthFort_Destroyed` — aggregate fort intel
- `EVENTS.Destroy_LesTourelles`, `EVENTS.LesTourelles_Reveal` — Tourelles objective/approach
- `EVENTS.TradeCart_Appears`, `EVENTS.TradeCart_Arrives`, `EVENTS.TradeCart_Arrives_Perpetual`, `EVENTS.Second_SupplyConvoy` — trade convoy events
- `EVENTS.TradeRoad_Complete` — first ambush cleared
- `EVENTS.Bridge_Fact`, `EVENTS.Keep_UnderAttack` — proximity/damage triggers
