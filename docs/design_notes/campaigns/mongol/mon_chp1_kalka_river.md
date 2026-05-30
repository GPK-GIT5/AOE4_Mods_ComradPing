# Mongol Chapter 1: Kalka River

## OVERVIEW

**mon_chp1_kalka_river** is the first Mongol campaign mission, set at the Battle of the Kalka River (1223). The player controls General Subutai's Mongol cavalry force and must set up an ambush for the advancing Rus army, then lure them into it and destroy them. The mission flows through distinct phases: position units at three ambush points (western ford, eastern ford, central woods) before a countdown timer expires → engage and lure the Rus across the river → spring the ambush to eliminate the main Rus force → assault the enclosed Rus defenders at their cart stockade. Three players are configured: Mongols (player1, General Subutai), Rus enemy (player2, Mstislav), and a neutral Mongol ally holder (player3) for the leader unit. All players are locked to Feudal Age. Difficulty scales Rus army sizes, player knight/horseman composition, reinforcement thresholds, merge thresholds, and the ambush setup timer across 4 levels via `Util_DifVar`.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp1_kalka_river.scar | core | Main mission orchestrator: player setup, variables, difficulty params, recipe with all RovingArmy/UnitSpawner/Defend modules, intro scout ambush, unit movement, parade system, upgrades, achievement tracking, outro cinematics |
| obj_setupambush.scar | objectives | Ambush setup phase: countdown timer (OBJ_RusTimer), three position sub-objectives requiring 15 units each at marked locations |
| obj_slowdowntherus.scar | objectives | Lure phase: parent "Destroy the Rus" objective, meet/engage the Rus, lead them to ambush point, spawn 3 staggered Rus army waves, early-kill detection |
| obj_ambushattack.scar | objectives | Ambush combat phase: eliminate all incoming Rus at ambush point with progress bar, reinforcement balancing, army merge logic, late retreat spawns |
| obj_defeat_enclosedrus.scar | objectives | Final phase: defeat enclosed Rus defenders at cart stockade, progress tracking via GE_SquadKilled, wall construction, victory/achievement triggers |
| obj_gettoambushpoint.scar | objectives | Legacy/unused objective stub for leading Rus to ambush point (functionality moved to obj_slowdowntherus) |
| training_kalkariver.scar | training | Tutorial goal sequences for control groups (KBM + Xbox), Khan signal arrow ability (KBM + Xbox), and Mangudai move-and-shoot mechanic |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | mon_chp1_kalka_river.scar | Configures 3 players, ages, alliances, names |
| Mission_SetupVariables | mon_chp1_kalka_river.scar | Creates all SGroups, difficulty vars, leader init |
| Mission_SetRestrictions | mon_chp1_kalka_river.scar | Enables auto-upgrades, unlocks cavalry upgrades |
| Mission_Preset | mon_chp1_kalka_river.scar | Sets colours, inits objectives, modifies Subutai abilities |
| Mission_Start | mon_chp1_kalka_river.scar | Zeroes resources, starts ambush setup objective |
| GetRecipe | mon_chp1_kalka_river.scar | Defines MissionOMatic recipe with all modules |
| Kalka_MoveStartingUnits | mon_chp1_kalka_river.scar | Formation-moves all starting units to initial positions |
| Monitor_scoutsForAmbush | mon_chp1_kalka_river.scar | Triggers intro scout ambush on proximity |
| MonitorScoutDeath | mon_chp1_kalka_river.scar | Repositions units after intro scouts eliminated |
| Kalka_UnlockCavalryUpgrades | mon_chp1_kalka_river.scar | Completes melee/ranged/cavalry upgrades for player |
| ParadeArmy | mon_chp1_kalka_river.scar | Manages Rus knight parade with phase rotation |
| TriggerCheeringNearKnight | mon_chp1_kalka_river.scar | Triggers walla cheering on nearby Rus groups |
| CheckUnitsLeftKalka | mon_chp1_kalka_river.scar | Fails mission if all player squads dead |
| Achievement_OnSquadKilled | mon_chp1_kalka_river.scar | Tracks horse archer deaths for Twinkle Hooves |
| Mongol_prepare_outro | mon_chp1_kalka_river.scar | Clears map, spawns outro units and corpse field |
| Mongol_StartOutroMovement | mon_chp1_kalka_river.scar | Moves outro units along spline paths |
| SetupTheRusAmbush_InitObjectives | obj_setupambush.scar | Registers ambush setup + timer + 3 position objectives |
| setup_Ambush_Start | obj_setupambush.scar | Hooks Khan ability event, unlocks music |
| RusArrivalTimer_Monitor | obj_setupambush.scar | Completes timer obj when countdown reaches zero |
| GetSquadProgressA_Monitor | obj_setupambush.scar | Tracks unit count at western ford position |
| GetSquadProgressB_Monitor | obj_setupambush.scar | Tracks unit count at eastern ford position |
| GetSquadProgressC_Monitor | obj_setupambush.scar | Tracks unit count at central woods position |
| SetupTheRusAmbush_OnComplete | obj_setupambush.scar | Starts parent "Destroy the Rus" objective |
| LureTheRusToAmbush_InitObjectives | obj_slowdowntherus.scar | Registers destroy/meet/lure objectives |
| ReDestroyTheRus_start | obj_slowdowntherus.scar | Starts MeetTheRus sub-objective, move-shoot tutorial |
| MeetTheRus_Start | obj_slowdowntherus.scar | Spawns 3 staggered Rus army waves into roving modules |
| SpawnUnitsRus02 | obj_slowdowntherus.scar | Spawns second Rus wave (spearmen ×4 groups) |
| SpawnUnitsRus03 | obj_slowdowntherus.scar | Spawns third Rus wave (archers ×4 groups) |
| MeetTheRusMonitor | obj_slowdowntherus.scar | Detects player contact with any Rus army group |
| MeetTheRus_OnComplete | obj_slowdowntherus.scar | Starts lure-to-ambush sub-objective |
| GetRusToAmbushPt_Start | obj_slowdowntherus.scar | Monitors Rus reaching ambush area |
| CheckifAllRusKilledEarlyMonitor | obj_slowdowntherus.scar | Detects early kill of Rus before ambush point |
| GetRusToAmbush_Failed | obj_slowdowntherus.scar | Handles ambush failure, skips to direct combat |
| GetToAmbushPointMonitor | obj_slowdowntherus.scar | Completes lure objective when Rus reach ambush |
| Kalka_ModifyRusSpeed | obj_slowdowntherus.scar | Applies speed modifier to all Rus units |
| DefeatRusUltimate_OnComplete | obj_slowdowntherus.scar | Locks music, calls Mission_Complete |
| AmbushAttack_InitObjectives | obj_ambushattack.scar | Registers ambush battle sub-objective |
| KillAllRusAmbushPt_Start | obj_ambushattack.scar | Inits army count, starts monitoring, locks combat music |
| Kalka_InitRusArmyCount | obj_ambushattack.scar | Counts all Rus attack groups for progress bar |
| KillAllRusAmbushPt_Monitor | obj_ambushattack.scar | Tracks kills, merges armies, completes on elimination |
| Kalka_CheckAllReinforcements | obj_ambushattack.scar | Checks all attack modules for reinforcement needs |
| Kalka_CheckReinforcements | obj_ambushattack.scar | Transfers 6-9 units from support to depleted module |
| spawnLateUnits_toRetreat | obj_ambushattack.scar | Spawns late spearmen/archers at stockade after 30s |
| make_units_retreat | obj_ambushattack.scar | Retreats surviving Rus to stockade defend module |
| DefeatEnclosedRus_InitObjectives | obj_defeat_enclosedrus.scar | Registers enclosed Rus battle objective + debug |
| KillAllEnclosedRus_Start | obj_defeat_enclosedrus.scar | Spawns 3 defender groups at stockade positions |
| EnemyKilledStockadeDefEvent | obj_defeat_enclosedrus.scar | Increments kill counter on tagged "RusEnclosed" deaths |
| KillAllEnclosedRus_Monitor | obj_defeat_enclosedrus.scar | Completes objective when all enclosed Rus dead |
| KillAllEnclosedRus_OnComplete | obj_defeat_enclosedrus.scar | Fires Twinkle Hooves achievement, completes parent obj |
| CheckMongolApproaching | obj_defeat_enclosedrus.scar | Plays stinger when player approaches stockade |
| Tutorials_Kalka_ControlGroups | training_kalkariver.scar | Control group tutorial (CTRL+0-9 / LT+RT) |
| Tutorials_Kalka_KhanAbility | training_kalkariver.scar | Khan ability tutorial for KBM |
| Tutorials_Kalka_KhanAbility_Xbox | training_kalkariver.scar | Khan ability tutorial for Xbox controller |
| HasIdleKhanOnScreen | training_kalkariver.scar | Trigger: detects idle Khan visible on screen |
| Tutorials_kalkariver_MoveShoot | training_kalkariver.scar | Move-and-shoot tutorial for Mangudai |
| Predicate_setKeyMoveShoot | training_kalkariver.scar | Trigger: checks horse archers near move-shoot markers |
| kalka_OnAbilityExecutedRightTime | training_kalkariver.scar | Tracks maneuver arrow ability usage for tutorial |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_SetupTheRusAmbush | Primary | Prepare army at 3 ambush positions before timer expires |
| OBJ_RusTimer | Information | Countdown timer for Rus arrival (difficulty-scaled) |
| SOBJ_GetSquadToPositionA | Sub (of Setup) | Move 15 units to western ford |
| SOBJ_GetSquadToPositionB | Sub (of Setup) | Move 15 units to eastern ford |
| SOBJ_GetSquadToPositionC | Sub (of Setup) | Move 15 units to central woods |
| OBJ_DestroyTheRusUltimate | Primary | Parent: destroy the entire Rus army |
| SOBJ_MeetTheRus | Sub (of Destroy) | Lure Rus cavalry across the river |
| SOBJ_GetRusToAmbushPt | Sub (of Destroy) | Lead Rus army to the ambush point |
| SOBJ_KillAllRusAmbushPt | Sub/Battle (of Destroy) | Eliminate all incoming Rus at ambush |
| SOBJ_KillAllEnclosedRus | Sub/Battle (of Destroy) | Defeat enclosed Rus at cart stockade |
| OBJ_DebugComplete | Debug | Instant-win cheat objective |

