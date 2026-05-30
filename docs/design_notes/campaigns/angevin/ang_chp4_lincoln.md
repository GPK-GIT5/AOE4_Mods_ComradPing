# Angevin Chapter 4: Lincoln

## OVERVIEW

Lincoln (1217) is a siege-defense-then-counterattack mission where the player (William Marshal / English) must defend Lincoln Castle's keep against rebel assaults, then destroy both rebel and French military infrastructure. The mission opens with a 6-minute timed defense phase before William Marshal arrives with knight reinforcements. After his arrival the player can capture the neutral hamlet of Stowe for additional resources and villagers. Rebels attack from three strongpoints, each with a Defend module and a RovingArmy attack wave that escalates over time. The French operate from two fortified camps (Fort A/West and Fort B/East) that activate sequentially and send increasingly powerful waves — including siege towers — toward the castle. Victory requires destroying all 6 rebel military production buildings AND all structures in both French forts.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp4_lincoln_data.scar` | data | Initializes all globals, SGroups, EGroups, unit composition tables, wave data for 3 rebel + 2 French waves, French attack path tables, and the MissionOMatic recipe with all Defend/RovingArmy modules |
| `ang_chp4_lincoln.scar` | core | Main mission script — imports, 5-player setup, difficulty config, restrictions, reinforcement spawning, wave management, fort proximity checks, keep monitoring, win/fail logic, outro |
| `ang_chp4_lincoln_training.scar` | training | Defines a training goal sequence prompting the player to view keep upgrades; checks for keep selection and timeout |
| `obj_defeat_french.scar` | objectives | Defines OBJ_DefeatFrench (primary) with sub-objectives SOBJ_DestroyFortWest and SOBJ_DestroyFortEast; tracks fort building destruction counters; wall-breach stingers |
| `obj_defeat_rebels.scar` | objectives | Defines OBJ_DefeatRebels (primary) with a 0/6 military building destruction counter; triggers French attack at halfway mark |
| `obj_defend_keep.scar` | objectives | Defines OBJ_DefendKeep (information) — activated when keep first takes damage; adds UI hint on keep |
| `obj_reinforcements.scar` | objectives | Defines OBJ_Reinforce1 (information) — 360s countdown timer; on completion spawns William Marshal + knights, activates Fort A |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Lincoln2_Data_Init` | data | Initializes all globals, SGroups, wave data, path tables |
| `GetRecipe` | data | Returns MissionOMatic recipe with all modules and locations |
| `Lincoln2_AddKeepUpgradesGoal` | training | Registers keep-upgrade training goal sequence |
| `ShouldPromptUpgradesHint` | training | Checks if player owns a keep and timer elapsed |
| `UserHasViewedUpgradeTraining` | training | Completes goal after keep selection or 25s timeout |
| `UserHasSelectedAKeep` | training | Returns true if player has a keep selected |
| `Mission_SetupPlayers` | core | Configures 5 players, ages, relationships, resources |
| `Mission_SetDifficulty` | core | Builds t_difficulty table with 10 Util_DifVar params |
| `Mission_SetRestrictions` | core | Removes scuttle, upgrades outposts, locks/unlocks buildings |
| `Mission_Preset` | core | Inits objectives, units, forts, walls, wave build times |
| `Mission_Start` | core | Adds kill/fail/win rules, starts rebel waves and timer |
| `Lincoln2_InitStartingUnits` | core | Deploys player archers, MAA, villagers; rebel intro archers |
| `Lincoln2_SetupFrenchForts` | core | Spawns crossbow/archer clusters at both fort markers |
| `Lincoln2_InitCollapsedWalls` | core | Destroys wall bastions near collapse markers |
| `Lincoln2_SetManualTargeting` | core | Sets rebel houses/gates to manual targeting |
| `Lincoln2_GarrisonOutposts` | core | Spawns archers and garrisons all outpost EGroups |
| `Lincoln2_ClearIntroUnits` | core | Destroys intro enemy SGroups after NIS |
| `Lincoln2_InitRebels` | core | Spawns initial rebel units into RovingArmy modules |
| `Lincoln2_CheckMissionFail` | core | Fails mission if keep is destroyed |
| `Lincoln2_CheckMissionWin` | core | Wins if both OBJ_DefeatRebels and OBJ_DefeatFrench complete |
| `Lincoln2_CheckKeep` | core | Starts OBJ_DefendKeep on first damage; intel at 50% |
| `Lincoln2_CheckRebelWaves` | core | Dispatches waves for each uncleared rebel strongpoint |
| `Lincoln2_CheckRebelWave` | core | Prepares a single rebel wave with siege cap enforcement |
| `Lincoln2_CheckRebelPrematureAttack` | core | Launches queued waves if player scouts strongpoints |
| `Lincoln2_CheckRebelBuildingProx` | core | Starts OBJ_DefeatRebels when player nears rebel areas |
| `Lincoln2_TrackMilitaryBuildings` | core | Adds UI hints/blips for all rebel military buildings |
| `Lincoln2_CheckStrongpoints` | core | Clears strongpoint flags when all buildings destroyed |
| `Lincoln2_CheckFrenchSightTrigger` | core | Enables fort proximity checks when French first sighted |
| `Lincoln2_CheckFortProxA` | core | Reveals Fort A FOW, starts defeat French objective |
| `Lincoln2_CheckFortProxB` | core | Reveals Fort B FOW, starts defeat French objective |
| `Lincoln2_InitFrenchAttack` | core | Sends initial French wave toward south gate |
| `Lincoln2_InitFrenchActivity` | core | Sets french_active flag, starts arrival check rule |
| `Lincoln2_ActivateFortA` | core | Starts French wave A interval, schedules Fort B |
| `Lincoln2_ActivateFortB` | core | Starts French wave B interval |
| `Lincoln2_CheckFrenchWaveA` | core | Dispatches wave from Fort A with cycling targets |
| `Lincoln2_CheckFrenchWaveB` | core | Dispatches wave from Fort B |
| `Lincoln2_CheckFrenchWave` | core | Prepares French wave with unit cap; sets siege tower paths |
| `Lincoln2_GetFrenchWaveTargets` | core | Cycles through french_targets table by difficulty |
| `Lincoln2_CheckFrenchArrival` | core | Triggers CTA when French reach south gate area |
| `Lincoln2_StartDefeatFrench` | core | Starts OBJ_DefeatFrench if keep not failed |
| `Lincoln2_CheckFrenchFirstAttack` | core | Starts defeat French obj after initial wave eliminated |
| `Lincoln2_SpawnReinforcements1` | core | Deploys 3 cavalry groups + William Marshal hero |
| `Lincoln2_MoveReinforcements1` | core | Formation-moves cavalry to destination markers |
| `Lincoln2_WilliamMarshalCTA` | core | Plays triumph stinger and celebrate CTA |
| `Lincoln2_CheckStoweTrigger` | core | Transfers Stowe to player on proximity; grants resources |
| `Lincoln2_OnEntityKilled` | core | Master kill handler — fort counters, rebel building tracking, wall breach |
| `Lincoln2_TriggerOutro` | core | Calls Mission_Complete for victory |
| `Lincoln2_OutroSetup` | core | Deploys William Marshal + army for outro NIS |
| `Lincoln2_SpawnUnitLine` | core | Spawns units along numbered marker line |
| `Lincoln2_SpawnUnitCluster` | core | Spawns a unit cluster at a named marker |
| `Lincoln2_InitDebugComplete` | core | Registers a cheat objective for debug victory |
| `DefeatFrench_InitObjectives` | obj_defeat_french | Registers OBJ_DefeatFrench, SOBJ_DestroyFortWest/East |
| `FortWestOnWallDown` | obj_defeat_french | Plays stinger on first Fort A wall breach |
| `FortEastOnWallDown` | obj_defeat_french | Plays stinger on first Fort B wall breach |
| `DefeatRebels_InitObjectives` | obj_defeat_rebels | Registers OBJ_DefeatRebels with 0/6 counter |
| `DefendKeep_InitObjectives` | obj_defend_keep | Registers OBJ_DefendKeep (information type) |
| `Reinforcements_InitObjectives` | obj_reinforcements | Registers OBJ_Reinforce1 with 360s countdown |
| `Reinforce1_TimerComplete` | obj_reinforcements | Completes OBJ_Reinforce1 after timer expires |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Reinforce1` | Information | 360s countdown — defend castle until William Marshal arrives |
| `OBJ_DefendKeep` | Information | Activated on first keep damage; mission fails if keep destroyed |
| `OBJ_DefeatRebels` | Primary | Destroy all 6 rebel military production buildings (counter 0/6) |
| `OBJ_DefeatFrench` | Primary | Destroy both French forts; parent of two sub-objectives |
| `SOBJ_DestroyFortWest` | Primary (sub) | Destroy all buildings/outposts in Fort A (west/south); counter tracked |
| `SOBJ_DestroyFortEast` | Primary (sub) | Destroy all buildings/outposts in Fort B (east); counter tracked |
| `OBJ_DebugComplete` | Primary (cheat) | Debug-only; triggers instant outro |

