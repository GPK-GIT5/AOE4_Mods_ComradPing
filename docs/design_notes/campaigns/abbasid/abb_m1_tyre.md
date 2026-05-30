# Abbasid Mission 1: Siege of Tyre

## OVERVIEW

**abb_m1_tyre** is the first Abbasid campaign mission. The player controls Turkic horse archers led by Tughtekin, raiding Frankish (Crusader) camps to disrupt resource gathering, then establishing a base, aging up, and ultimately destroying a massive siege engine called "The Beast." The mission flows through distinct phases: raid enemy camps → build economy/base → countdown timer while Franks construct the ram → defend Tyre and destroy the ram. The Franks (player2) gather resources, construct The Beast via scripted build states, then march it along a land bridge ("the mole") toward Tyre while skirmish armies harass the player's base. Four players are configured: Damascenes (player, Dark Age), Franks (enemy, Feudal), and two Tyre allies (Castle Age). Difficulty scales enemy villager speed, garrison limits, ambush timing, resource targets, and unit counts across 4 levels via `Util_DifVar`.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| abb_m1_tyre.scar | core | Main mission orchestrator: player setup, phase transitions, skirmish armies, ram/escort army management, upgrade restrictions, and debug utilities |
| abb_m1_tyre_ambush.scar | spawns | Defines 4 proximity-triggered ambush encounters with attack/guard armies along the raiding path |
| abb_m1_tyre_automated.scar | automated | Automated test harness that AI-drives the player through all 3 mission phases with checkpoint validation |
| abb_m1_tyre_camps.scar | core | Manages 4 Frankish camps with villager gathering, flee/garrison AI, resource tracking, and camp-clear detection |
| abb_m1_tyre_data.scar | data | Initializes all globals, SGroups, difficulty parameters (`t_diff`), and the MissionOMatic recipe with all army modules |
| abb_m1_tyre_objectives.scar | objectives | Registers all objectives (clear camps, age up, harvest, produce units, assault countdown, destroy ram) and fail conditions |
| abb_m1_tyre_training.scar | training | Tutorial goal sequences for Tughtekin's ability, Leader Tent, dock selection, villager production, and House of Wisdom wing |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | abb_m1_tyre.scar | Configures 4 players, ages, relationships, colors |
| Mission_Preset | abb_m1_tyre.scar | Applies upgrades, modifiers, production restrictions by difficulty |
| Mission_PreStart | abb_m1_tyre.scar | Registers all mission objectives |
| Mission_Start | abb_m1_tyre.scar | Starts initial objectives, ram army init, first intel |
| Tyre_StartBasePhase | abb_m1_tyre.scar | Transfers base to player, spawns villagers, starts econ phase |
| Tyre_InitSkirmishArmy | abb_m1_tyre.scar | Configures enemy skirmish army with escalating unit mixes |
| Tyre_MonitorSkirmishing | abb_m1_tyre.scar | State machine: spawn→attack→disband→retreat cycle (enemy) |
| Tyre_InitAllySkirmishArmy | abb_m1_tyre.scar | Configures ally skirmish army with archer-based composition |
| Tyre_MonitorAllySkirmishing | abb_m1_tyre.scar | State machine: spawn→attack→disband→retreat cycle (ally) |
| Tyre_InitRamArmy | abb_m1_tyre.scar | Initializes "The Beast" army params and escort references |
| Tyre_SpawnEscorts | abb_m1_tyre.scar | Creates 3 escort armies with speed-limited units |
| Tyre_ReinforceEscorts | abb_m1_tyre.scar | Adds units to escorts using enemy resource stockpile |
| Tyre_SpawnRamBuilders | abb_m1_tyre.scar | Deploys 10 special villagers to construct The Beast |
| Tyre_ConstructRamTower | abb_m1_tyre.scar | Orders ram builders to construct siege tower entity |
| Tyre_RamTowerComplete | abb_m1_tyre.scar | Replaces construct entity with real ram tower unit |
| Tyre_SpawnRam | abb_m1_tyre.scar | Spawns The Beast, applies difficulty modifiers, reveals to player |
| Tyre_LaunchRam | abb_m1_tyre.scar | Starts ram army movement, sets escort phase to "escort" |
| Tyre_MonitorRam | abb_m1_tyre.scar | Tracks ram progress, updates escort targets, spawns garrison |
| Tyre_CheckMoleTrigger1 | abb_m1_tyre.scar | Splits escorts at first palisade on the mole |
| Tyre_CheckMoleTrigger2 | abb_m1_tyre.scar | Splits escorts at second palisade on the mole |
| Tyre_CheckRamTrigger | abb_m1_tyre.scar | Triggers ram garrison spawn when escorts thin or ram damaged |
| Tyre_SpawnRamGarrison | abb_m1_tyre.scar | Spawns garrison waves (MAA + militia) near ram |
| Tyre_ModifyRamHealth | abb_m1_tyre.scar | Applies health multiplier to ram based on difficulty |
| Tyre_StartFinalRetreat | abb_m1_tyre.scar | Dissolves all enemy armies and retreats to camp |
| Tyre_SpawnTransport | abb_m1_tyre.scar | Spawns ally transport ship with reinforcements |
| Tyre_CheckTransportArrival | abb_m1_tyre.scar | Deploys spearmen/archers/horsemen when transport arrives |
| Tyre_SpawnAllyDefenders | abb_m1_tyre.scar | Scatters ally archers and militia across Tyre |
| Tyre_SpawnWallArchers | abb_m1_tyre.scar | Spawns 17 militia archers along Tyre's walls |
| Tyre_StartPreparing | abb_m1_tyre.scar | Initializes ally skirmish army, starts wall archer movement |
| Tyre_MonitorHorseArcherCount | abb_m1_tyre.scar | Triggers horse archer objective if count drops below 50% |
| Tyre_MonitorTughtekin | abb_m1_tyre.scar | Detects Tughtekin death/respawn, triggers leader tent training |
| Tyre_SpawnScatteredUnits | abb_m1_tyre.scar | Utility: spawns units at all markers sharing a name |
| Ambushes_Init | abb_m1_tyre_ambush.scar | Configures 4 ambush tables with armies/destinations, starts monitor |
| Ambushes_Monitor | abb_m1_tyre_ambush.scar | Checks proximity triggers and dispatches ambush attack armies |
| Ambush_DestinationIsTriggered | abb_m1_tyre_ambush.scar | Returns destination marker if player squads are nearby |
| Ambushes_SpawnAlliedMonks | abb_m1_tyre_ambush.scar | Spawns 3 allied monks at markers after ambush 1 cleared |
| AutoTest_OnInit | abb_m1_tyre_automated.scar | Entry point for campaign autotest command-line mode |
| AutomatedTyre_RegisterCheckpoints | abb_m1_tyre_automated.scar | Registers 4 timed autotest checkpoints with timeout values |
| AutomatedMission_Start | abb_m1_tyre_automated.scar | Builds raid target list, starts raider monitor loop |
| AutomatedTyre_MonitorRaiders | abb_m1_tyre_automated.scar | Reinforces and targets AI raiders at enemy camp sgroups |
| AutomatedTyre_InitBuildUp | abb_m1_tyre_automated.scar | Creates defender army, assigns villagers, starts build-up phase |
| AutomatedTyre_MonitorBuildUp | abb_m1_tyre_automated.scar | Adds resources, spawns defenders, maintains unit count |
| AutomatedTyre_BuildHouseOfWisdom | abb_m1_tyre_automated.scar | Commands villager to construct House of Wisdom |
| AutomatedTyre_InitDestroyRam | abb_m1_tyre_automated.scar | Creates attacker army with upgrades for final assault |
| AutomatedTyre_MonitorDestroyRam | abb_m1_tyre_automated.scar | Periodically spawns attacker reinforcements during ram phase |
| AutomatedTyre_SpawnAttackers | abb_m1_tyre_automated.scar | Creates mixed spear/archer/horseman squads for attack army |
| Camps_Init | abb_m1_tyre_camps.scar | Creates 4 camps, 9 villager groups, cost modifiers, starts monitor |
| Camps_AddUI | abb_m1_tyre_camps.scar | Attaches objective UI markers to each camp |
| Camps_UpdateUI | abb_m1_tyre_camps.scar | Checks camp clear conditions, updates counter, triggers VO |
| Camp_CreateVillagers | abb_m1_tyre_camps.scar | Spawns villagers at group marker, applies speed modifier |
| Camp_AssignWork | abb_m1_tyre_camps.scar | Commands villager group to gather appropriate resource type |
| Camps_MonitorEntry | abb_m1_tyre_camps.scar | Waits for player proximity to any camp, activates subsystems |
| Camps_MonitorVillagers | abb_m1_tyre_camps.scar | State machine: gather→flee→wait→idle→construct for villagers |
| Camps_GatherResources | abb_m1_tyre_camps.scar | Accumulates enemy resources based on active gatherer count |
| Camps_RetreatAll | abb_m1_tyre_camps.scar | Sends all villagers and camp armies to retreat marker |
| Tyre_InitData1 | abb_m1_tyre_data.scar | Initializes all SGroups, globals, constants, and t_diff table |
| GetRecipe | abb_m1_tyre_data.scar | Returns MissionOMatic recipe with armies, intro/outro NIS, title card |
| Tyre_InitData2 | abb_m1_tyre_data.scar | Calls Camps_Init and conditionally Ambushes_Init |
| Tyre_GetMarkers | abb_m1_tyre_data.scar | Returns array of sequential markers matching a stem name |
| Tyre_RegisterObjectives | abb_m1_tyre_objectives.scar | Defines and registers all OBJ/SOBJ/TOBJ objective tables |
| Tyre_MonitorResources | abb_m1_tyre_objectives.scar | Tracks player gather rates, triggers PrepareForAttack early |
| Tyre_CheckDestroyRamStart | abb_m1_tyre_objectives.scar | Waits for ram spawn flag, then starts OBJ_DestroyRam |
| Training_Tyre_GeneralAura | abb_m1_tyre_training.scar | Tutorial for selecting Tughtekin and viewing his ability |
| Training_Tyre_LeaderTent | abb_m1_tyre_training.scar | Tutorial for Leader Tent when Tughtekin dies |
| Training_Tyre_BuildFishingBoat | abb_m1_tyre_training.scar | Tutorial for selecting dock to build fishing boat |
| Training_Tyre_ProduceVillagers | abb_m1_tyre_training.scar | Tutorial reminder when TC idle 60s with <20 villagers |
| Training_Tyre_BuildWing | abb_m1_tyre_training.scar | Tutorial for selecting HoW and starting a wing upgrade |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_HorseArchers | Information (fail) | Horse archers must survive; triggers Mission_Fail if all die |
| OBJ_DefendLandmarks | Information (fail) | Landmarks must survive; superseded by OBJ_DefendTyre later |
| OBJ_DefendTyre | Information (fail) | Tyre Town Center must survive during final phase |
| OBJ_ClearCamps | Primary | Clear 4 Frankish camps (counter 0/4) |
| SOBJ_EliminateGuardsAndGatherers | Primary (sub) | Sub-objective of ClearCamps — eliminate guards and gatherers |
| OBJ_FranksGathering | Information | Tracks enemy resource accumulation toward attack threshold |
| OBJ_AssaultCountdown | Information | 360-second countdown while Franks construct "The Beast" |
| TOBJ_EnemyConstructing | Tip | Tip displayed during assault countdown |
| OBJ_PauseMenu | Tip | Suggests viewing pause menu for mission info |
| OBJ_AgeUp | Primary | Advance to Feudal Age (requires HoW + Wing) |
| OBJ_HouseOfWisdom | Primary (sub) | Build a House of Wisdom |
| OBJ_Wing | Primary (sub) | Build a Wing on the House of Wisdom |
| OBJ_PrepareForAttack | Primary | Prepare defenses — complete via harvest OR unit production |
| OBJ_BuildUpStockpile | Primary (sub) | Harvest 6000 resources total |
| OBJ_ProduceUnits | Primary (sub) | Reach 80 population |
| OBJ_DestroyRam | Battle | Destroy "The Beast" siege engine to win |
| SOBJ_RamHP | Primary (sub) | Progress bar showing ram remaining health |
| OBJ_DefendMole | Primary | Position army at the mole to defend Tyre |

