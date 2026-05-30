# Challenge Mission: Advanced Combat

## OVERVIEW

The Advanced Combat challenge mission teaches players unit counter mechanics across 6 enemy attack waves. The player defends an HRE village against Abbasid attackers by selecting production buildings to spawn pre-set unit groups (archers, crossbowmen, spearmen, men-at-arms, horsemen, knights), then the chosen army auto-engages the incoming wave. Each wave introduces a different unit composition, requiring the player to pick effective counters. Performance is scored by a medal system (gold/silver/bronze) based on total units lost, with a secondary failure condition if too many village buildings are destroyed (max 7). An elaborate 6-shot pre-intro cinematic demonstrates unit matchups and formations before gameplay begins.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_advancedcombat.scar` | core | Main mission logic: wave spawning, army selection, objectives, victory/defeat, medal tracking, destruction callbacks |
| `challenge_mission_advancedcombat_preintro.scar` | other (cinematic) | Pre-intro cinematic with 6 scripted battle vignettes demonstrating unit counters and formations |
| `challenge_mission_advancedcombat_automated.scar` | automated | Automated smoke-test harness: registers checkpoints per wave, auto-selects buildings, and commands player units to attack |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | core | Registers wave functions, celebrations, attack delays; Xbox medal adjust |
| `Mission_Preset` | core | Sets up players and diplomacy |
| `Mission_PreStart` | core | Spawns starting units, launches pre-intro cinematic |
| `Mission_Start` | core | Initializes objectives, events, rules, hint points |
| `ChallengeMission_SetupChallengePlayers` | core | Configures 5 players: local, enemy, village, 2 training |
| `ChallengeMission_SetupDiplomacy` | core | Sets alliances and shared LOS between players |
| `ChallengeMission_SetupChallenge` | core | Zeroes resources, removes death/scuttle/garrison abilities |
| `ChallengeMission_InitStartingUnits` | core | Creates SGroups/EGroups for buildings and leader units |
| `ChallengeMission_InitializeObjectives` | core | Registers and starts all objectives with counters |
| `ChallengeMission_InitializeWave` | core | Adds recruit UI hints, resets defense flags per wave |
| `ChallengeMission_FirstWave` | core | Spawns wave 1: 10 men-at-arms on path 1 |
| `ChallengeMission_SecondWave` | core | Spawns wave 2: 10 crossbowmen on path 2 |
| `ChallengeMission_ThirdWave` | core | Spawns wave 3: 5 knights on path 3 |
| `ChallengeMission_FourthWave` | core | Spawns wave 4: 15 spearmen + 10 crossbowmen on path 2 |
| `ChallengeMission_FifthWave` | core | Spawns wave 5: 10 men-at-arms + 10 horsemen on path 3 |
| `ChallengeMission_SixthWave` | core | Spawns wave 6: 15 archers + 5 knights on path 1 |
| `ChallengeMission_SixthWave_Split` | core | Knights split off to attack-move at path waypoint 4 |
| `ChallengeMission_SendWave` | core | Issues formation attack-move along current path |
| `ChallengeMission_NextWave` | core | Transfers army to village, increments wave counter |
| `ChallengeMission_CleanUpWave` | core | Destroys current army, resets defense flags |
| `ChallengeMission_IsDefenseSetup` | core | Returns true if enough unit groups selected (1 or 2) |
| `ChallengeMission_DefenseGroupsRemaining` | core | Returns how many more groups player must select |
| `ChallengeMission_Update` | core | Polls building selection to trigger unit spawning |
| `ChallengeMission_OnDestruction` | core | GE_EntityKilled handler: medals, wave win/loss, building loss |
| `ChallengeMission_UpdateMedals` | core | Downgrades medal tier when unit loss threshold exceeded |
| `ChallengeMission_WaveWon` | core | Plays celebration event, completes wave sub-objective |
| `ChallengeMission_WaveLost` | core | Fails wave objective, burns 2 houses, checks defeat |
| `ChallengeMission_RespondToPlayerAttack` | core | Redirects AI to attack player units if engaged early |
| `ChallengeMission_IncreaseBuildingVulnerability` | core | Accelerates building damage when under attack |
| `ChallengeMission_UpdateBuildingSpawner` | core | Handles unit spawn or undo on building selection |
| `ChallengeMission_RemoveProductionUI` | core | Removes recruit/undo hint points by unit type |
| `ChallengeMission_CheckVictory` | core | Stores KPI, completes primary objectives |
| `ChallengeMission_EndChallenge` | core | Plays outro intel, calls Mission_Complete |
| `ChallengeMission_BuildingLost` | core | Plays lost-building intel events |
| `ChallengeMission_RemindPlayer` | core | Prompts player if no army selected after 30s |
| `ChallengeMission_StealthForestHint` | core | CTA for stealth forest ambush opportunity |
| `ChallengeMission_CliffsHint` | core | CTA for cliffs terrain advantage |
| `ChallengeMissionDeployDummyUnits` | core | Deploys 6 leader units at village with weapons disabled |
| `ArcherLeaderSelected` | core | Spawns 15 archers for player army |
| `CrossbowmanLeaderSelected` | core | Spawns 10 crossbowmen for player army |
| `SpearmanLeaderSelected` | core | Spawns 15 spearmen for player army |
| `ManatarmsLeaderSelected` | core | Spawns 10 men-at-arms for player army |
| `HorsemanLeaderSelected` | core | Spawns 10 horsemen for player army |
| `KnightLeaderSelected` | core | Spawns 5 knights for player army |
| `ArcFormation` | core | Arranges units in curved line between two positions |
| `AdvancedCombat_PreIntro_Setup_Scenes` | preintro | Creates all SGroups for 6 cinematic shots |
| `AdvancedCombat_PreIntro_Shot01_Units` | preintro | Shot 1: HRE crossbowmen fire at targets, knights parade |
| `AdvancedCombat_PreIntro_Shot02_Units` | preintro | Shot 2: HRE men-at-arms vs Abbasid mixed force |
| `AdvancedCombat_PreIntro_Shot03_Units` | preintro | Shot 3: HRE crossbowmen kite Abbasid men-at-arms |
| `AdvancedCombat_PreIntro_Shot04_Units` | preintro | Shot 4: HRE knights charge into crossbowmen/spearmen |
| `AdvancedCombat_PreIntro_Shot05_Units` | preintro | Shot 5: Abbasid knights circle with men-at-arms march |
| `AdvancedCombat_PreIntro_Shot06_Units` | preintro | Shot 6: Full battle — spearmen hold, crossbows retreat, knights flank |
| `AdvancedCombat_PreIntro_Clean_Scenes` | preintro | Destroys all squads from all players post-cinematic |
| `AutomatedMission_Start` | automated | Entry point for autotest, called from Mission_Start |
| `AutomatedMission_SetupCheckpoints` | automated | Registers 7 checkpoints (6 waves + victory), 150s limit each |
| `AutomatedMission_Update` | automated | Polls objective status, triggers auto-spawn per wave |
| `AutomatedMission_UpdateCheckpoints` | automated | Checks pass/fail/timeout for each checkpoint |
| `AutomatedMission_Attack` | automated | Auto-commands player units to attack-move enemies |
| `AutomatedMission_FormationMove` | automated | Regroups player units then resumes attack after 10s |
| `AutomatedMission_Spawn_Wave1` | automated | Selects stable2 to trigger knight spawn |
| `AutomatedMission_Spawn_Wave2` | automated | Selects stable1 to trigger horseman spawn |
| `AutomatedMission_Spawn_Wave3` | automated | Selects barracks1 to trigger spearman spawn |
| `AutomatedMission_Spawn_Wave4` | automated | Selects barracks2 then stable1 (two groups) |
| `AutomatedMission_Spawn_Wave5` | automated | Selects barracks2 then archeryRange2 (two groups) |
| `AutomatedMission_Spawn_Wave6` | automated | Selects barracks1 then stable2 (two groups) |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `_challenge.victory.objectiveVictory` | OT_Primary | Defend camp against all 6 enemy attacks (counter: 0/6) |
| `_challenge.victory.objectiveVictory2` | OT_Primary | Do not let the enemy burn down the village |
| `_challenge.objective.surviveWave1` | OT_Bonus | Defeat approaching men-at-arms (wave 1) |
| `_challenge.objective.surviveWave2` | OT_Bonus | Defeat approaching crossbowmen (wave 2) |
| `_challenge.objective.surviveWave3` | OT_Bonus | Defeat approaching knights (wave 3) |
| `_challenge.objective.surviveWave4` | OT_Bonus | Defeat approaching spearmen + crossbowmen (wave 4) |
| `_challenge.objective.surviveWave5` | OT_Bonus | Defeat approaching men-at-arms + horsemen (wave 5) |
| `_challenge.objective.surviveWave6` | OT_Bonus | Defeat approaching archers + knights (wave 6) |
| `_challenge.objective.trainWave1–6` | ObjectiveType_Information | Prompt to train 1 or 2 unit groups |
| `_challenge.objective.protectTown` | OT_Bonus | Track buildings lost (counter: 0/7, fail at 7) |
| `_challenge.benchmarks.gold.objective` | OT_Bonus | Lose fewer than 15 units (18 on Xbox) |
| `_challenge.benchmarks.silver.objective` | OT_Bonus | Lose fewer than 30 units (35 on Xbox) |
| `_challenge.benchmarks.bronze.objective` | OT_Bonus | Lose fewer than 40 units (45 on Xbox) |
| `_challenge.benchmarks.unplaced.objective` | OT_Bonus | No medal — exceeds bronze threshold |

### Difficulty

No `Util_DifVar` usage. Difficulty is implicit through the medal tier system:

| Medal | Max Units Died (PC) | Max Units Died (Xbox) |
|-------|---------------------|-----------------------|
| Gold | 15 | 18 |
| Silver | 30 | 35 |
| Bronze | 40 | 45 |

Xbox thresholds are relaxed in `Mission_OnInit` via `UI_IsXboxUI()` check.

### Spawns

**Player Defenders** (spawned on building selection):

| Unit Type | Blueprint | Count | Building |
|-----------|-----------|-------|----------|
| Archers | `unit_archer_3_hre` | 15 | archeryRange1 |
| Crossbowmen | `unit_crossbowman_3_hre` | 10 | archeryRange2 |
| Spearmen | `unit_spearman_3_hre` | 15 | barracks1 |
| Men-at-Arms | `unit_manatarms_3_hre` | 10 | barracks2 |
| Horsemen | `unit_horseman_3_hre` | 10 | stable1 |
| Knights | `unit_knight_3_hre` | 5 | stable2 |

- Waves 1–3: player selects **1** unit group; waves 4–6: player selects **2** unit groups.
- Selection can be undone by re-clicking the same building; resets all spawned units.

**Enemy Waves** (Abbasid, Castle Age):

| Wave | Units | Count | Path | Formation |
|------|-------|-------|------|-----------|
| 1 | Men-at-Arms (`unit_manatarms_3_generic_abb`) | 10 | path1 (5 waypoints) | default |
| 2 | Crossbowmen (`unit_crossbowman_3_abb`) | 10 | path2 (8 waypoints) | line |
| 3 | Knights (`unit_knight_3_abb`) | 5 | path3 (6 waypoints) | default |
| 4 | Spearmen (`unit_spearman_3_abb`) + Crossbowmen (`unit_crossbowman_3_abb`) | 15 + 10 | path2 | default |
| 5 | Men-at-Arms (`unit_manatarms_3_generic_abb`) + Horsemen (`unit_horseman_3_abb`) | 10 + 10 | path3 | wedge |
| 6 | Archers (`unit_archer_3_abb`) + Knights (`unit_knight_3_abb`) | 15 + 5 | path1 | default; knights split at waypoint 4 |

- All waves are FOW-revealed to the player for 30 seconds.
- Each wave triggers a minimap blip (`threat_group`) and a Call-to-Action event cue.
- Wave 4 triggers a stealth forest hint after 10s; wave 5 triggers a cliffs hint after `hintDelay` (10s).

### AI

- No `AI_Enable` or encounter plan usage. Enemy units follow scripted waypoint paths via `Cmd_FormationAttackMove`.
- `ChallengeMission_RespondToPlayerAttack`: If any enemy unit is under attack, all non-attacking enemies redirect to attack player units. If the player attacks early with only 1 of 2 required groups, the wave is sent immediately.
- `ChallengeMission_SixthWave_Split`: Wave 6 knights break off and attack-move independently once near waypoint 4 (within 37 range).
- `ChallengeMission_IncreaseBuildingVulnerability`: Polls every 0.5s during waves 2 and 4; any village building under attack loses 2.5% HP per tick, accelerating destruction.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Rule_AddInterval(ChallengeMission_Update, 0.25)` | 0.25s | Polls building selection for unit spawning |
| `Rule_AddInterval(ChallengeMission_RespondToPlayerAttack, 1.5)` | 1.5s | Checks if AI should redirect to player units |
| `Rule_AddOneShot(ChallengeMission_FirstWave, revealDelay)` | 10s | Starts first wave after mission start |
| `Rule_AddOneShot(ChallengeMission_InitializeWave, revealDelay + selectionDelay)` | 15s | Opens unit selection UI after wave reveal |
| `Rule_AddOneShot(ChallengeMission_SendWave, attackDelay[wave])` | 10s | Sends player army to engage after selection complete |
| `Rule_AddOneShot(ChallengeMission_RemindPlayer, reminderDelay)` | 30s | Reminds player if no army selected |
| `Rule_AddOneShot(Mission_Fail, missionEndDelay)` | 15s | Delayed mission failure after too many buildings lost |
| `Rule_AddInterval(Mission_PreStart_IntroNISFinished, 0.125)` | 0.125s | Polls for pre-intro cinematic completion |
| `Rule_AddInterval(ChallengeMission_IncreaseBuildingVulnerability, 0.5)` | 0.5s | Accelerates building damage (waves 2, 4) |
| `Rule_AddInterval(AutomatedMission_Update, 0.25)` | 0.25s | Autotest: polls objectives, triggers auto-spawns |
| `Rule_AddOneShot(AutomatedMission_FormationMove, 3)` | 3s | Autotest: regroups then attacks after 10s |

