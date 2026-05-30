# Challenge Mission: Basic Combat

## OVERVIEW

The Basic Combat challenge mission teaches players unit counter mechanics across 5 enemy attack waves. The player defends an HRE village against French attackers by selecting one of three production buildings (archery range, barracks, stable) to spawn a pre-set unit group (archers, spearmen, or horsemen), then the chosen army engages the incoming wave. Waves 1–3 require 1 unit group selection; waves 4–5 require 2. Performance is scored by a medal system (gold/silver/bronze) based on total units lost, with a secondary failure condition if too many village buildings are destroyed (max 7). A 4-shot pre-intro cinematic demonstrates unit matchups, formations, and micro techniques before gameplay begins.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_basiccombat.scar` | core | Main mission logic: wave spawning, army selection, objectives, victory/defeat, medal tracking, destruction callbacks |
| `challenge_mission_basiccombat_preintro.scar` | other (cinematic) | Pre-intro cinematic with 4 scripted battle vignettes demonstrating unit counters, formations, and retreat micro |
| `challenge_mission_basiccombat_training.scar` | training | Training goal system: meat-shield hint prompting player to place spearmen in front of archers |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | core | Registers wave functions, celebrations, attack delays; Xbox medal adjust |
| `Mission_OnGameSetup` | core | Gets player handles from world slots |
| `Mission_Preset` | core | Sets up players, diplomacy, FOW reveal |
| `Mission_PreStart` | core | Launches pre-intro cinematic, holds mission start |
| `Mission_Start` | core | Initializes objectives, events, rules, first wave timer |
| `ChallengeMission_SetupChallengePlayers` | core | Configures 4 players: local, enemy, village, training |
| `ChallengeMission_SetupDiplomacy` | core | Sets alliances and shared LOS between players |
| `ChallengeMission_SetupChallenge` | core | Zeroes resources, removes death/scuttle/garrison abilities |
| `ChallengeMission_InitStartingUnits` | core | Creates SGroups/EGroups for buildings and scout |
| `ChallengeMission_InitializeObjectives` | core | Registers and starts all objectives with counters |
| `ChallengeMission_InitializeWave` | core | Deploys leader units, adds recruit UI hints, resets flags |
| `ChallengeMission_FirstWave` | core | Spawns wave 1: 10 horsemen on East path |
| `ChallengeMission_SecondWave` | core | Spawns wave 2: 15 spearmen on North path |
| `ChallengeMission_SecondWaveHint` | core | Reveals stealth forest, CTA for ambush |
| `ChallengeMission_ThirdWave` | core | Spawns wave 3: 15 archers on South path |
| `ChallengeMission_FourthWave` | core | Spawns wave 4: 15 spearmen + 10 horsemen on East path |
| `ChallengeMission_FourthWaveHint` | core | Triggers meat shield training hint |
| `ChallengeMission_FifthWave` | core | Spawns wave 5: 15 archers + 10 horsemen on South path |
| `ChallengeMission_FifthWaveHint` | core | Reveals ridge, CTA for elevation advantage |
| `ChallengeMission_SendWave` | core | Issues formation attack-move along current path |
| `ChallengeMission_NextWave` | core | Transfers army to village, increments wave counter |
| `ChallengeMission_CleanUpWave` | core | Destroys current army, resets FOW |
| `ChallengeMission_ExtinguishFires` | core | Stops burning on village buildings between waves |
| `ChallengeMission_CleanUpDefense` | core | Destroys enemy wave, disables building selection |
| `ChallengeMission_IsDefenseSetup` | core | Returns true if enough unit groups selected (1 or 2) |
| `ChallengeMission_Update` | core | Polls building selection to trigger unit spawning |
| `ChallengeMission_OnDestruction` | core | GE_EntityKilled handler: medals, wave win/loss, building loss |
| `ChallengeMission_UpdateMedals` | core | Downgrades medal tier when unit loss threshold exceeded |
| `ChallengeMission_WaveWon` | core | Plays celebration event, completes wave sub-objective |
| `ChallengeMission_WaveLost` | core | Fails wave objective, burns 2 houses, checks defeat |
| `ChallengeMission_RespondToPlayerAttack` | core | Redirects AI to attack player units if engaged early |
| `ChallengeMission_CheckWave4Idle` | core | Nudges idle wave 4 enemies to resume attack-move |
| `ChallengeMission_RemindPlayer` | core | Prompts player if no army selected after 30s |
| `ChallengeMission_CheckVictory` | core | Stores KPI, completes primary objectives |
| `ChallengeMission_EndChallenge` | core | Plays outro intel, calls Mission_Complete |
| `ChallengeMission_Intro_RallyScout` | core | Moves scout along waypoints during intro |
| `ChallengeMission_Intro_Clean_Up` | core | Destroys intro scout |
| `ArcherLeaderSelected` | core | Spawns 15 archers for player army |
| `InfantryLeaderSelected` | core | Spawns 15 spearmen for player army |
| `CavalryLeaderSelected` | core | Spawns 10 horsemen for player army |
| `BasicCombat_PreIntro_Setup_Scenes` | preintro | Creates all SGroups for 4 cinematic shots |
| `BasicCombat_PreIntro_Shot01_Units` | preintro | Shot 1: village life with villagers and marching troops |
| `BasicCombat_PreIntro_Shot01_Train_Archer` | preintro | Spawns archer walking through village (delayed 3s) |
| `BasicCombat_PreIntro_Shot02_Units` | preintro | Shot 2: 20 spearmen vs 15 horsemen in formation |
| `BasicCombat_PreIntro_Shot02_Cavalry_Charge` | preintro | Horsemen form wedge and charge spearmen |
| `BasicCombat_PreIntro_Shot03_Units` | preintro | Shot 3: 20 archers ambush 10 spearmen |
| `BasicCombat_PreIntro_Shot03_Archer_Ambush` | preintro | Archers attack-move toward spearmen |
| `BasicCombat_PreIntro_Shot03_Archer_Retreat` | preintro | Splits archers, half retreat when under attack |
| `BasicCombat_PreIntro_Shot04_Units` | preintro | Shot 4: spearmen + horsemen vs spearmen + archers |
| `BasicCombat_PreIntro_Shot04_Archer_Attack` | preintro | Enemy archers join attack (delayed 1s) |
| `BasicCombat_PreIntro_Shot04_Cavalry_Charge` | preintro | Player horsemen charge flanking attack |
| `BasicCombat_PreIntro_Shot05_Units` | preintro | Shot 5: empty / unused |
| `BasicCombat_PreIntro_Clean_Scenes` | preintro | Destroys all squads from all players post-cinematic |
| `BasicCombatTrainingGoals_OnInit` | training | Registers meat-shield goal sequence |
| `TrainingGoal_EnableBasicCombatGoals` | training | Enables basic combat training goals |
| `TrainingGoal_DisableBasicCombatGoals` | training | Disables basic combat training goals |
| `UserHasSpearmenAndArchers` | training | Predicate: checks if meat-shield hint should trigger |
| `UserHasSelectedUnits` | training | Completion check: player has selected units |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `_challenge.victory.objectiveVictory` | OT_Primary | Defend camp against all 5 enemy attacks (counter: 0/5) |
| `_challenge.victory.objectiveVictory2` | OT_Primary | Do not let the enemy burn down the village |
| `_challenge.objective.surviveWave1` | OT_Bonus | Defeat approaching horsemen (wave 1) |
| `_challenge.objective.surviveWave2` | OT_Bonus | Defeat approaching spearmen (wave 2) |
| `_challenge.objective.surviveWave3` | OT_Bonus | Defeat approaching archers (wave 3) |
| `_challenge.objective.surviveWave4` | OT_Bonus | Defeat approaching spearmen + horsemen (wave 4) |
| `_challenge.objective.surviveWave5` | OT_Bonus | Defeat approaching archers + horsemen (wave 5) |
| `_challenge.objective.protectTown` | OT_Bonus | Track buildings lost (counter: 0/7, fail at 7) |
| `_challenge.benchmarks.gold.objective` | OT_Bonus | Lose fewer than 16 units (19 on Xbox) |
| `_challenge.benchmarks.silver.objective` | OT_Bonus | Lose fewer than 21 units (26 on Xbox) |
| `_challenge.benchmarks.bronze.objective` | OT_Bonus | Lose fewer than 36 units (41 on Xbox) |
| `_challenge.benchmarks.unplaced.objective` | OT_Bonus | No medal — exceeds bronze threshold |

### Difficulty

No `Util_DifVar` usage. Difficulty is implicit through the medal tier system:

| Medal | Max Units Died (PC) | Max Units Died (Xbox) |
|-------|---------------------|-----------------------|
| Gold | 15 | 18 |
| Silver | 20 | 25 |
| Bronze | 35 | 40 |

Xbox thresholds are relaxed in `Mission_OnInit` via `UI_IsXboxUI()` check. All players set to `AGE_FEUDAL`.

### Spawns

**Player Defenders** (spawned on building selection):

| Unit Type | Blueprint | Count | Building |
|-----------|-----------|-------|----------|
| Archers | `unit_archer_2_hre` | 15 | archeryRange |
| Spearmen | `unit_spearman_2_hre` | 15 | barracks |
| Horsemen | `unit_horseman_2_hre` | 10 | stable |

- Waves 1–3: player selects **1** unit group; waves 4–5: player selects **2** unit groups.
- Leader units (1 per building type) are deployed at village as selection targets with weapons disabled.
- Once defense is set up, remaining leaders are destroyed and the wave is sent after `attackDelay`.

**Enemy Waves** (French, Feudal Age):

| Wave | Units | Count | Path | Attack Delay |
|------|-------|-------|------|-------------|
| 1 | Horsemen (`unit_horseman_2_fre`) | 10 | East (3 waypoints) | 12s |
| 2 | Spearmen (`unit_spearman_2_fre`) | 15 | North (4 waypoints) | 30s |
| 3 | Archers (`unit_archer_2_fre`) | 15 | South (4 waypoints) | 12s |
| 4 | Spearmen + Horsemen (`unit_spearman_2_fre` + `unit_horseman_2_fre`) | 15 + 10 | East (4 waypoints) | 25s |
| 5 | Archers + Horsemen (`unit_archer_2_fre` + `unit_horseman_2_fre`) | 15 + 10 | South (4 waypoints) | 25s |

- All waves are FOW-revealed to the player for 30 seconds.
- Each wave triggers a minimap blip (`threat_group`) and a Call-to-Action event cue.
- Wave 2 triggers a stealth forest hint after 10s; wave 4 triggers a meat-shield training hint after 10s; wave 5 triggers a ridge/elevation hint after 10s.
- Wave 4 has an idle-check rule (`ChallengeMission_CheckWave4Idle`) polling every 1s to nudge stuck units near `enemy_waypoint2_East`.
- Wave 5 splits enemies into 2 separate SGroups with distinct rally points, merged before engagement.

### AI

- No `AI_Enable` or encounter plan usage. Enemy units follow scripted waypoint paths via `Cmd_FormationAttackMove`.
- `ChallengeMission_RespondToPlayerAttack`: Polls every 1.5s. If any enemy unit is under attack, all non-attacking enemies redirect to attack player units. If buildings are under attack, even attacking enemies re-target player units.
- Village buildings (excluding stables, archery ranges, barracks) have `Modify_TargetPriority` set to 100, making them high-priority targets for enemy pathfinding.
- When player army is destroyed (wave lost), 2 village houses are set to 1% HP (preferring undamaged ones). Fires are extinguished between waves via `ChallengeMission_ExtinguishFires`.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Rule_AddInterval(ChallengeMission_Update, 0.25)` | 0.25s | Polls building selection for unit spawning |
| `Rule_AddInterval(ChallengeMission_RespondToPlayerAttack, 1.5)` | 1.5s | Checks if AI should redirect to player units |
| `Rule_AddOneShot(ChallengeMission_FirstWave, revealDelay)` | 10s | Starts first wave after mission start |
| `Rule_AddOneShot(ChallengeMission_InitializeWave, revealDelay + selectionDelay)` | 15s | Opens unit selection UI after wave reveal |
| `Rule_AddOneShot(ChallengeMission_SendWave, attackDelay[wave])` | 12–30s | Sends player army to engage after selection complete |
| `Rule_AddOneShot(ChallengeMission_RemindPlayer, reminderDelay)` | 30s | Reminds player if no army selected |
| `Rule_AddOneShot(ChallengeMission_CleanUpWave, 5)` | 5s | Delayed cleanup of army after wave transition |
| `Rule_AddOneShot(ChallengeMission_SecondWaveHint, hintDelay)` | 10s | Stealth forest reveal for wave 2 |
| `Rule_AddOneShot(ChallengeMission_FourthWaveHint, hintDelay)` | 10s | Meat shield training hint for wave 4 |
| `Rule_AddOneShot(ChallengeMission_FifthWaveHint, hintDelay)` | 10s | Ridge elevation hint for wave 5 |
| `Rule_AddInterval(ChallengeMission_CheckWave4Idle, 1)` | 1s | Nudges idle wave 4 enemies (active waves 4–5) |
| `Rule_AddInterval(Mission_PreStart_IntroNISFinished, 0.125)` | 0.125s | Polls for pre-intro cinematic completion |