### Difficulty

All values use `Util_DifVar({easy, standard, hard, hardest})`:

| Parameter | Easy | Standard | Hard | Hardest | What it scales |
|-----------|------|----------|------|---------|----------------|
| `enemyTargetLevel` | 0 | 0 | 1 | 2 | French attack path complexity (easy/medium/hard tables) |
| `enemyUnitBuildTime` | 13 | 11 | 9 | 7 | Wave infantry unit build time (seconds) |
| `siegeUnitBuildTime` | 35 | 30 | 25 | 20 | Wave siege unit build time (seconds) |
| `rebelWaveInterval` | 130 | 110 | 90 | 80 | Seconds between rebel wave dispatches |
| `rebelSiegeMax` | 3 | 4 | 6 | 8 | Max rebel siege weapons alive at once |
| `frenchWaveInterval` | 600 | 400 | 340 | 280 | Seconds between French wave dispatches |
| `rebelDefenderCount` | 5 | 5 | 10 | 15 | Squads per rebel Defend module unit type |
| `frenchDefenderCount` | 3 | 4 | 7 | 10 | Squads per French fort Defend module unit type |
| `enemyInitUnitIndex` | 1 | 1 | 2 | 3 | Starting index into escalating unit_tables |
| `enemyEndUnitIndex` | 3 | 4 | 6 | 8 | Maximum index into unit_tables (wave cap) |