### Difficulty

All values ordered `{Easy, Normal, Hard, Hardest}`:

| Parameter | Values | What It Scales |
|-----------|--------|----------------|
| rusReinforceThreshold | {18, 20, 22, 26} | Unit count below which attack groups receive reinforcements |
| rusMergeThreshold | {70, 100, 130, 160} | Total Rus below which remaining armies merge together |
| earlyKillThreshold | {130, 160, 190, 220} | Enemy count below which lure objective auto-fails (killed too fast) |
| i_Troops01Player2 | {24, 24, 26, 30} | First Rus wave spearmen per sub-group (×3 groups) |
| i_Troops02Player2 | {24, 24, 26, 30} | Second Rus wave spearmen per sub-group (×4 groups) |
| i_Troops03Player2 | {32, 32, 36, 40} | Third Rus wave archers per sub-group (×4 groups) |
| i_TroopsPlayer2Enclosed | {20, 20, 25, 27} | Enclosed Rus per defend group (×3 = total) |
| i_Knights01Player1 | {28, 10, 0, 0} | Player's western ambush knights (replaced by horsemen on Hard+) |
| i_Knights02Player1 | {28, 28, 28, 28} | Player's central ambush knights (constant) |
| i_Knights03Player1 | {28, 10, 0, 0} | Player's eastern ambush knights (replaced by horsemen on Hard+) |
| i_Horsemen01Player1 | {0, 18, 28, 28} | Player's western ambush horsemen (inverse of knights) |
| i_Horsemen03Player1 | {0, 18, 28, 28} | Player's eastern ambush horsemen (inverse of knights) |
| i_HorseArchersPlayer1 | {36, 36, 36, 36} | Player's Mangudai horse archers (constant) |
| OBJ_RusTimer | {70, 60, 50, 50} | Seconds before Rus army arrives (setup phase timer) |

