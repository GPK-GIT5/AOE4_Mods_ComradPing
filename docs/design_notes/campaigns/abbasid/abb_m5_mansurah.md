# Abbasid Mission 5: Mansurah

## OVERVIEW

This mission is a two-phase Abbasid campaign scenario set in the Nile Delta in 1250. In Phase 1, the player controls spy units that must navigate an enemy Crusader camp to reach a messenger and send word for reinforcements — a stealth-oriented gameplay segment with ambush triggers and tutorial sequences. Upon signaling, a cinematic transition hands the player full control of Mansurah's defenses (player3 assets transfer to player1), beginning Phase 2: a prolonged siege defense against escalating Crusader invasion waves. The player must defend their landmarks (House of Wisdom) while optionally eliminating three Holy Order Grand Masters (Teuton, Hospitaller, Templar), whose deaths cause their armies to flee. After a 1500-second countdown timer, Baybars arrives with cavalry reinforcements, and the mission ends when the player destroys the enemy headquarters (leader tent).

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m5_mansurah.scar` | core | Main entry point; imports all sub-files, sets up players, tech tree, resources, events, and mission lifecycle |
| `abb_m5_mansurah_data.scar` | data | Defines all global constants, difficulty scaling, lane configs, holy orders, unit tables, defending armies, and invasion rounds |
| `abb_m5_mansurah_objectives.scar` | objectives | Registers and manages all OBJ_ objectives, kill-tracking event handlers |
| `abb_m5_mansurah_camp.scar` | spawns | Pool/Member/Wander/Lighthouse/Rest/Patrol system — manages enemy camp ambient life and unit cycling |
| `abb_m5_mansurah_invasion.scar` | spawns | Invasion wave queue/launch/retreat system with cost-based unit scaling |
| `abb_m5_mansurah_singles.scar` | spawns | Spawns individual/small-group Crusader patrols and stationary guards across the map |
| `abb_m5_mansurah_training.scar` | training | Tutorial goal sequences for Spy, Stealth Strike, Pickup, Farmhouse, and Appoint Spy mechanics |
| `abb_m5_mansurah_transition.scar` | other | Handles Phase 1→2 transition: spy arrival detection, asset transfer, objective sequencing, Baybars arrival |
| `abb_m5_mansurah_automated.scar` | automated | Automated test harness with checkpoint monitoring for CI/CD validation |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Configure 3 players, colors, alliances, age caps |
| `Mission_SetupVariables` | core | Call `InitData1()` to initialize globals |
| `Mission_Preset` | core | Tech tree, upgrades, villagers, spawns, event hooks |
| `Mission_PreStart` | core | Register objectives, set starting resources, audio mapping |
| `Mission_Start` | core | Start intro intel, initial objectives, tutorials |
| `GetRecipe` | core | Return MissionOMatic config (NIS, audio, title card) |
| `Ambush_Spawn` | core | Create left/right cavalry ambush armies near spy path |
| `Ambush_Monitor` | core | Trigger ambush on proximity or bait death |
| `Ambush_Trigger` | core | Add attack targets to ambush armies, reveal FOW |
| `SpawnCampFollowers` | core | Spawn camp follower units into pools |
| `SpawnHolyOrders` | core | Init Army for each holy order with patrol targets |
| `SpawnDefendingArmies` | core | Init all 34 defending Army instances |
| `BaybarsArrives` | core | Spawn Baybars leader + cavalry reinforcement waves |
| `BaybarsArrives_B` | core | Staggered spawning of 10 rows of reinforcements |
| `RemoveGatherSpeedModifications` | core | Remove economic gather rate modifiers at transition |
| `StartMonitoringResources` | core | Lock resource deposit amounts until transition |
| `PrintReport` | core | Debug: log player/enemy unit counts every 60s |
| `OnAbilityExecuted` | core | Handle farmhouse ungarrison ability |
| `skipBaybarsTimer` | core | Debug: reduce Baybars timer to 20s |
| `InitData1` | data | Define all mission globals, constants, timers, lanes |
| `InitData2` | data | Define camp follower units, 14 invasion rounds |
| `Camp_Init` | camp | Initialize 7 pools, building/map-edge trainers |
| `Camp_Monitor` | camp | Per-tick pool monitoring loop |
| `Camp_SpawnUnitsIntoPools` | camp | Spawn units directly into assigned pools |
| `Camp_SpawnUnitsFromBuildings` | camp | Queue units via building trainer with delay |
| `Camp_SpawnUnitsFromMapEdge` | camp | Queue units via map edge trainer |
| `Camp_MusterCohort` | camp | Release all cohort members from pools into sgroup |
| `Camp_AssignPools` | camp | Distribute units across valid pools randomly |
| `Pool_Init` | camp | Initialize pool state and lighthouse chances |
| `Pool_Monitor` | camp | Process idle members, count, reinforce followers |
| `Pool_MonitorFollowers` | camp | Detect dead followers, queue replacements |
| `Pool_ReleaseMembers` | camp | Extract cohort members from all subsystems |
| `Wander_Init` | camp | Create area-weighted wander system |
| `Wander_Monitor` | camp | Detect idle wanderers, return to pool idle |
| `Lighthouse_Init` | camp | Create lighthouse with entry/queue/discharge slots |
| `Lighthouse_AddMember` | camp | Send member to lighthouse via waypoints |
| `Lighthouse_MemberEnters` | camp | Destroy squad, set stay timer, mark occupied |
| `Lighthouse_MemberExits` | camp | Recreate squad after stay, discharge to wander |
| `Lighthouse_ReleaseMembers` | camp | Extract cohort from all lighthouse states |
| `Rest_Init` | camp | Create rest area with positional slots |
| `Rest_AddMember` | camp | Assign member to random open slot with timer |
| `Patrol_Init` | camp | Create patrol route from named markers |
| `Patrol_AddMember` | camp | Queue attack-move along patrol markers |
| `Member_Init` | camp | Create member record with SBP-based capability flags |
| `Member_AssignNewActivity` | camp | Weighted random: lighthouse/rest/patrol/wander |
| `Member_FindAvailableLighthouse` | camp | Probability-weighted lighthouse assignment |
| `Member_FindAvailableRest` | camp | Probability-weighted rest assignment |
| `Member_FindAvailablePatrol` | camp | Probability-weighted patrol assignment |
| `SpawnCampInvaders` | invasion | Pre-spawn first 2 invasion cohorts into pools/muster |
| `GetNextRound` | invasion | Cycle through rounds, wrapping last ROUNDS_REPEATED |
| `Invasion_Init` | invasion | Create invasion object with round+lane+sgroup |
| `Invasion_QueueAndLaunch` | invasion | Queue next invasion from map edge, launch current |
| `Invasion_LimitMaxUnits` | invasion | Scale wave size based on active enemy cost |
| `Invasion_Muster` | invasion | Pull cohort from pools into army formation |
| `Invasion_Launch` | invasion | Transfer blocked army, add lane targets |
| `Invasion_OnArmyBlocked` | invasion | Retreat blocked army to staging area |
| `Invasion_RetreatComplete` | invasion | Merge retreated units into army_blocked |
| `Invasion_GetLane` | invasion | Random lane selection without repeat |
| `Man_RegisterObjectives` | objectives | Define and register all 9 objective tables |
| `StartInitialObjectives` | objectives | Start dummy + SendForHelp objectives |
| `OnEntityKilled` | objectives | Detect headquarters destruction |
| `OnSquadKilled` | objectives | Track leader kills, trigger HolyOrder_Flee |
| `HolyOrder_Flee` | objectives/transition | Dissolve holy order army, stagger flee movement |
| `HolyOrder_SingleMemberFlees` | objectives/transition | Move individual fleeing members to map edge |
| `SpawnSingles` | singles | Spawn all single/multiple patrol units from markers |
| `Single_Init` | singles | Create single unit with patrol/stationary/AI mode |
| `Single_MonitorPatrol` | singles | Bounce-patrol between markers with idle delay |
| `Single_MonitorStationary` | singles | Return stationary units to assigned marker |
| `Singles_Monitor` | singles | Monitor 10 singles per frame for performance |
| `Multiple_Init` | singles | Initialize multi-unit patrol group |
| `Multiple_Change` | singles | Redirect multiple group 2 post-ambush |
| `Fire_Init` | singles | Spawn units at campfire marker positions |
| `RemoveScoutBlocker` | singles | Convert scout blocker to patrol at transition |
| `Tutorials_Init` | training | Initialize all 5 tutorial goal sequences |
| `SpyTutorial_Init` | training | Spy stealth auto-enter tutorial |
| `StealthStrikeTutorial_Init` | training | Spy stealth damage bonus tutorial |
| `PickupTutorial_Init` | training | Spy resource pickup reveals stealth tutorial |
| `FarmhouseTutorial_Init` | training | Farmhouse garrison tutorial |
| `AppointSpyTutorial_Init` | training | Shajar al-Durr appoint spy ability tutorial |
| `Transition_MonitorSpy` | transition | Detect spy reaching signal messenger |
| `Transition_SpyArrived` | transition | Complete spy objectives, disable spy targeting |
| `Transition_ResumeGameplay` | transition | Full phase transition: transfer assets, spawn camp, start defense |
| `Transition_ResumeGameplay_Objetives` | transition | Start destroy/eliminate/tip objectives after 7s |
| `Transition_ResumeGameplay_HelpSoon` | transition | Start Baybars countdown objective after 27s |
| `AutoTest_OnInit` | automated | Check command line, enable AI, register checkpoints |
| `Automated_RegisterCheckpoints` | automated | Register PlayStart/BaibarsSignaled/MissionComplete |
| `Automated_Phase1_Monitor` | automated | Wait for OBJ_SendForHelp completion |
| `Automated_CheckForTransitionComplete` | automated | Spawn test armies after transition |
| `Automated_CreateArmy` | automated | Create crossbowman/mangonel/knight test forces |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DummyBattle` | Battle (secret) | Hidden objective for UI element anchoring |
| `OBJ_DummyPrimary` | Primary (secret) | Hidden objective for UI element anchoring |
| `OBJ_SendForHelp` | Primary | Phase 1 goal: bring spy to messenger (parent) |
| `OBJ_BringSpy` | Primary | Sub-objective: move spy to signal trigger proximity |
| `OBJ_DefendMansurah` | Information | Phase 2 fail condition: all landmarks destroyed |
| `OBJ_DestroyTheHeadquarters` | Primary | Phase 2 win condition: destroy enemy leader tent |
| `OBJ_EliminateTheLeaders` | Optional | Kill all 3 Grand Masters (counter-tracked) |
| `OBJ_GrandMasterTip` | Tip | "A Holy Order will flee if their leader is eliminated" |
| `OBJ_BaybarsArrivingSoon` | Optional | Countdown timer (1500s) until Baybars arrives |