Additional difficulty-based scaling:
- `strongpoint_unit_cap`: `Util_DifVar({30, 30, 40, 50})` — max rebel units near a strongpoint before wave is suppressed
- `french_unit_cap`: `Util_DifVar({70, 70, 85, 100})` — max French units near a fort before wave is suppressed
- Easy mode spawns extra wall archers (markers 8–12) and 4 additional villagers

### Spawns

**Rebel Waves (3 channels):**
- `rebel_wave_1` (spawn: `mkr_rebels_attack1`): Crossbowmen + archers with rams; escalates to springalds and mangonels. 8 unit table entries. Staging → `RebelDefenders1`, assault → `RebelAttack1` targeting crossroads → north gate → castle north.
- `rebel_wave_2` (spawn: `mkr_rebels_attack2`): Spearmen + MAA with rams; escalates to mangonels. 8 entries. Assault → `RebelAttack2` targeting crossroads → tower2 → castle north.
- `rebel_wave_3` (spawn: `mkr_rebels_attack3`): Crossbowmen/archers with rams; escalates to 8 squads. 8 entries. Assault → `RebelAttack3` targeting tower3 → castle north.
- Waves are dispatched every `rebelWaveInterval` seconds. Siege weapon count is capped at `rebelSiegeMax`. Waves suppressed if strongpoint unit count exceeds cap.
- Strongpoints cleared when all military buildings near their Defend marker are destroyed; clears wave channel.