**Win condition:** Destroy "The Beast" (OBJ_DestroyRam complete) → `Mission_Complete()`.
**Lose condition:** Player horse archers all dead OR player landmarks destroyed OR Tyre TC destroyed → `Mission_Fail()`.

### Difficulty

| Parameter | Easy → Expert | What it scales |
|-----------|---------------|----------------|
| villager_speed | 0.8 → 1.0 | Enemy villager movement speed multiplier |
| villager_reaction_delay | 4 → 2.5s | Delay before villagers flee from player |
| camp_max_garrison | 1 → 4 | Max villagers garrisoning per outpost |
| skirmish_spawn_delay | 15 → 4s | Delay between skirmish wave spawns |
| skirmish_attack_threshold | 10 → 20 | Unit count before skirmish army attacks |
| skirmish_unit_mix_cap | 1 → 6 | Cap on advanced unit types in skirmish waves |
| ram_weapon_cooldown | 2 → 1s | Ram attack cooldown |
| ram_health_multiplier | 1 → 1.5 | Ram HP multiplier |
| research_level | 1 → 4 | Enemy tech level |
| ambushes_trigger | false → true | Whether ambushes activate (only Hard/Hardest) |
| ambush_delay | 120 → 30s | Time after trigger before ambush army attacks |
| enemy_resource_target | 2000 → 5000 | Resources Franks need before assault starts |
| enemy_gather_delay | 20 → 7s | Interval for enemy resource accumulation tick |
| numSquads_* | varies | 20+ scaling parameters for army/escort/ram unit counts |