### Difficulty

All values use `Util_DifVar({ Easy, Normal, Hard, Expert })`:

| Parameter | Easy | Normal | Hard | Expert | Scaling |
|-----------|------|--------|------|--------|---------|
| `ENEMY_REINFORCEMENT_DELAY` | -1 (off) | -1 (off) | 800 | 400 | Seconds before dead camp followers respawn |
| `INVASION_DELAY_AFTER_TRANSITION` | 200 | 180 | 160 | 140 | Seconds before first invasion wave |
| `INVASION_INTERVAL` | 300 | 270 | 240 | 210 | Seconds between invasion waves |
| `COST_UPPER` | 900 | 1200 | 1750 | 2400 | Max resource cost threshold for active enemies |
| Front army unit counts | 5 | 6 | 9 | 12 | Per-army squad count for defending/camp units |
| Holy order Teuton count | 14 | 16 | 22 | 28 | Teuton holy order member count |
| Holy order Hosp/Temp count | 7 | 8 | 11 | 14 | Hospitaller/Templar member counts |
| Starting resources (wood/food) | 350 | 300 | 250 | 200 | Player starting resources |
| Starting stone | 150 | 100 | 50 | 0 | Player starting stone |
| Military build time modifier | 0.5 | 0.75 | 1 | 1 | Ayyubid military build time multiplier |
| Attack lanes | North only | North only | W/N/E | W/N/E | Number of invasion approach lanes |
| Enemy military upgrades | 0 | 0 | 1 | 2 | Tiered military upgrade level for player2 |
| `DEFAULT_IDLE_DELAY` (singles) | 3 | 2.5 | 2 | 1.5 | Patrol idle delay for single units |

