# Hundred Years War Chapter 2: Pontvallain

## OVERVIEW

The "Pontvallain" mission (Loire Valley, 1370) is an RTS defense scenario where the player controls Bertrand du Guesclin (French, Feudal Age) defending the allied town of Pontvallain against English forces led by Alan Buxhull. After a 30-second grace period, English raids and armies muster at a staging area; three timed raiding parties (cavalry/knights) attack along distinct paths at 3:00, 7:00, and 11:00, while three larger combined-arms armies march on the town when a 15:00 countdown expires (or earlier if raids are defeated). The player must keep Pontvallain's buildings alive while destroying all six English forces, managing an economy with traders, villagers, and ally waves that reinforce from production buildings. A bandit camp with patrolling horsemen provides an optional mid-map threat, and a secondary trade-route training hint teaches new players about trading.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp2_pontvallain.scar` | core | Main mission script: imports sub-files, player setup, restrictions, recipe/MissionOMatic modules, unit deployment, economy setup, intro/outro, and primary game-flow logic. |
| `hun_chp2_pontvallain_data.scar` | data | Initializes all global variables, SGroups, timing constants, unit compositions (with difficulty scaling), raid/army target marker lists, and MissionOMatic module references. |
| `hun_chp2_pontvallain_objectives.scar` | objectives | Defines and registers all objectives: protect Pontvallain, defeat English (parent), defeat raiding parties (sub), defeat armies (sub), countdown timer, optional build objective. |
| `hun_chp2_pontvallain_training.scar` | training | Adds a trade-cart tutorial goal sequence that guides the player to select a trader and establish a trade route with the allied market. |
| `obj_destroy.scar` | objectives | Standalone destroy objective template registering `OBJ_Destroy` ("Defeat the English army") — appears to be a supplementary/template file. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Pontvallain_InitData1` | data | Initializes globals, SGroups, timing constants, unit compositions |
| `Pontvallain_InitData2` | data | Binds MissionOMatic modules, links raid/army SGroups |
| `GetRecipe` | data | Returns MissionOMatic recipe with modules and playbill |
| `Pontvallain_SetupWaves` | data | Creates 3 ally reinforcement waves with 20s build times |
| `Mission_SetupPlayers` | core | Configures 4 players: French, English, Pontvallain ally, Bandits |
| `Mission_SetupVariables` | core | Calls `Pontvallain_InitData1` to create mission globals |
| `Mission_SetRestrictions` | core | Removes walls, towers, outposts, palisades from player build menu |
| `Mission_Preset` | core | Deploys starting units, villagers, traders, scout; assigns economy tasks |
| `Mission_Start` | core | Starts protect objective, economy, bandit detection, enemy arrival timer |
| `Pontvallain_EnemyArrives` | core | Moves all 6 English groups to muster point after grace period |
| `Pontvallain_MoveEnglish` | core | Sets initial muster target for a raid/army module |
| `Pontvallain_StartObjective` | core | Starts `OBJ_DefeatEnglish` 5s after enemy arrives |
| `Pontvallain_StartRaid` | core | Activates a raid group: sets targets, UI icons, path markers |
| `Pontvallain_MonitorRaid` | core | Tracks raid position for UI/celebration on death |
| `Pontvallain_RaidDead` | core | Handles raid death: increments counter, checks completion |
| `Pontvallain_StartArmies` | core | Activates all 3 army groups simultaneously |
| `Pontvallain_StartArmy` | core | Activates one army: sets targets, UI icons, threat arrows |
| `Pontvallain_MonitorArmy` | core | Tracks army position for UI/celebration on death |
| `Pontvallain_ArmyDead` | core | Handles army death: increments counter, checks victory |
| `FindBandits` | core | Polls every 2s if player can see bandits, triggers intel |
| `Pontvallain_OnConstructionComplete` | core | Tracks military building construction for optional objective |
| `Pontvallain_ShowBuildObjective` | core | Shows optional build objective after 60s if incomplete |
| `Pontvallain_IntroMoveScout` | core | Queues scout along 11 waypoints toward player base |
| `Pontvallain_IntroMoveScout_2` | core | Applies 3x speed modifier to scout mid-path |
| `SpawnOutroUnits` | core | Destroys all units, spawns villager crowds for outro NIS |
| `SpawnOutroRiders` | core | Spawns knight parade rows for victory outro |
| `Pontvallain_SetMusicTense` | core | Resets music to tense intensity mapping |
| `Pontvallain_RemovePath` | core | Clears path icons 30s after route display |
| `Pontvallain_InitObjectives` | objectives | Registers all 7 objectives (including debug) |
| `Destroy_InitObjectives` | obj_destroy | Registers standalone `OBJ_Destroy` defeat objective |
| `Pontvallain_AddHintTrade` | training | Adds trade tutorial goal sequence (non-Xbox only) |
| `TradeTrigger` | training | Checks if trader and allied market are visible on screen |
| `TradeIgnore` | training | Bypasses trade hint if player already trading |
| `UserIsSelectingTrader` | training | Returns true if player has trade cart selected |
| `UserIsTrading` | training | Returns true if player has active trader count > 0 |
| `FindSquadOnScreen` | training | Finds closest squad of type visible on camera |
| `UserIsSelectingSquadType` | training | Checks if selected squads match a given type |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Protect` | Primary | Town of Pontvallain must survive (fails mission if all buildings in `eg_pontvallain` destroyed) |
| `OBJ_Build` | Optional | Construct 3 military production buildings (Easy/Normal only, shown after 60s) |
| `OBJ_DefeatEnglish` | Battle (Parent) | Top-level objective: defeat all English forces |
| `SOBJ_DefeatRaids` | Battle (Sub) | Defeat all 3 raiding parties (counter: 0/3) |
| `SOBJ_DefeatArmies` | Battle (Sub) | Defeat all 3 English armies (counter: 0/3) |
| `OBJ_Wait` | Information | 15:00 countdown timer until English armies march |
| `OBJ_Destroy` | Primary | Template-based "Defeat the English army" (from `obj_destroy.scar`) |
| `OBJ_DebugComplete` | Primary (hidden) | Debug cheat: removes all rules and completes mission |