### Spawns

**Camps**: 4 camps with patrol armies (militia, horsemen, spearmen) sized by difficulty. Individual archers/spearmen/MAA/horsemen/crossbowmen/knights placed at marker positions within camp radius.

**Villager Groups**: 9 groups across 4 camps gathering wood/food/gold (3–5 villagers each). State machine: gather → flee → garrison outpost or scatter → idle → return to work.

**Ambushes**: 4 ambush pairs (attack + guard army). Attack armies use horsemen, MAA, spearmen, or knights (0–4 squads). Triggered by player proximity.

**Escort Armies**: 3 escort groups with militia/MAA/archers/horsemen/knights. Reinforced from resource stockpile with cost-based unit requests. Speed reduced to 40% when not in combat.

**Skirmish Armies**: Enemy spawns from production buildings; escalating unit mix from militia/archer → knight/MAA/archer. Ally skirmish: max 14 units (archers + spearmen).

**Ram System**: 10 special villagers construct siege tower → replaced with real ram tower unit → The Beast spawns with health multiplier → marches along mole with 3 escort armies → garrison waves spawn when escorts thin or ram health < 75%.

**Static Defenders**: Ally archers and militia scattered across Tyre; 17 wall archers along walls. Transport ship delivers 5 spearmen + 5 archers + 5 horsemen.