### Spawns

**Camp Followers**: 7 pools — `pool_tents` (infantry), `pool_tents_siege` (siege), `pool_field_west/east/south` (cavalry with patrols), `pool_home` (elite guards), `pool_home_master` (Grand Master bodyguard). Units cycle between Wander → Idle → Rest/Lighthouse/Patrol activities with weighted random selection.

**Singles**: Individual Crusader units (militia, archers, scouts, knights, holy order members) spawned at specific markers. Support stationary, bounce-patrol, and looping patrol modes. 3 multi-unit groups (scouts + knights) also created. 10 singles monitored per frame for performance.

**Holy Orders**: 3 orders (Teuton, Hospitaller, Templar) with Army-controlled member groups and individual Grand Masters in pools. Killing a master causes all members to flee to map edge.

**Defending Armies**: 34 Army instances positioned around the Crusader camp (front armies 01–16 + defend 01–09 + armies 09–34). Patrol-mode with custom directions and idle times.

**Invasion Waves**: 14 defined rounds with escalating compositions (militia/rams → knights/trebuchets/mangonels). Rounds cycle with last `ROUNDS_REPEATED` (4) repeating. 2 invasions pre-spawned into pools/muster. Cost-based scaling (`Invasion_LimitMaxUnits`) reduces wave size when active enemies exceed threshold. Blocked armies retreat and merge into `army_blocked` staging group.