**French Waves (2 channels):**
- `french_wave_a` (spawn: `mkr_fort_a`): Spearmen + crossbowmen + springalds + siege towers; escalates to 15 spearmen + 15 crossbowmen + mangonels. 8 entries. Assault → `FrenchAttackA` with difficulty-based cycling target paths.
- `french_wave_b` (spawn: `mkr_fort_b`): Horsemen/knights + crossbowmen + mangonels; escalates to 15 cavalry + 15 crossbowmen + 15 MAA. 8 entries. Assault → `FrenchAttackB` targeting eastroad → west field → castle.
- Fort A activates at t=350s (just before reinforcements). Fort B activates 600s after Fort A.
- French waves dispatched every `frenchWaveInterval` (+ 30s offset for wave B).
- Siege tower waves use dedicated `french_targets_st` paths toward castle assault markers.

**Initial French Attack:**
- Triggered when 3 of 6 rebel buildings are destroyed (or on proximity); spawns 1 springald + 5 spearmen + 5 crossbowmen toward south gate.

**Starting Units:**
- Player: 5 villagers, 4 archers, 12 MAA, plus 12 archers along wall markers.
- Stowe villagers (neutral): 5 farmers, 4 woodcutters, 2 miners (transfer to player on proximity).
- Rebel intro: 12 archers at 4 positions (destroyed after intro NIS).
- French forts: Crossbow/archer clusters at fort markers; archers garrisoned in all outposts.

### AI

- `AI_Enable(playerStowe, false)` — Stowe villagers are script-controlled, no AI.
- `AI_Enable(playerNeutral, false)` — Neutral player has no AI.
- Rebel and French players have AI enabled (implicit default) with `PlayerUpgrades_Auto` for automatic upgrades.
- Player also has `PlayerUpgrades_Auto` excluding Chemistry and Corned Gunpowder (removed).
- All combat behavior is module-driven through MissionOMatic Defend (hold position) and RovingArmy (attack-move along waypoints with fallbacks) modules.
- French forts have patrol module `FrenchPatrolA` cycling between gate markers with 5 MAA + 5 crossbowmen.
- 5 French camp guard Defend modules with static garrisons (CampGuards1–5).
- French fort static springald modules (`FrenchFortSpringaldA/B`) holding position at fort markers.

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `Objective_StartTimer(OBJ_Reinforce1, COUNT_DOWN, 360)` | 360s | Countdown until William Marshal arrives |
| `Rule_AddOneShot(Reinforce1_TimerComplete, 360)` | 360s | Completes reinforcement objective |
| `Rule_AddOneShot(Lincoln2_ActivateFortA, 350)` | 350s | Activates French Fort A wave spawning |
| `Rule_AddOneShot(Lincoln2_ActivateFortB, 600)` | 600s after Fort A | Activates French Fort B wave spawning |
| `Rule_AddInterval(Lincoln2_CheckRebelWaves, rebelWaveInterval)` | 80–130s | Periodic rebel wave dispatch check |
| `Rule_AddInterval(Lincoln2_CheckFrenchWaveA, frenchWaveInterval)` | 280–600s | Periodic French Fort A wave dispatch |
| `Rule_AddInterval(Lincoln2_CheckFrenchWaveB, frenchWaveInterval+30)` | 310–630s | Periodic French Fort B wave dispatch |
| `Rule_AddInterval(Lincoln2_CheckMissionFail, 1)` | 1s | Checks if keep is destroyed |
| `Rule_AddInterval(Lincoln2_CheckMissionWin, 1)` | 1s | Checks if both primary objectives complete |
| `Rule_AddInterval(Lincoln2_CheckKeep, 1)` | 1s | Monitors keep health for OBJ_DefendKeep trigger |
| `Rule_AddInterval(Lincoln2_CheckRebelBuildingProx, 1)` | 1s | Starts OBJ_DefeatRebels on player proximity |
| `Rule_AddInterval(Lincoln2_CheckFrenchSightTrigger, 1)` | 1s | Enables fort checks when French first spotted |
| `Rule_AddInterval(Lincoln2_CheckStoweTrigger, 1)` | 1s | Transfers Stowe to player on proximity |
| `Rule_AddInterval(Lincoln2_CheckFrenchArrival, 1)` | 1s | CTA when French reach south gate |
| `Rule_AddOneShot(Lincoln2_InitFrenchAttack, 10)` | 10s delay | Initial French attack after 3 rebel buildings down |
| `Rule_AddOneShot(Lincoln2_WilliamMarshalCTA, 0.5)` | 0.5s | Plays arrival CTA for William Marshal |
| `Rule_AddOneShot(Lincoln2_MoveReinforcements1, 4.5)` | 4.5s | Moves cavalry to destinations after spawn |
| `Music_LockIntensity(MUSIC_TENSE, 30)` | 30s | Initial tense music lock at mission start |
| `_g_UpgradesTimer (training)` | 25s | Timeout for keep upgrade training hint |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (modules, waves, objectives, recipe)
- `obj_defeat_french.scar` — local objective file for French defeat
- `obj_defeat_rebels.scar` — local objective file for rebel defeat
- `obj_defend_keep.scar` — local objective file for keep defense
- `obj_reinforcements.scar` — local objective file for reinforcement timer
- `training/campaigntraininggoals.scar` — imported by training file for Training_Goal/Training_GoalSequence/Training_AddGoalSequence utilities