### Pre-Intro Cinematic System

The pre-intro consists of 6 choreographed battle shots, each with setup/cleanup functions:

| Shot | Theme | Player Units (HRE/village) | Enemy Units (Abbasid) |
|------|-------|---------------------------|----------------------|
| 1 | Crossbow drill + knight parade | 9 crossbowmen, 6 knights, 10 men-at-arms | 3 invulnerable/hidden targets |
| 2 | Men-at-arms vs mixed force | 16 men-at-arms | 6 spearmen, 8 archers (50% HP), 8 horsemen (50% HP) |
| 3 | Crossbow kiting | 16 crossbowmen (50% dmg reduction) | 16 men-at-arms (70% HP) |
| 4 | Knight charge vs ranged/spear | 7 knights | 12 crossbowmen, 12 spearmen |
| 5 | Enemy muster | — | 10 knights (circling), 20 men-at-arms |
| 6 | Full combined-arms battle | 10 knights, 10 crossbowmen, 20 spearmen | 10 knights, 20 men-at-arms |

## CROSS-REFERENCES

### Imports

**core (`challenge_mission_advancedcombat.scar`)**:
- `Cardinal.scar` — standard Cardinal framework
- `training/coretraininggoals.scar` — training goal system (disabled: `TrainingGoal_DisableAgeUpGoals`, `DisableCoreControlGoals`, `DisableCoreEconGoals`)
- `challenge_mission_advancedcombat.events` — event definitions (EVENTS table)
- `challenge_mission_advancedcombat_preintro.scar` — pre-intro cinematic
- `challenge_mission_advancedcombat_automated.scar` — automated testing