On higher difficulties, the player receives weaker horsemen instead of knights in flanking positions, while facing larger Rus armies. The setup timer is also reduced.

### Spawns

**Player Forces (Mongols):**
- `mongol_bait`: 36 horse archers at player start (all difficulties)
- `ambush_spawn_2`: Knights (28→0) + Horsemen (0→28) at right flank, difficulty-scaled
- `ambush_spawn_3`: 28 knights at central position (all difficulties)
- `ambush_spawn_4`: Knights (28→0) + Horsemen (0→28) at left flank, difficulty-scaled
- `ambush_spawn_introcam` / `introcam02`: 10+10 intro knights for scout ambush cinematic
- `PlayerStartLeader`: Subutai (unit_subutai_3_cmp_mon) as hero leader

**Rus Forces (Enemy):**
- `Intro_RusScouts`: 4 scouts + 15 horsemen, initial roving force
- First wave (MeetTheRus_Start): 1 knight + 4 scouts + spearmen (24-30 ×3 groups) in RovingArmy modules
- Second wave (SpawnUnitsRus02, 5s delay): Spearmen (24-30 ×4 groups)
- Third wave (SpawnUnitsRus03, 8s total delay): Archers (32-40 ×4 groups)
- Late retreat spawn (30s into ambush): 10 spearmen + 5 archers at stockade
- Enclosed defenders: Spearmen + archers (20-27 ×3 groups) at cart stockade