### Shared Globals
- `player1` / `playerRebels` / `playerFrench` / `playerStowe` / `playerNeutral` — 5-player references used across all files
- `t_difficulty` — difficulty table referenced in data (defender counts) and core (wave intervals, unit indices, caps)
- `g_leaderWilliamMarshal` — leader data initialized via `Missionomatic_InitializeLeader`, used for hero spawning and speech
- `OBJ_DefeatRebels`, `OBJ_DefeatFrench`, `OBJ_DefendKeep`, `OBJ_Reinforce1` — objective tables registered in objective files, started/checked in core
- `SOBJ_DestroyFortWest`, `SOBJ_DestroyFortEast` — sub-objectives checked in core's `Lincoln2_OnEntityKilled`
- `rebel_wave_1/2/3`, `french_wave_a/b` + their `_data` tables — wave objects created in data, managed in core
- `eg_fort_a`, `eg_fort_b`, `eg_french_outposts_a/b`, `eg_keep`, `eg_military` — EGroups used across data, core, and objective files
- `fort_init_count_a/b`, `fort_prev_count_a/b`, `fort_destroyed_count_a/b` — fort destruction counters shared between obj_defeat_french PreStart and core's OnEntityKilled
- `buildingHints`, `military_destroyed_count` — rebel building tracking shared between core functions
- `EVENTS.*` — intel event keys (Lincoln2_Intro, Lincoln2_Outro, DefeatFrench_Objective, DefeatRebelsStart, etc.)

### Inter-file Function Calls
- Core calls `DefeatFrench_InitObjectives()`, `DefeatRebels_InitObjectives()`, `DefendKeep_InitObjectives()`, `Reinforcements_InitObjectives()` from respective objective files in `Mission_Preset`
- Core calls `Lincoln2_Data_Init()` from data file in `Mission_SetupVariables`
- `obj_reinforcements` calls `Lincoln2_SpawnReinforcements1()` and `Lincoln2_ActivateFortA()` (both in core) via OneShot rules
- `obj_defeat_rebels.OnComplete` calls `Lincoln2_StartDefeatFrench()` and `Lincoln2_TrackMilitaryBuildings()` (core)
- Core's `Lincoln2_OnEntityKilled` reads/writes objective state from all three objective files
- `FortWestOnWallDown` / `FortEastOnWallDown` (obj_defeat_french) call `Lincoln2_PlayCelebrateAtPosition` (core)

### MissionOMatic Module References
- Defend modules: `RebelDefenders1–3`, `FortDefendersA1–A2`, `FortDefendersB1–B3`, `CampGuards1–5`
- RovingArmy modules: `RebelAttack1–3`, `FrenchAttackA`, `FrenchAttackB`, `FrenchFortSpringaldA/B`, `FrenchPatrolA`
- UnitSpawner: `PlayerStartLeader` (William Marshal)
- Location: `Stowe` (neutral hamlet transferable to player)