### Difficulty

All scaling uses `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| Starting resources (Food/Wood/Stone/Gold) | 400 | 300 | 200 | 100 | Player starting economy |
| Player woodcutters | 8 | 4 | 4 | 4 | Starting villager count at wood |
| Raid 1 horsemen | 6 | 8 | 11 | 15 | First raiding party size |
| Raid 2 horsemen | 8 | 10 | 14 | 20 | Second raid cavalry |
| Raid 2 knights | 3 | 4 | 6 | 9 | Second raid heavy cavalry |
| Raid 3 knights | 12 | 15 | 21 | 30 | Third raid heavy cavalry |
| Army 1 archers | 14 | 18 | 25 | 35 | First army ranged |
| Army 1 MAA | 14 | 18 | 25 | 35 | First army melee infantry |
| Army 2 archers | 14 | 18 | 25 | 35 | Second army ranged |
| Army 2 MAA | 14 | 18 | 25 | 35 | Second army melee infantry |
| Army 3 archers | 14 | 18 | 25 | 35 | Third army ranged |
| Army 3 MAA | 10 | 13 | 17 | 25 | Third army melee infantry |
| Army 3 knights | 7 | 10 | 14 | 20 | Third army heavy cavalry |
| Bandit defenders (spearmen) | 4 | 5 | 7 | 10 | Static bandit camp defense |
| Bandit defenders (archers) | 4 | 5 | 7 | 10 | Static bandit camp defense |
| Bandit patrol (horsemen) | 6 | 7 | 10 | 14 | Roving bandit patrol |
| Optional build objective | shown | shown | hidden | hidden | Only Easy/Normal get build hint |

### Spawns

- **Player starting forces**: 10 archers, 10 spearmen, 8 farmers, 4-8 woodcutters (by difficulty), 2 idle villagers, 1 scout, 2 trade carts.
- **English raids** (3 groups, `RovingArmy` modules): Spawned at `mkr_raid_spawn_1/2/3`, initially move to muster point `mkr_english_muster_defend`, then dispatched along target marker chains (`raid_targets1/2/3` with 8-11 waypoints each) at timed intervals.
  - Raid 1: Horsemen only (6-15 by difficulty)
  - Raid 2: Horsemen (8-20) + Knights (3-9)
  - Raid 3: Knights only (12-30)
- **English armies** (3 groups, `RovingArmy` modules): Spawned at `mkr_army_spawn_1/2/3`, muster then march when timer expires.
  - Army 1: Archers (14-35) + MAA (14-35)
  - Army 2: Archers (14-35) + MAA (14-35)
  - Army 3: Archers (14-35) + MAA (10-25) + Knights (7-20)
- **Allied waves** (3 waves from `Wave_New`): Each produces 5 archers + 5 spearmen from `mkr_pontvallain_buildings` with 20s build time per unit, assigned to `PontvallainDefend1/2/3` modules that hold defensive positions.
- **Ally villagers**: 20 farmers (7 groups) + 18 woodcutters (4 groups) pre-deployed for player3.
- **Bandits**: Static defenders at `mkr_bandit_defense` + roving patrol cycling 4 waypoints.

### AI

- **No AI_Enable calls** — all enemy behavior is module-driven via `RovingArmy` (with `onDeathFunction` callbacks) and `Defend` modules from MissionOMatic.
- **Player upgrades disabled**: `PlayerUpgrades_Auto(player1/2, false)` — no automatic tech research.
- **Ally outposts**: Auto-upgraded with `UPGRADE_OUTPOST_ARROWSLITS` at preset.
- **Bandit patrol**: Uses `ARMY_TARGETING_REVERSE` targeting type, cycling through 4 patrol markers.
- **English movement**: Raids and armies first muster at `mkr_english_muster_defend`, then are redirected to attack targets via `RovingArmy_SetTargets` with `useCustomDirection = false`.

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `GRACE_PERIOD` | 30s OneShot | Delay before `Pontvallain_EnemyArrives` moves English to muster |
| `Pontvallain_StartObjective` | 5s OneShot | Starts `OBJ_DefeatEnglish` after enemy muster |
| `RAID_1_TIME` | 180s (3:00) OneShot | Activates first raiding party |
| `RAID_2_TIME` | 420s (7:00) OneShot | Activates second raiding party |
| `RAID_3_TIME` | 660s (11:00) OneShot | Activates third raiding party |
| `TIMER_DURATION` | 960s (15:00) Countdown | `OBJ_Wait` countdown; armies march when it expires |
| `SHOW_BUILD_OBJECTIVE_TIME` | 60s OneShot | Shows optional build objective (Easy/Normal) |
| `FindBandits` | 2s Interval | Polls if player can see bandit SGroup, triggers intel event |
| `Pontvallain_RemovePath` | 30s OneShot | Removes path marker icons after raid/army activation |
| `Pontvallain_IntroMoveScout_2` | 4s OneShot | Applies 3x speed modifier to intro scout |
| `SpawnOutroRiders` | 0/5.5s/11s OneShot | Stages 3 waves of knight parade riders in outro |
| `Wave_OverrideUnitBuildTime` | 20s each | Ally wave spearmen/archers take 20s per unit to train |
| `Music_LockIntensity` | 10s/180s | Locks music to tense (raid start) or combat (army start) |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core mission framework (RovingArmy, Defend modules, Wave system, Objective system)
- `training.scar` — Base training/tutorial goal system
- `training/campaigntraininggoals.scar` — Shared campaign training utilities (`CampaignTraining_TimeoutIgnorePredicate`, `AShortPeriodOfTimeHasPassed`)
- `hun_chp2_pontvallain_objectives.scar` — Objective definitions (imported by core)
- `hun_chp2_pontvallain_data.scar` — Data/variable initialization (imported by core)
- `hun_chp2_pontvallain_training.scar` — Training hints (imported by core)

### Shared Globals
- `player1`–`player4` — Standard player slots (French, English, Pontvallain, Bandits)
- `PLAYERS` — Global player table used in outro cleanup
- `sg_allsquads`, `eg_allentities` — Engine-provided global groups
- `sg_temp` — Shared temporary SGroup for filtering/proximity checks
- `eg_pontvallain` — EGroup of Pontvallain buildings (defined on map, checked by `OBJ_Protect`)
- `eg_ally_market` — Allied market EGroup for trade route target

### Inter-file Function Calls
- `core` → `data`: `Pontvallain_InitData1()`, `Pontvallain_InitData2()`, `GetRecipe()`, `Pontvallain_SetupWaves()`
- `core` → `objectives`: `Pontvallain_InitObjectives()`
- `core` → `training`: `Pontvallain_AddHintTrade()`
- `objectives` → `core`: `Pontvallain_StartRaid()`, `Pontvallain_StartArmies()` (via timer/objective callbacks)
- `data`/`objectives` → `core`: `Pontvallain_RaidDead()`, `Pontvallain_ArmyDead()` (via `onDeathFunction` module callbacks)

### MissionOMatic Modules
- `PontvallainDefend1/2/3` — `RovingArmy` (player3 ally defenders, wave targets)
- `EnglishRaid1/2/3` — `RovingArmy` (player2 raiders, `onDeathFunction = Pontvallain_RaidDead`)
- `EnglishArmy1/2/3` — `RovingArmy` (player2 armies, `onDeathFunction = Pontvallain_ArmyDead`)
- `BanditDefenders` — `Defend` (player4 static camp defense)
- `BanditPatrol` — `RovingArmy` (player4 roving patrol, `ARMY_TARGETING_REVERSE`)

### Blueprint References
- `EBP.FRENCH.BUILDING_DEFENSE_WALL_FRE`, `BUILDING_DEFENSE_WALL_GATE_FRE`, `BUILDING_DEFENSE_TOWER_FRE`, `BUILDING_DEFENSE_OUTPOST_FRE`, `BUILDING_DEFENSE_PALISADE_FRE`, `BUILDING_DEFENSE_PALISADE_GATE_FRE` — Removed from player build menu
- `UPG.COMMON.UPGRADE_OUTPOST_ARROWSLITS` — Applied to ally outposts at preset

### Event/NIS References
- `EVENTS.Pontvallain_Intro` — Intro NIS
- `EVENTS.Victory` — Outro NIS
- `EVENTS.English_Spawn` — Intel for `OBJ_DefeatEnglish` start
- `EVENTS.First_English` — Intel for first raid start
- `EVENTS.English_March` — Intel for armies marching
- `EVENTS.More_English` — Intel for subsequent raids (raids 2/3)
- `EVENTS.Discover_Bandits` — Intel triggered when player spots bandits