**RovingArmy Attack Modules:**
- 3 center attack groups (`rus_attack`, `_a`, `_b`) → target ambush point
- 4 left attack groups (`rus_attack02`, `_a`, `_b`, `_c`) → target river crossing
- 4 right attack groups (`rus_attack03`, `_a`, `_b`, `_c`) → target archer positions
- All have withdrawThreshold 0.15-0.2, combatRange/leashRange 35-50, fallback to cart stockade
- Support module system: depleted groups pull 6-9 units from paired support groups

### AI

- No `AI_Enable` calls; all enemy behavior is RovingArmy module-driven
- **Patrol system**: Two scout groups cycle through 10 waypoints each (ARMY_TARGETING_CYCLE) searching for player units near ambush area
- **Knight parade**: Rus knights march between display waypoints, triggering cheering walla on nearby armies; phases rotate randomly between "phase1" and "phase2" routes
- **Army merge logic**: When total Rus count drops below `rusMergeThreshold`, center and right attack groups dissolve into left groups via `DissolveModuleIntoModule`
- **Reinforcement balancing**: `Kalka_CheckReinforcements` monitors each attack module; when a module drops to 10-threshold units and its support module has 15+, it transfers 6-9 units
- **Module dissolution on lure**: When Rus reach ambush point, all roving/patrol modules dissolve into attack modules via 18 `DissolveModuleIntoModule` calls
- **Defend modules**: 3 defend modules at cart stockade (combatRange 20, leashRange 45) for enclosed phase
- **Retreat behavior**: Late-spawned units retreat to stockade and dissolve into defend module
- **Rus speed**: Initially slowed to 0.8× on spawn, boosted to 1.25× during ambush combat

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `Rule_AddOneShot(Tutorials_Start_ControlGroup, 8)` | 8s after preset | Starts control group tutorial |
| `Rule_AddInterval(CheckUnitsLeftKalka, 2)` | Every 2s | Checks for total player unit loss → mission fail |
| `Rule_AddOneShot(StartKhanAbilityTuto, 1)` | 1s after MeetTheRus | Starts Khan ability tutorial |
| `Rule_AddOneShot(SpawnUnitsRus02, 5)` | 5s after first wave | Spawns second Rus wave |
| `Rule_AddOneShot(SpawnUnitsRus03, 3)` | 3s after second wave | Spawns third Rus wave |
| `Rule_AddInterval(MeetTheRusMonitor, 1)` | Every 1s | Checks player proximity to any Rus group |
| `Rule_AddInterval(CheckifAllRusKilledEarlyMonitor, 5)` | Every 5s | Detects if Rus killed before reaching ambush |
| `Rule_AddOneShot(spawnLateUnits_toRetreat, 30)` | 30s into ambush battle | Spawns late reinforcements at stockade |
| `Rule_AddInterval(KillAllRusAmbushPt_Monitor, 1)` | Every 1s | Tracks ambush kill progress |
| `Rule_AddInterval(Kalka_CheckAllReinforcements, 3)` | Every 3s | Checks reinforcement transfers between modules |
| `OBJ_RusTimer countdown` | {70, 60, 50, 50}s | Timer before Rus army arrives during setup phase |
| `Rule_AddOneShot(Kalka_DelayedInteractivityChange, 25)` | 25s after timer expires | Changes world interaction stage |
| `Rule_AddOneShot(Start_Tutorial_MoveShoot, 3)` | 3s after Destroy phase | Starts Mangudai move-shoot tutorial |
| `Music_LockIntensity(MUSIC_COMBAT_RARE, 30)` | 30s lock | Combat music intensity during ambush |
| `Rule_AddOneShot(intro_setvulnerable, 3)` | 3s after scouts found | Makes intro Rus scouts vulnerable (health set to 10%) |
| `Rule_AddOneShot(MoveSubutaiAcrossRiver, 1.5)` | 1.5s after scouts dead | Moves Subutai to ambush location |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core mission framework (includes Cardinal scripts)
- `obj_slowdowntherus.scar` — Lure/destroy Rus objectives
- `obj_setupambush.scar` — Ambush setup phase objectives
- `obj_ambushattack.scar` — Ambush battle objective
- `obj_defeat_enclosedrus.scar` — Enclosed Rus final objective
- `training_kalkariver.scar` — Tutorial sequences
- `training/campaigntraininggoals.scar` — Shared campaign training goal framework
- `training/coretrainingconditions.scar` — Core training predicates
- `training/mongoltrainingconditions.scar` — Mongol-specific training predicates