**preintro (`challenge_mission_advancedcombat_preintro.scar`)**:
- `Cardinal.scar`

**automated (`challenge_mission_advancedcombat_automated.scar`)**:
- `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`

### Shared Globals

- `_challenge` — central data table shared between core and automated files; holds objectives, benchmarks, balance data, wave state, building EGroups
- `localPlayer`, `enemyPlayer`, `villagePlayer`, `trainingPlayer`, `trainingPlayer2` — player handles used across all files
- `EVENTS` — event table from `.events` import, referenced in core for narration/celebrations

### Inter-File Function Calls

- Core → Preintro: `AdvancedCombat_PreIntro_Setup_Scenes()` called from `Mission_PreStart`
- Core → Automated: `AutomatedMission_Start()` called from `Mission_Start` when `CampaignAutoTest` command-line arg is present
- Automated → Core: reads `_challenge.objective.*` and `_challenge.victory.*` for checkpoint status; references `_challenge.stable1/2`, `_challenge.barracks1/2`, `_challenge.archeryRange2` to trigger building selection
- Preintro → Core: `AdvancedCombat_Intro_Cleanup()` called indirectly via `Mission_PreStart_IntroNISFinished`
- Automated uses `CampaignAutotest_RegisterCheckpoint` and `CampaignAutotest_SetCheckpointStatus` — external autotest framework functions