### Pre-Intro Cinematic System

The pre-intro consists of 4 choreographed battle shots (shot 5 is empty), each with setup functions:

| Shot | Theme | Player Units (local/village) | Enemy Units |
|------|-------|------------------------------|-------------|
| 1 | Village life | 9 villagers (cheering), 5 spearmen, 3 archers, 3 horsemen | — |
| 2 | Spearmen vs horsemen | 20 spearmen (line formation) | 15 horsemen (wedge) |
| 3 | Archer ambush + retreat | 20 archers (line formation) | 10 spearmen |
| 4 | Combined arms | 30 spearmen + 20 horsemen (player) | 25 spearmen + 15 archers (enemy) |
| 5 | (empty) | — | — |

- Shot 3 demonstrates micro: half the archers retreat when under attack, splitting based on proximity to enemy.
- Shot 4 features archers with spread formation joining delayed (1s), horsemen flanking immediately.

### Training System

Two goal sequences registered via `coretraininggoals.scar`:

| Goal Sequence ID | Trigger | Message |
|------------------|---------|---------|
| `meat_shield` | `_challenge.meatShieldHint` set to true (wave 4 hint) | "Place your Spearmen in front of your Archers to protect them." |
| `hold_ground` | Registered but no implementation shown in this batch | — |

- `UserHasSpearmenAndArchers` predicate activates when `_challenge.meatShieldHint` is true and player has squads.
- `UserHasSelectedUnits` completion check verifies the player has selected the target squad.