**Baybars Reinforcements**: 10 rows spawned at 0.75s intervals — 5 rows of knights + 5 rows of Turkic horse archers. Reinforcement file count (3–5 per row) scales with player population.

### AI

- `AI_Enable(player1, true)` — only in automated test mode
- `Army_Init` used extensively for defending armies, holy orders, ambush squads, and invasion forces
- Ambush system: 2 cavalry armies triggered by spy proximity or bait kill
- `army_blocked` — staging army for retreated invasion forces, re-launched with next wave
- Holy orders use `TARGET_ORDER_PATROL` with large combat/leash ranges (45/85)
- Camp pool system creates ambient AI life without using AI_Enable — behavior driven by weighted random activity assignment

### Timers

| Timer/Rule | Delay | Purpose |
|------------|-------|---------|
| `Camp_Monitor` | 1s interval | Pool idle/follower monitoring |
| `Wander_Monitor` | 1s interval | Detect idle wanderers |
| `Lighthouse_Monitor` | 1s interval | Queue advancement, validate members |
| `Lighthouse_MonitorEnrouteMember` | 0.25s interval | Detect enroute member arrival |
| `Lighthouse_MonitorEnteringMember` | 0.25s interval | Detect member entry completion |
| `Lighthouse_MemberExits` | `LIGHTHOUSE_STAY_TIME` (30s) one-shot | Eject occupant after stay |
| `Rest_Monitor` | 1s interval | Check rest stay timers, release members |
| `Patol_Monitor` | 1s interval | Detect idle patrollers |
| `Singles_Monitor` | every frame (Rule_Add) | Monitor 10 singles per tick |
| `Invasion_QueueAndLaunch` | `INVASION_DELAY_AFTER_TRANSITION` then `INVASION_INTERVAL` | Spawn + launch invasion waves |
| `Invasion_Muster` | `INVASION_INTERVAL - INVASION_MUSTER_DURATION` (varies) | Muster next pending cohort |
| `Invasion_MonitorIncomingInvasion` | 1s interval | Detect wave reaching arrival marker |
| `Invasion_MonitorRetreatingInvasion` | 0.5s interval | Detect retreat completion |
| `Transition_MonitorSpy` | per frame (Rule_Add) | Check spy proximity to messenger |
| `Transition_ResumeGameplay_Objetives` | 7s one-shot | Start Phase 2 objectives |
| `Transition_ResumeGameplay_HelpSoon` | 27s one-shot | Start Baybars countdown |
| `Transition_ResumeGameplay_Autosave` | 29s one-shot, then 600s interval | Autosave schedule |
| `Transition_ResumeGameplay_SpyHint` | 34s one-shot | Enable appoint spy tutorial |
| `BAIBARS_DELAY` | 1500s (25 min) | Countdown until Baybars arrives |
| `BaybarsArrives_B` | 0.75s interval | Stagger reinforcement row spawning |
| `MonitorResources` | 1s interval | Lock resource deposits pre-transition |
| `PrintReport` | 60s interval | Debug unit count logging |
| `HolyOrder_SingleMemberFlees` | 0.375s interval | Stagger individual flee movement |
| `LEADER_SETUP_TIME` | 80s | Grand Master setup delay |
| `SHAJAR_ABILITY_DELAY` | 20s | Delay before Shajar ability available |
| `VOCue_BaybarsSelected` | 1s interval | Detect player selecting Baybars for VO |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `abb_m5_mansurah.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/missionomatic_leadertent.scar`, all 8 sub-files |
| `abb_m5_mansurah_data.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m5_mansurah_objectives.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar` |
| `abb_m5_mansurah_camp.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m5_mansurah_invasion.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m5_mansurah_singles.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m5_mansurah_training.scar` | `training.scar`, `training/campaigntraininggoals.scar`, `cardinal.scar`, `missionomatic/missionomatic.scar` |
| `abb_m5_mansurah_transition.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m5_mansurah_automated.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`; conditionally: `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals

| Global | Defined In | Used In |
|--------|-----------|---------|
| `player1`, `player2`, `player3` | core | all files |
| `sg_spies` | prefab/core | objectives, transition, training, automated, core |
| `sg_masters` | data | objectives (kill tracking), core (spawn) |
| `holy_orders` | data | objectives (OnSquadKilled), core (SpawnHolyOrders), transition (Camp_AddMaster) |
| `rounds` | data (InitData2) | invasion (GetNextRound) |
| `lanes`, `all_lanes` | data | invasion (Invasion_GetLane) |
| `pending_invasions`, `active_invasions` | data | invasion, core (PrintReport) |
| `enemy_leaders_killed`, `enemy_headquarters_killed` | data | objectives |
| `pools`, `pool_tents`, `pool_home`, etc. | camp/data | camp, invasion, data |
| `army_blocked` | data | invasion (staging), core (PrintReport) |
| `singles`, `multiples` | singles | objectives (OnComplete removes multiple), core |
| `WALK_SPEED` | data | camp, singles |
| `BAIBARS_DELAY` | data | objectives (timer), transition |
| `INVASION_DELAY_AFTER_TRANSITION`, `INVASION_INTERVAL`, `INVASION_MUSTER_DURATION` | data | invasion |
| `ENEMY_REINFORCEMENT_DELAY` | data | camp (Pool_MonitorFollowers) |
| `camp_follower_units` | data (InitData2) | core (SpawnCampFollowers) |
| `defending_armies` | data | core (SpawnDefendingArmies) |
| `siege_started_at` | transition | core (PrintReport) |
| `stop_reinforcing_resources` | transition | core (MonitorResources) |
| `OBJ_*` constants | objectives | transition, core, automated |
| `sg_shajar` | prefab/core | training (AppointSpyTutorial) |
| `EVENTS.*` | MissionOMatic events | objectives, core, transition |
| `invaders_spawned` | invasion | invasion (Invasion_QueueAndLaunch guard) |
| `invasion_delay_pending` | objectives | invasion (delay on 3 leaders killed) |

### Inter-File Function Calls

| Caller File | Calls Function In |
|-------------|-------------------|
| core → data | `InitData1()`, `InitData2()` |
| core → objectives | `Man_RegisterObjectives()`, `StartInitialObjectives()` |
| core → camp | `Camp_Init()` (via data) |
| core → singles | `SpawnSingles()`, `RemoveScoutBlocker()` |
| core → training | `Tutorials_Init()`, `SpyTutorial_Enable()`, `StealthStrikeTutorial_Enable()`, `PickupTutorial_Enable()`, `FarmhouseTutorial_Enable()`, `AppointSpyTutorial_Enable()` |
| core → transition | via `Rule_Add(Transition_MonitorSpy)` from objectives |
| core → invasion | `SpawnCampInvaders()` (from transition) |
| transition → camp | `SpawnCampFollowers()` → `Camp_SpawnUnitsIntoPools()` |
| transition → invasion | `SpawnCampInvaders()`, `Invasion_QueueAndLaunch()` |
| transition → singles | `RemoveScoutBlocker()` |
| transition → training | `AppointSpyTutorial_Enable()` |
| invasion → camp | `Camp_SpawnUnitsFromMapEdge()`, `Camp_MusterCohort()`, `Camp_SpawnUnitsIntoMuster()`, `Camp_SpawnUnitsIntoPools()` |
| objectives → singles | Removes `multiples[1]` on spy completion |
| objectives → camp | `Camp_AddMaster()` (via holy_orders post-spy) |
| data → camp | `Camp_Init()` called during `InitData1()` |