### Shared Globals
- `player1`, `player2`, `player3` — Player handles used across all files
- `g_leaderSubutai` — Leader struct initialized via `Missionomatic_InitializeLeader`, referenced in multiple files
- `sg_mon_horsearchers`, `sg_ambush_group_2/3/4` — Player army SGroups shared across objectives
- `sg_rus_army_*_attack*` — Rus attack SGroups referenced by ambush monitoring and reinforcement logic
- `sg_rus_global` — Aggregate Rus SGroup for early-kill detection
- `sg_first_army`, `sg_second_army`, `sg_third_army` — Staggered Rus wave SGroups
- `sg_first_army_knight`, `sg_first_army_scout` — Rus cavalry SGroups for meet detection
- `rusInitArmyCount`, `rusHaveMerged`, `rusKilledPrev` — Ambush battle state tracking
- `i_deathRusEnclosed`, `i_amountOfEnclosedRus` — Stockade kill progress
- `horseArchersKilled` — Achievement tracking flag (Twinkle Hooves - Achievement #17)
- `b_used_khan_ability`, `b_used_khan_abilityRightTime` — Khan ability tutorial state
- `g_ambushFailed` — Flag set when lure objective fails, affects victory VO selection
- `RusKilledEarly` — Flag for early Rus elimination path

### Inter-File Function Calls
- Core → `SetupTheRusAmbush_InitObjectives()`, `LureTheRusToAmbush_InitObjectives()`, `AmbushAttack_InitObjectives()`, `DefeatEnclosedRus_InitObjectives()` — Objective registration from core
- Core → `Tutorials_Kalka_ControlGroups()`, `Tutorials_Kalka_KhanAbility()`, `Tutorials_Kalka_KhanAbility_Xbox()`, `Tutorials_kalkariver_MoveShoot()` — Tutorial activation from core
- obj_setupambush → `OBJ_DestroyTheRusUltimate` — Starts parent destroy objective on ambush setup complete
- obj_slowdowntherus → `SOBJ_KillAllRusAmbushPt`, `SOBJ_KillAllEnclosedRus` — Starts next sub-objective on completion
- obj_ambushattack → `CheckMongolApproaching()` — Starts stockade proximity check after ambush complete
- obj_ambushattack → `ObjectiveStartNextObj_Enclosed()` → `SOBJ_KillAllEnclosedRus` — Chains to enclosed phase
- obj_defeat_enclosedrus → `DefeatRusUltimate_OnComplete()` → `Mission_Complete()` — Final victory chain
- Training → `kalka_OnAbilityExecutedRightTime` — Global event handler registered from training, state used in core

### MissionOMatic Modules
- **UnitSpawner**: `Intro_RusScouts`, `mongol_bait`, `ambush_spawn_2/3/4`, `ambush_spawn_introcam`, `PlayerStartLeader`
- **RovingArmy**: 20+ modules for Rus roving/patrol/attack formations with dissolution chains
- **Defend**: `stockade_defend`, `stockade_defend02`, `stockade_defend_archers` at cart stockade

### Blueprint References
- `SBP.MONGOL.UNIT_SUBUTAI_3_CMP_MON` — Subutai hero unit
- `SBP.RUS.UNIT_SCOUT_1_RUS`, `UNIT_HORSEMAN_2_RUS`, `UNIT_SPEARMAN_1/2_RUS`, `UNIT_VILLAGER_1_RUS` — Rus unit blueprints
- `SBP.MONGOL.UNIT_KNIGHT_2_MON` — Mongol knight blueprint
- `khan_attack_speed_signal_arrow_mon`, `khan_maneuver_signal_arrow_mon`, `khan_defensive_signal_arrow_mon` — Khan ability blueprints
- `UPG.MONGOL.UPGRADE_MELEE_ARMOR_I_IMPROVED_MON`, `UPGRADE_MELEE_DAMAGE_I_IMPROVED_MON`, `UPGRADE_RANGED_ARMOR_I_IMPROVED_MON`, `UPGRADE_RANGED_DAMAGE_I_IMPROVED_MON`, `UPGRADE_RANGED_BODKIN_MON`, `UPGRADE_RANGED_ARCHER_QUIVVER_MON`, `UPGRADE_CAVALRY_GRAPERED_LANCE_MON` — Pre-completed cavalry upgrades
- `CE_ACHIEVHORSEARCHERSSURVIVE` — Custom challenge event for Twinkle Hooves achievement