## CROSS-REFERENCES

### Imports

**core (`challenge_mission_basiccombat.scar`)**:
- `Cardinal.scar` — standard Cardinal framework
- `challenge_mission_basiccombat_training.scar` — training goals specific to this mission
- `challenge_mission_basiccombat_preintro.scar` — pre-intro cinematic

**preintro (`challenge_mission_basiccombat_preintro.scar`)**:
- `Cardinal.scar`

**training (`challenge_mission_basiccombat_training.scar`)**:
- `training/coretrainingconditions.scar` — shared training condition predicates
- `training/coretraininggoals.scar` — shared training goal framework
- Registers module via `Core_RegisterModule("BasicCombatTrainingGoals")`

### Shared Globals

- `_challenge` — central data table shared between core and training files; holds objectives, benchmarks, balance data, wave state, building EGroups, `meatShieldHint` flag
- `localPlayer`, `enemyPlayer`, `villagePlayer`, `trainingPlayer` — player handles used across all files
- `EVENTS` — event table from `.events` import, referenced in core for narration/celebrations
- `safeguard` — game-tick guard preventing duplicate wave win/loss processing in same tick
- `playerBuildingLost` — boolean flag for event completion tracking (gold medal + no buildings lost)
- `sg_preintro_*` — SGroups shared between preintro setup and cleanup functions
- `hintPoint_recruit1/2/3`, `HintPoint_StealthForest`, `HintPoint_Ridge` — UI hint point handles

### Inter-File Function Calls

- Core → Preintro: `BasicCombat_PreIntro_Setup_Scenes()` called from `Mission_PreStart`
- Core → Training: training module auto-initialized via `Core_RegisterModule("BasicCombatTrainingGoals")` calling `BasicCombatTrainingGoals_OnInit`
- Training → Core: reads `_challenge.meatShieldHint` to determine when to show meat-shield goal
- Core sets `_challenge.meatShieldHint = true` in `ChallengeMission_FourthWaveHint`, which training module polls
- Preintro has vestigial cleanup stubs referencing `EarlyEconomy_PreIntro_Shot03/04/05_Clean_Up` — likely copy-paste artifacts from another challenge mission

### Notable Implementation Details

- Uses `safeguard = World_GetGameTicks()` pattern to prevent `ChallengeMission_OnDestruction` from processing wave win/loss multiple times in the same game tick.
- Building selection polling (`ChallengeMission_Update`) only triggers spawning when exactly 1 building is selected and enemy units exist, preventing multi-select exploits.
- Village buildings are filtered to exclude military buildings (stable, archery_range, barracks) from the high-priority target pool.
- `GetRecipe()` function exists but is incomplete — only defines `outroNIS` with no return statement.
