# Abbasid Mission 3: Red Sea

## OVERVIEW

This mission is a naval-focused campaign scenario set on the Red Sea in 1183 where the player (Ayyubid/Saladin) must protect allied trade routes from Crusader raids and pirates while accumulating gold. The mission flows through three phases: a **naval tutorial** (build fishing boats, trade ships, warships; defeat intro Crusaders), a **main trade phase** (gather a gold threshold via allied trade while managing Civil Unrest and fending off escalating Crusader raid waves), and a **finale** (defend allied docks from Reynald's final assault). Raids escalate through progressively harder wave templates featuring fleets, net formations, marine landings, and demolition ships, culminating in a finale wave led by Reynald's flagship. Allied trade convoys (players 4/5/6) circulate between ports generating gold, while a civil unrest meter tracks trade ship losses versus enemy kills. A secondary pirate system on a nearby island provides an optional objective that resets Civil Unrest when completed. Difficulty scaling is extensive, affecting fleet sizes, wave intervals, unrest accumulation, and unit compositions across four tiers.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m3_redsea.scar` | core | Mission entry point: player setup, imports, lifecycle hooks, squad death handling, achievement tracking |
| `abb_m3_redsea_data.scar` | data | Central data definitions: difficulty tables, unit compositions, wave patterns, raider routes, pirate armies, recipe/MissionOMatic config |
| `abb_m3_redsea_objectives.scar` | objectives | Registers all objectives (tutorial, main gold-gathering, unrest meter, pirate hunt, finale), defines completion/failure logic and Civil Unrest system |
| `abb_m3_redsea_raid.scar` | spawns | Manages all Crusader raid waves: fleets, net formations, marines, demolishers, and the finale wave |
| `abb_m3_redsea_pirates.scar` | spawns | Pirate fleet spawning, patrol AI, dock rebuilding, hunter/patrol lifecycle, camp defense triggers |
| `abb_m3_redsea_trade_convoys.scar` | trade | Spawns and routes allied trade convoys between ports, awards gold on arrival, handles evacuation |
| `abb_m3_redsea_training.scar` | training | Tutorial goal sequences for allied banner, patrol command, and sea outpost hints |
| `abb_m3_redsea_automated.scar` | automated | Automated testing harness: skips/plays intro, queues starting ships, drives bots through all objectives to victory |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Configures 6 players, alliances, colors, House of Wisdom |
| `Mission_Preset` | core | Sets resources, removes land units/upgrades, configures allies |
| `Mission_PreStart` | core | Registers objectives, boosts ship sight/speed, sets audio |
| `Mission_Start` | core | Starts convoys, pirates, first objective, VO, monitors |
| `CheckSquadDeath` | core | Handles unrest on trade deaths, loot drops from enemies |
| `ActivateDockMegavision` | core | Gives all docks 20x sight radius for map reveal |
| `RedSea_CheckForAchievement` | core | Awards achievement if 20+ trade ships actively trading |
| `RedSea_InitData` | data | Initializes all difficulty, unit, wave, and route tables |
| `GetBundle` | data | Retrieves a raider target bundle by ID |
| `GetLandingPartyIndex` | data | Returns incrementing index for landing parties |
| `GetRaiderIndex` | data | Returns incrementing index for raider armies |
| `GetRaiderUnits` | data | Cycles through raider unit group compositions |
| `GetRaiderTargets` | data | Cycles through raider target route sets |
| `GetRecipe` | data | Returns MissionOMatic recipe with NIS, title card, pirate armies |
| `RedSea_RegisterObjectives` | objectives | Defines and registers all mission objectives |
| `TallyTeamGoldDuringObjective` | objectives | Sums player + allied gold earned since objective start |
| `RedSea_TrackPlayerEarnedGold` | objectives | GE_PlayerAddResource handler tracking player gold income |
| `ModifyCivilUnrest` | objectives | Adjusts unrest value, triggers thresholds/warnings/failure |
| `_RedSea_LogBatchedUnrest` | objectives | Sends aggregated unrest delta to UI each frame |
| `MonitorTeamGold` | objectives | Updates gold counter display for SOBJ_GoldCounter |
| `Debug_ForceWave` | objectives | Debug: forces next raid wave timer to 1s |
| `Debug_BumpUnrest` | objectives | Debug: sets unrest to 80% |
| `Raids_Init` | raid | Initializes wave state, net fleet data, starts raid objective |
| `Raids_HandleIntroShips` | raid | Replaces Reynald with hulk, routes intro crusaders |
| `Raids_LaunchRaiderWave` | raid | Spawns next raid wave from template with all unit types |
| `Raiders_TriggerPreFinaleRetreat` | raid | Retreats active raiders to allied ports before finale |
| `Raids_LaunchFinalRaiderWave` | raid | Spawns finale wave with net fleets, demos, blockaders |
| `Raids_ValidateFinalWave` | raid | Confirms finale units spawned, sets up Reynald UI crown |
| `Raids_Monitor` | raid | Detects wave end, starts countdown timer for next wave |
| `Raid_SpawnFleet` | raid | Creates patrolling NavalArmy hunting trade convoys |
| `Raids_GetTargetConvoyRoute` | raid | Picks random route, orients closest waypoint first |
| `Raid_SpawnBlockaders` | raid | Spawns bombardment fleet targeting allied ports |
| `Raid_SpawnNetFleets` | raid | Creates 3-fleet closing net formation around player base |
| `Raid_NetManager` | raid | Advances net stages; withdraws if player has no docks |
| `Raid_SpawnMarines` | raid | Spawns transport ships with embarked land units |
| `_Raids_TransitionToLand` | raid | Converts marine army to land targets after disembark |
| `Raids_SpawnMarinesEscort` | raid | Spawns escort fleet accompanying marine transports |
| `Raid_SpawnDemolishers` | raid | Spawns explosive ship army targeting player waters |
| `Raids_DemolishersConfigureUI` | raid | Shows OBJ_DemoRaiders objective with UI tracking |
| `Pirates_Init` | pirates | Creates pirate groups, targets, patrol routes, starts camp check |
| `Pirates_Start` | pirates | Starts pirate sighting check and delayed monitoring |
| `Pirates_CheckForCampAttack` | pirates | Activates Crusader camp army if player approaches |
| `Pirates_EnablePlayerBaseDriveby` | pirates | Adds near-player route to pirate targets (Hard+) |
| `Pirates_CheckForPlayerSighting` | pirates | Starts SOBJ_PirateHunt when player spots pirate units |
| `Pirates_Monitor` | pirates | Main pirate lifecycle: respawn, patrol, engage raiders |
| `Pirates_RebuildDock` | pirates | Rebuilds pirate dock if destroyed and player not nearby |
| `Pirates_CommenceConstruction` | pirates | Finds placed dock blueprint, starts villager construction |
| `Pirates_MaintainReconstruction` | pirates | Keeps villagers repairing dock until complete |
| `Pirates_Spawn` | pirates | Spawns hunter or patrol pirate fleet via NavalArmy_Init |
| `Pirates_OnComplete` | pirates | Reassigns pirate fleet targets after route completion |
| `Pirates_OnDeath` | pirates | Clears active pirate fleet reference on death |
| `TradeConvoys_Init` | trade_convoys | Sets destinations, starts 3 staggered convoy launches |
| `TradeConvoys_SendHome` | trade_convoys | Evacuates all convoys to nearest exit points |
| `_TradeConvoys_Launch` | trade_convoys | Spawns 8 trade ships at next port in rotation |
| `_TradeConvoys_PlanRoute` | trade_convoys | Builds shuffled multi-stop circuit from home port |
| `_TradeConvoys_Manager` | trade_convoys | Monitors convoys, awards gold at stops, respawns dead ones |
| `MissionTutorial_AddHintToAlliedBanners` | training | Goal sequence for selecting allied banner |
| `MissionTutorial_Patrol` | training | Two-step goal: select dhows then issue patrol command |
| `MissionTutorial_AddHintToSeaOutpost` | training | Hint about defensive structures vs naval units |
| `MissionTutorial_TagDock` | training | Creates UI tag on dock for trade setup hint |
| `AutoTest_OnInit` | automated | Entry point; checks CampaignAutoTest arg, registers checkpoints |
| `AutomatedMission_Start` | automated | Reveals FOW, registers checkpoints, starts tutorial check |
| `Automated_RegisterCheckpoints` | automated | Registers 4 test checkpoints with timeout durations |
| `AutomatedRedSea_CheckTutorialStart` | automated | Waits for OBJ_TutNaval, queues ships and villager gather |
| `AutomatedRedSea_QueueStartingShips` | automated | Queues fishing boats, baghlahs, trade ships at docks |
| `AutomatedRedSea_ManageTutorialShips` | automated | Auto-commands fishers, warships, traders during tutorial |
| `AutomatedRedSea_CheckPlayStart` | automated | Waits for OBJ_AllyGold, starts hunt/defense rules |
| `AutomatedRedSea_StartPirateHunt` | automated | Deploys fleet toward pirate island, transitions to land |
| `AutomatedRedSea_PlayerHuntFranks` | automated | Spawns hunter groups to chase Crusader naval units |
| `AutomatedRedSea_PlayerDefendBase` | automated | Deploys harbor patrol fleet along defensive waypoints |
| `AutomatedRedSea_PlayerDefendAlly` | automated | Redirects defense fleet to allied base after gold phase |
| `AutomatedRedSea_PlayerHuntPirates` | automated | Manages fleet + land army assault on pirate island |
| `AutomatedRedSea_CheckMissionComplete` | automated | Checks OBJ_FinalWave completion, marks victory checkpoint |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_TutNaval` | Primary | Tutorial wrapper: build ships, fish, trade, fight — timed on Hard+ (300s) |
| `SOBJ_TutFishingBoats` | Sub | Build 3 fishing boats |
| `SOBJ_TutFishing` | Sub | Assign 3 fishing boats to gather food |
| `SOBJ_TutTradeShips` | Sub | Build 5 trade ships |
| `SOBJ_TutTrading` | Sub | Assign 5 trade ships to trade with allied dock |
| `SOBJ_TutWarships` | Sub | Build 3 Baghlahs (warships) |
| `SOBJ_TutNavalCombat` | Battle (sub) | Destroy intro Crusader ships |
| `OBJ_AllyGold` | Primary | Accumulate gold threshold (30k–35k) with allies |
| `SOBJ_GoldCounter` | Sub | Tracks/displays team gold progress toward threshold |
| `SOBJ_ClearRaiders` | Sub | Clear remaining raiders after gold threshold reached |
| `TOBJ_TradeTip` | Tip | Trade guidance (Easy/Story only) |
| `OBJ_UnrestMeter` | Unrest | Civil Unrest progress bar — reaches 1.0 = mission fail |
| `TOBJ_UnrestTip` | Tip | Unrest explanation tooltip |
| `OBJ_RaidWaveIncoming` | Battle | Countdown timer to next Crusader raid wave |
| `OBJ_DemoRaiders` | Information | Tracks approaching demolition ships with UI indicator |
| `SOBJ_PirateHunt` | Optional | Destroy pirate camp on island — resets unrest to 0 |
| `TOBJ_PirateTip` | Tip | Pirate hunt guidance |
| `OBJ_BufferFinalWave` | Information | Prep timer before Reynald's final assault (60–300s by difficulty) |
| `SOBJ_NavyConstruction` | Sub | Guidance: build 40 warships before finale (Easy/Story) |
| `OBJ_FinalWave` | Information | Defend 3 allied docks from Reynald — victory/failure condition |
| `SOBJ_DockCounter` | Sub | Tracks remaining allied docks (all destroyed = fail) |

### Difficulty

All via `Util_DifVar({Story, Easy, Intermediate, Hard})`:

| Parameter | Scaling |
|-----------|---------|
| `victoryGoldThreshold` | 30k/30k/35k/35k gold to win |
| `productionSpeedBonus` | Player production speed: 2.0x → 1.0x |
| `unrestStartValue` | Starting unrest: 0.05 → 0.15 |
| `extraGuidance` | Tip objectives shown on Story/Easy only |
| `raiderWaveInterval` | Wave spacing: 6min → 3min (decays by 0.2/wave, min 0.4x) |
| `raiderWaveCleanupTime` | Wave cleanup timeout: 8min → 5min |
| `raiderCampSpearmen/Archers` | Coastal camp garrison: 6–10 spear / 4–8 archer |
| `raiderFleetGalleys/Hulks/SiegeGalleys` | Fleet sizes: ~2–8 per type |
| `raiderDemolishers` | Demo ships: 2 → 12 |
| `raiderMarinesCount` | Marine landing party: 8 → 48 units |
| `raiderMarinesSiege` | Siege type: Springald → Mangonel |
| `raiderReynaldHulks/Galleys` | Reynald escort fleet sizes |
| `raiderFinale*` | Finale bombardment fleet sizes, prep time (300s→60s), net multiplier (1.0→2.0) |
| `pirateRespawnDelay` | Pirate respawn: 90s → 15s |
| `pirateHunter*` | Pirate hunter/patrol fleet composition |
| `pirateLandUnits1-3/Siege` | Pirate island garrison sizes |
| `pirateOutpostWeapons` | Outpost upgrade: Arrowslits or Springald (stone upgrade on Hard+) |
| Military build time multiplier | `Util_DifVar({0.5, 0.75, 1, 1})` — faster on Easy/Story |
| `PlayerUpgrades_ApplyHealthBonuses` | Health bonuses based on difficulty/console |

Easy/Story also restricts raider routes to 4 (vs 6 on higher).

### Spawns

- **Crusader Raid Waves**: Defined in `RAIDER_WAVES` (6 wave templates), each composed of `fleets` (galleys/hulks/mixed), `net` (net-closing fleets), `marines` (transport landing parties with 60% spear/30% archer/10% siege), and `demoShips` (demolition ships). Unit groups cycle via `GetRaiderUnits()` and progressively add hulk, raid galley, and mixed compositions. Spawns at 5 `RAIDER_SPAWN_POINTS`, route through paired waypoints.
- **Net Formation**: 3 fleets (`fleet1/2/3`) spawn from different points, advance through `RAIDER_NET_STAGES` (outer → inner markers) to close a net on the player base. Withdraws if player has no docks.
- **Marines**: Transport ships (`RAIDER_MARINES_TRANSPORT_COUNT`) with embarked land units (`RAIDER_MARINES_UNITS`); siege added after first marine wave. Escort fleet accompanies first marine group. After landing, transitions to land army targeting inland markers.
- **Demolishers**: `RAIDER_UNITS_DEMOLITION` — explosive ships aimed at `mkr_demolition_target`. Frequency: 300s interval.
- **Finale Wave**: Three net fleets (west/mid with Reynald leader/east) plus bombardment fleets targeting 9 finale markers and 3 blockader fleets at allied ports. Scaled by `raiderFinaleNetMultiplier`. Reynald's flagship gets leader crown UI.
- **Trade Convoys**: 8 Ayyubid trade ships per convoy, 3 convoys launched 2s apart, cycling through all ports. Destroyed convoys respawn after 15s. Gold awarded at each stop.
- **Pirates**: Hunter fleet (Baghlahs + Xebecs/Battleships) and patrol fleet (Dhows + Baghlahs) spawned via `NavalArmy_Init` at `mkr_pirate_spawn`. Respawn after `pirateRespawnDelay`. Dock auto-rebuilds if destroyed.
- **Pirate Island Garrison**: 4 MissionOMatic Army modules — Pirate melee (8–16), Pirate archers patrol (2–5), Archer patrol (2–4), Springald siege (0–3).
- **Crusader Camp**: Spearman + archer garrison on coast between player and ally, activated on player proximity.
- **Wave Interval Decay**: `g_raidWaveIntervalMultiplier` starts at 1.0, decreases by 0.2 per wave (min 0.4), accelerating raids.

### AI

- **NavalArmy Pattern**: Fleets patrol routes via `TARGET_ORDER_LOOP` or waypoint sequences with `onCompleteFunction` callbacks for retargeting. No explicit `AI_Enable` calls — behavior driven entirely through `NavalArmy_Init` and `Army_Init` systems.
- **Pirate AI**: `Pirates_Monitor` drives hunter fleet to random attack routes, detects/pursues Crusader raiders via `SGroup_CanSeeSGroup`. Patrol fleet follows fixed patrol route around island. On Hard+, pirate targets extended near player base after 300s delay.
- **Pirate Dock Rebuild**: `Pirates_RebuildDock` checks every 5s, places new dock via `LocalCommand_PlayerPlaceAndConstructEntitiesPlanned`, spawns villagers to construct.
- **Crusader Camp**: `Pirates_CheckForCampAttack` uses `Army_Init` to activate camp garrison when player enters proximity.
- **Blockaders**: `attackBuildings = BUILDINGS_ALL`, `attackMove = false` — direct building assault at allied ports.
- **Pre-Finale Retreat**: `Raiders_TriggerPreFinaleRetreat()` redirects all active raider armies to nearest spawn/exit point, then dissolves and self-destructs.
- Allied buildings set to `Targeting_None` so enemies don't get stuck; allied docks set invulnerable. Player AI resource bonus set to 1.0 for allies (players 3–6).

### Timers

| Rule/Timer | Interval | Purpose |
|------------|----------|---------|
| `OBJ_TutNaval` timer | 300s countdown (Hard+ only) | Tutorial time limit; 30s warning |
| `OBJ_RaidWaveIncoming` timer | `raiderWaveInterval * multiplier` | Visible countdown to next Crusader raid wave; warns at 15s |
| `OBJ_BufferFinalWave` timer | 60–300s (by difficulty) | Prep time before Reynald's final attack |
| `Raids_Monitor` | 2s | Checks if wave cleared, starts countdown to next wave |
| `Raid_NetManager` | 3s | Advances net fleet stages, handles dock-loss withdrawal |
| `_TradeConvoys_Manager` | 3s | Manages convoy routing, gold rewards, respawns |
| `_TradeConvoys_Launch` | 2s/4s/6s initial; 15s respawn | Staggers convoy launches and respawns after destruction |
| `DEMO_RAID_INTERVAL` | 300s | Demolition ship raid frequency |
| `raiderWaveCleanupTime` | 5–8 min (by difficulty) | Force-cleanup stale raid waves |
| `Pirates_CheckForPlayerSighting` | 3s | Check if player sees pirate units |
| `Pirates_Monitor` | Initial delay 55–115s, then 3s | Main pirate spawn/behavior loop |
| `Pirates_RebuildDock` | 5s | Check/rebuild pirate dock |
| `Pirates_EnablePlayerBaseDriveby` | 300s one-shot | Enable pirate near-player routes (Hard+) |
| `pirateRespawnDelay` | 15–90s (by difficulty) | Delay before new pirate fleet spawns |
| `Raids_ValidateFinalWave` | 1s | Polls until finale units are fully spawned |
| `Raids_DemolishersConfigureUI` | 5s one-shot | Delayed UI setup for demo ship objective |
| `VOCue_HistoryAyyubids` | 20s one-shot | Starting voice-over cue |
| `MissionTutorial_AddHintToSeaOutpost` | 7s one-shot | Delayed outpost training hint |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| core (`abb_m3_redsea.scar`) | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`, `abb_m3_redsea.events`, all 6 sub-files below |
| data | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar` |
| objectives | `cardinal.scar`, `missionomatic/missionomatic.scar` |
| raid | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| pirates | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| trade_convoys | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| training | `training/campaigntraininggoals.scar` |
| automated | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/modules/module_rovingarmy.scar`, `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals

| Global | Defined In | Used In |
|--------|-----------|---------|
| `player1`–`player6` | core | all files — player1=Ayyubid, player2=Crusader, player3=Pirates, player4-6=Allies |
| `t_difficulty` | data | raid, core, objectives, pirates |
| `t_tutorial`, `t_civilUnrest` | data | objectives, core |
| `RAIDER_WAVES`, `RAIDER_SPAWN_POINTS`, `RAIDER_ROUTES`, `RAIDER_NET_STAGES` | data | raid |
| `RAIDER_UNITS_*` tables | data | raid |
| `RAIDER_MARINES_*` constants | data | raid |
| `raider_unit_groups`, `raider_armies` | data (init) | raid (mutate), pirates (read) |
| `g_waveActive`, `g_finaleStarted`, `g_goldThresholdReached` | objectives | raid, core |
| `TRADE_CONVOY_GOLD` | data | trade_convoys |
| `RAID_LOCKOUT_GOLD_RATIO` | data | raid |
| `NAVAL_LOOT_TABLE`, `g_bootyIndex`, `g_pirateBootyCap`, `spawnPirateBooty` | data | core |
| `sg_intro_crusader`, `sg_camped_pirates` | map editor | core, pirates |
| `eg_dock_*`, `eg_pirate_camp`, `eg_pirate_dock` | map editor | core, objectives, pirates |
| `EVENTS.*` | events file | core (NIS/Intel: Intro, Victory, BuildShips, AccumulateGold, ExplainTrade, StakesRaised, PirateIsland, RazedPirateIsland, GoldTargetReached, UnrestCritical, ExplainUnrest) |
| Objective handles (`OBJ_*`, `SOBJ_*`) | objectives | raid, core, trade_convoys |

### Inter-file Function Calls

| Caller | Callee | Functions |
|--------|--------|-----------|
| core → data | `RedSea_InitData()` |
| core → objectives | `RedSea_RegisterObjectives()` |
| core → pirates | `Pirates_Init()` |
| core → trade_convoys | `TradeConvoys_Init()` |
| core → training | `MissionTutorial_AddHintToSeaOutpost()` |
| core → objectives | `ModifyCivilUnrest()` (on squad death) |
| core → core | `ActivateDockMegavision()` (also called from raid) |
| objectives → pirates | `Pirates_Start()` (from `OBJ_UnrestMeter.OnStart`) |
| objectives → raid | `Raids_Init()`, `Raids_LaunchRaiderWave()`, `Raids_LaunchFinalRaiderWave()`, `Raiders_TriggerPreFinaleRetreat()` |
| objectives → trade_convoys | `TradeConvoys_SendHome()` (from `OBJ_BufferFinalWave.OnStart`) |
| objectives → training | `MissionTutorial_TagDock()`, `MissionTutorial_UntagDock()` |
| objectives → raid | `VOCue_EnemyFlagShip_CTA()` |
| raid → objectives | `TallyTeamGoldDuringObjective()` |
| raid → data | `GetRaiderIndex()`, `GetRaiderUnits()` |
| data → MissionOMatic | `Army` modules, `UnitTable_CountUnits()`, `NavalArmy_Init()`, `Army_Init()`, `Army_SetTargets()` |
| automated → test framework | `CampaignAutotest_RegisterCheckpoint()`, `CampaignAutotest_SetCheckpointStatus()` |
| core → MissionOMatic | `PlayerUpgrades_ApplyHealthBonuses()` |
| core → automated | `FoodReserves_Init()` |