### AI

- **Automated testing**: Full AI takeover via `AI_Enable(player1, true)` + `Game_AIControlLocalPlayer()` during autotest.
- **Villager AI**: Custom state machine — gather, flee, garrison, attack-move, reconstruct, return to work.
- **Army modules**: All enemy armies use `Army_Init` via MissionOMatic recipe with `TARGET_ORDER_PATROL` or `TARGET_ORDER_LINEAR`.
- **Ram army**: `TARGET_ORDER_LINEAR` along mole toward Tyre; escorts dynamically retarget based on ram progress.
- **Escort splitting**: At mole trigger points, escort armies diverge to north/south/center attack paths.
- **Final retreat**: All enemy armies dissolve into retreat group and move to camp.

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| Ambushes_Monitor | 2s | Checks ambush proximity triggers |
| Camps_MonitorEntry | 1s | Waits for player to approach any camp |
| Camps_MonitorVillagers | 2s | Runs villager state machine |
| Camps_GatherResources | 7–20s (difficulty) | Accumulates enemy resources |
| Camps_UpdateUI | 1s | Camp-clear detection and UI updates |
| Tyre_MonitorResources | 1s | Player resource tracking for harvest objective |
| OBJ_AssaultCountdown | 360s countdown | Time until Frankish assault |
| Tyre_MonitorSkirmishing | 2s | Enemy skirmish state machine |
| Tyre_MonitorAllySkirmishing | 4s | Ally skirmish state machine |
| Tyre_MonitorRam | 2s | Ram progress and garrison spawning |
| Tyre_ReinforceEscorts | 2s | Add units to escorts from resource pool |
| Tyre_SpawnRamGarrison | 0.75s | Spawn garrison units near ram |

## CROSS-REFERENCES

### Imports
- All files import `cardinal.scar` and `MissionOMatic/MissionOMatic.scar`.
- `abb_m1_tyre_training.scar` imports `training/campaigntraininggoals.scar`.
- `abb_m1_tyre_automated.scar` conditionally imports `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar`.
- `abb_m1_tyre.scar` imports all other mission files plus `abb_m1_tyre.events`.

### Shared Globals
- **base_phase_started**: Boolean flag gating base-building systems (set in core, read by automated/camps/objectives).
- **enemy_resource_stockpile / enemy_resource_total**: Franks' economy tracking (shared across camps/objectives/automated).
- **ram_has_spawned**: Signals ram existence to objectives.
- **escort_phase**: State variable for escort army behavior ("prepare"→"escort"→"mole1"→"mole2"→"final").
- **t_diff**: Difficulty parameter table (defined in data, used everywhere).
- **sg_p1_horse_archers, sg_tughtekin**: Player unit groups (defined in data, used in objectives/training/core).
- **OBJ_ClearCamps, OBJ_AssaultCountdown, OBJ_DestroyRam**: Objective constants (defined in objectives, checked across files).

### Inter-File Function Calls
- Core → Data: `Tyre_InitData1()`, `Tyre_InitData2()`, `FoodReserves_Init()`.
- Core → Objectives: `Tyre_RegisterObjectives()`.
- Core → Training: `Training_Tyre_GeneralAura()`, `Training_Tyre_LeaderTent()`, etc.
- Data → Camps: `Camps_Init()`.
- Data → Ambush: `Ambushes_Init()`.
- Objectives → Camps: `Camps_AddUI()`, `Camps_RetreatAll()`.
- Objectives → Training: `Training_Tyre_BuildWing()`.
