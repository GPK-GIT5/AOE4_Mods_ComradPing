# Mongol Chapter 2: Liegnitz

## OVERVIEW

Mongol Chapter 2 recreates the 1241 Battle of Liegnitz (Mission 5 of The Mongol Horde campaign). The player controls Baidar's Mongol army (player1) against the Polish Army (player2) and a timed Bohemian reinforcement army (player3), plus a neutral environment player (player4). The core loop is a three-zone sweep: defeat Polish defenders across the Field, Ridge, and Valley areas — each composed of multiple RovingArmy modules — before a Bohemian countdown timer expires. If the timer runs out, the Bohemian army spawns and must also be destroyed. A unique Nest of Bees siege unit (Chinese blueprint) is given to the player with a speed buff, and an optional objective tracks gold looted from raiding settlements. The mission uses MissionOMatic with 17 RovingArmy modules, staggered engagement logic, wall-breach audio triggers, and a training hint system for the Nest of Bees.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `mon_chp2_liegnitz.scar` | core | Main mission file: player setup, restrictions, difficulty, recipe with 17 RovingArmy modules, combat engagement logic, intro/outro cinematics |
| `obj_destroypoles.scar` | objectives | All objective definitions (primary, sub-objectives, timer, optional raid), objective progress tracking, Bohemian spawn/attack logic, fail conditions |
| `training_liegnitz.scar` | training | Nest of Bees training hint system: goal sequence for instructing the player to attack with siege units |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_SetupPlayers` | mon_chp2_liegnitz | Configure 4 players, ages, alliances, colors, LOS |
| `Mission_SetupVariables` | mon_chp2_liegnitz | Init objectives, SGroups, EGroups, leader, unit templates |
| `Mission_SetRestrictions` | mon_chp2_liegnitz | Lock economy upgrades, remove trade carts, learn Castle units |
| `Mission_SetDifficulty` | mon_chp2_liegnitz | Set `bohemian_timer` via Util_DifVar |
| `Mission_Preset` | mon_chp2_liegnitz | Spawn Mongol buildings, set resources, apply Nest of Bees speed buff |
| `Mission_Start` | mon_chp2_liegnitz | Find all RovingArmy modules, upgrade towers, start primary objective |
| `GetRecipe` | mon_chp2_liegnitz | Define MissionOMatic recipe: 17 RovingArmy modules, audio, title card |
| `Liegnitz_FirstGroupIsEngaged` | mon_chp2_liegnitz | Trigger field group attack when player spots them (1s interval) |
| `Liegnitz_StaggerAttackerEngagement` | mon_chp2_liegnitz | Sort groups by distance, stagger attack commands 5s apart |
| `Liegnitz_StaggerAttackerEngagement_Delayed` | mon_chp2_liegnitz | Execute delayed RovingArmy_SetTarget per group |
| `Liegnitz_ValleyGroupAggro` | mon_chp2_liegnitz | Trigger valley groups to attack when player spots them |
| `Liegnitz_BreachWallCharge` | mon_chp2_liegnitz | Play charge walla audio on wall segment destruction |
| `Liegnitz_FieldWithdrawCelebrate` | mon_chp2_liegnitz | Handle cleanup when all field modules withdraw |
| `Liegnitz_RidgeWithdrawCelebrate` | mon_chp2_liegnitz | Handle cleanup when all ridge modules withdraw |
| `Liegnitz_ValleyWithdrawCelebrate` | mon_chp2_liegnitz | Handle cleanup when all valley modules withdraw |
| `Liegnitz_RovingWithdrawCelebrate` | mon_chp2_liegnitz | Handle cleanup when roving templars withdraw |
| `Liegnitz_BohemianWithdrawCelebrate` | mon_chp2_liegnitz | Handle cleanup when Bohemian army withdraws |
| `Liegnitz_WithdrawCleanup` | mon_chp2_liegnitz | Generic withdraw handler: remove UI, play celebration/VO |
| `Liegnitz_AssignWallsToEGroups` | mon_chp2_liegnitz | Filter wall entities near village markers into EGroups |
| `Liegnitz_AssignSquadsToControlGroups` | mon_chp2_liegnitz | Debug: assign player units to control groups 1-4 |
| `Liegnitz_IntroMovement` | mon_chp2_liegnitz | Spawn and parade player units for intro cinematic |
| `Liegnitz_SkippedIntro` | mon_chp2_liegnitz | Respawn units at final positions if intro skipped |
| `Liegnitz_OutroMovement` | mon_chp2_liegnitz | Spawn parade units, set buildings on fire for outro |
| `Outro_ScoutMove` | mon_chp2_liegnitz | Move scout to outro target after 20s delay |
| `DestroyPoles_InitObjectives` | obj_destroypoles | Register all OBJ/SOBJ constants and objective definitions |
| `DestroyPoles_CheckPlayerStatus` | obj_destroypoles | Fail condition: no units, no production, no resources |
| `DestroyPoles_UpdateObjectiveProgress` | obj_destroypoles | Calculate and display progress bar from module casualties |
| `DestroyPoles_CanPlayerSeeSGroups` | obj_destroypoles | Start sub-objective when player first sees enemy group |
| `DestroyPoles_UpdateObjectiveCounter` | obj_destroypoles | Update counter UI from module kill counts |
| `DestroyPoles_UpdateHintpoints` | obj_destroypoles | Remove hintpoints for withdrawn/dissolved modules |
| `DestroyPoles_StartKnightsOBJ` | obj_destroypoles | Start SOBJ_RovingKnights sub-objective |
| `DestroyPoles_BohemiaAttack` | obj_destroypoles | Spawn Bohemian army and assign to roving_bohemians module |
| `DestroyPoles_DelayStartBohemianArmyUI` | obj_destroypoles | Create threat arrow for Bohemian army after 1s delay |
| `DestroyPoles_BohemiaWarningTimer` | obj_destroypoles | Play Bohemian warning VO at timer midpoint |
| `DestroyPoles_OnSquadKilled` | obj_destroypoles | Track last killed enemy position (GE_SquadKilled) |
| `DestroyPoles_BurnFieldsReminder` | obj_destroypoles | Start OBJ_RaidSettlements after 8s delay |
| `DestroyPoles_FarmAttacked` | obj_destroypoles | Detect burning Polish buildings, play VO (1s interval) |
| `DestroyPoles_BeesReminder` | obj_destroypoles | Play Nest of Bees VO when player selects them (0.5s) |
| `DestroyPoles_BeesAttackCheck` | obj_destroypoles | Flag Nest of Bees confirmed kill on military target |
| `DestroyPoles_FindHiddenStables` | obj_destroypoles | Retarget all enemy modules toward moved player stables |
| `Liegnitz_InitializeBeesTrainingHints` | training_liegnitz | Set up Nest of Bees training goal sequence |
| `Liegnitz_BeesAreAlive` | training_liegnitz | Predicate: Nest of Bees units exist |
| `Liegnitz_IgnoreBeesDead` | training_liegnitz | Ignore predicate: timeout or Bees group empty |
| `Liegnitz_SkipBeesTip` | training_liegnitz | Skip if Bees already damaged an enemy |
| `Liegnitz_BeesComplete` | training_liegnitz | Complete when Bees have engaged the enemy |
| `Liegnitz_DamageCheck` | training_liegnitz | GE_DamageReceived: confirm Bees attacked non-player entity |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DestroyPolishArmy` | Primary (Battle) | Destroy all Polish army groups across field, ridge, valley, and templars |
| `SOBJ_DefeatRemainingField` | Sub-objective (Battle) | Defeat field area defenders (4 modules) |
| `SOBJ_DefeatRemainingRidge` | Sub-objective (Battle) | Defeat ridge area defenders (4 modules) |
| `SOBJ_DefeatRemainingValley` | Sub-objective (Battle) | Defeat valley area defenders (6 modules) |
| `SOBJ_DefeatRemainingPatrol` | Sub-objective (Battle) | Defeat roving templar knights (1 module) |
| `SOBJ_RovingKnights` | Sub-objective (Battle) | Defeat the Elite Knights specifically |
| `OBJ_BohemianTimer` | Information | Countdown timer until Bohemian reinforcements arrive |
| `OBJ_DestroyBohemianArmy` | Primary (Battle) | Destroy Bohemian army (activates on timer expiry) |
| `OBJ_RaidSettlements` | Optional | Loot 2000 gold from raiding Polish settlements |
| `OBJ_ArmySurvive` | Information | Player army must not be fully destroyed (registered but commented out) |
| `OBJ_DebugComplete` | Debug | Instantly complete mission |

### Difficulty

| Parameter | Easy | Normal | Hard | Hardest |
|-----------|------|--------|------|---------|
| `bohemian_timer` | 1440s (24m) | 1320s (22m) | 1200s (20m) | 1140s (19m) |
| `player_resources.food` | 1000 | 800 | 600 | 400 |
| `player_resources.wood` | 1000 | 800 | 600 | 400 |
| `player_resources.gold` | 1000 | 800 | 600 | 400 |
| `player_resources.stone` | 500 | 400 | 300 | 200 |
| Nest of Bees count | 5 | 4 | 3 | 2 |
| Field cavalry (horsemen) | 7 | 8 | 10 | 12 |
| Field cavalry (knights) | 1 | 2 | 3 | 4 |
| Field center archers | 8 | 10 | 14 | 18 |
| Field center spearmen | 3 | 4 | 6 | 8 |
| Field patrol spearmen | 6 | 7 | 10 | 14 |
| Field patrol archers | 4 | 5 | 7 | 10 |
| Ridge left horsemen | 8 | 9 | 13 | 18 |
| Ridge left knights | 2 | 3 | 4 | 5 |
| Ridge right spearmen | 7 | 8 | 12 | 16 |
| Ridge center archers | 7 | 8 | 12 | 18 |
| Ridge center spearmen | 8 | 10 | 12 | 14 |
| Ridge patrol spearmen | 5 | 7 | 10 | 14 |
| Ridge patrol archers | 4 | 5 | 7 | 10 |
| Valley front landsknechts | 6 | 7 | 10 | 14 |
| Valley center archers | 11 | 13 | 19 | 26 |
| Valley back knights (T4) | 7 | 8 | 12 | 16 |
| Valley left/right spearmen | 7 | 8 | 12 | 16 |
| Valley patrol spearmen | 6 | 7 | 10 | 14 |
| Valley patrol archers | 3 | 4 | 6 | 8 |
| Roving templars (T4 knights) | 12 | 14 | 20 | 28 |
| Bohemian knights | 6 | 7 | 10 | 14 |
| Bohemian horsemen | 6 | 7 | 10 | 14 |
| Bohemian archers | 6 | 7 | 10 | 14 |
| Bohemian men-at-arms | 6 | 7 | 10 | 14 |

### Spawns

**Player Army (Intro):**
- 18 Horseman T3 (3 groups of 6, paraded in from intro markers)
- 12 Horse Archer T3 (2 groups of 6, paraded in)
- 2 Scouts, 1 Baidar (leader/Khan), 2-5 Nest of Bees (difficulty-scaled)
- 3 Stables, 1 Ovoo, 1 Arsenal, 1 Blacksmith, 1 Market, 4 Gers, 1 Kurultai spawned at preset markers

**Polish Army (player2) — 15 RovingArmy modules across 3 zones:**
- **Field (4 modules):** Left/Right cavalry, center archers+spearmen, patrol infantry. Withdraw at 20-30%, fallback to village markers.
- **Ridge (4 modules):** Left cavalry, right spearmen, center archers+spearmen, patrol infantry. Withdraw at 20-30%.
- **Valley (6 modules):** Front landsknechts, center archers, back T4 knights, left/right spearmen, patrol infantry. Withdraw at 20-40%.
- **Templars (1 module):** T4 knights cycling through 14 patrol markers. Withdraw at 30%.
- All Polish modules use `ARMY_TARGETING_REVERSE` (defenders) or `ARMY_TARGETING_CYCLE` (patrols), with `onDeathDissolve = true`.

**Bohemian Army (player3) — 1 RovingArmy module:**
- Spawned only on timer failure via `DestroyPoles_BohemiaAttack()` at `mkr_bohemia_start`
- Knights, horsemen, archers, men-at-arms (all T3 HRE). Withdraw at 40%.

### AI

- No `AI_Enable` calls — enemies are entirely RovingArmy module-driven, not standard AI.
- **Staggered engagement:** When the player first sees field or valley groups, `Liegnitz_StaggerAttackerEngagement` sorts groups by distance and issues `RovingArmy_SetTarget` commands 5 seconds apart, creating a wave effect.
- **Reactive retargeting:** `DestroyPoles_FindHiddenStables` (5s interval) detects if the player moves their production buildings and retargets all 17 enemy modules toward the new stable position.
- **Bohemian activation:** On timer failure, all surviving Polish modules get `mkr_bohemia_6` added to their target lists, and Bohemians cycle through 6 bohemia markers.
- **Tower upgrades:** All player2 towers are instantly upgraded with springald emplacements at mission start.
- Polish towers get `UPGRADE_TOWER_SPRINGALD` applied via `Cmd_InstantUpgrade`.

### Timers

| Timer | Type | Delay | Purpose |
|-------|------|-------|---------|
| `Liegnitz_FirstGroupIsEngaged` | `Rule_AddInterval` | 1s | Poll if player can see field groups, then trigger stagger attack |
| `Liegnitz_ValleyGroupAggro` | `Rule_AddInterval` | 1s | Poll if player can see valley groups, then trigger stagger attack |
| `Liegnitz_BreachWallCharge` | `Rule_AddGlobalEvent` | GE_EntityKilled | Play charge walla when wall segments destroyed |
| `DestroyPoles_BurnFieldsReminder` | `Rule_AddOneShot` | 8s | Start OBJ_RaidSettlements |
| `DestroyPoles_FarmAttacked` | `Rule_AddInterval` | 1s | Check for burning buildings, play VO |
| `DestroyPoles_BeesReminder` | `Rule_AddInterval` | 0.5s | Play VO when Nest of Bees selected |
| `DestroyPoles_BeesAttackCheck` | `Rule_AddGlobalEvent` | GE_DamageReceived | Track Nest of Bees combat usage |
| `DestroyPoles_CanPlayerSeeSGroups` | `Rule_AddInterval` | 1s | Start sub-objectives when enemy groups are spotted (×4 instances) |
| `DestroyPoles_BohemiaWarningTimer` | `Rule_AddOneShot` | timer/2 | Play Bohemian approach warning VO at halfway |
| `OBJ_BohemianTimer` countdown | `Objective_StartTimer` | difficulty-based | 19-24 minute countdown with 60s warning |
| `Liegnitz_InitializeBeesTrainingHints` | `Rule_AddOneShot` | 17s | Initialize Nest of Bees training tips (after VO) |
| `DestroyPoles_FindHiddenStables` | `Rule_AddInterval` | 5s | Retarget enemies if player moves stables |
| `DestroyPoles_DelayStartBohemianArmyUI` | `Rule_AddOneShot` | 1s | Create threat arrow for Bohemian army |
| `Outro_ScoutMove` | `Rule_AddOneShot` | 20s | Move scout during outro cinematic |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core mission framework (RovingArmy, MissionOMatic_FindModule, objective system)
- `obj_destroypoles.scar` — Objective definitions (imported by core via function call pattern)
- `training_liegnitz.scar` — Imported via `import("training_liegnitz.scar")`
- `training/campaigntraininggoals.scar` — Base training framework (imported by training_liegnitz)

### Shared Globals
- `player1`–`player4` — Player handles used across all files
- `sg_rocketsiege` — Nest of Bees SGroup, referenced in core, objectives, and training
- `sg_player_units`, `sg_group_01`, `sg_scout_01/02` — Player unit groups shared across files
- `sg_bohemian_units`, `sg_polish_units` — Enemy unit SGroups
- `eg_player_production_structures` — Player buildings EGroup, used for fail checks and retargeting
- `b_BeesHaveKilledBeforeAndWillDoItAgain` — Flag set in objectives, read in training to skip tips
- `b_BeesHaveEngagedTheEnemy` — Flag set in training, read by training goal completion check
- `last_killed_position` — Tracked in objectives for enemy death position
- `t_difficulty` — Difficulty table set in core, read in objectives for timer values
- `field_cavalry` — Unit composition table defined in core, used in recipe modules
- `defeated_groups` — Counter tracking how many Polish groups have been fully routed
- `stable_position` — Tracks player stable location for enemy retargeting
- `polish_modules`, `bohemian_modules` — Module reference arrays built in `Mission_Start`, used in objectives
- All RovingArmy module handles (`field_defend_left`, `ridge_patrol`, `roving_templars`, etc.) — Set in core, referenced in objectives

### Inter-File Function Calls
- `mon_chp2_liegnitz.scar` calls `DestroyPoles_InitObjectives()` (from obj_destroypoles) during `Mission_SetupVariables`
- `obj_destroypoles.scar` calls `Liegnitz_InitializeBeesTrainingHints()` (from training_liegnitz) via `Rule_AddOneShot` after Bees VO
- `obj_destroypoles.scar` references `EVENTS.*` constants (Intro, Victory, Polish_Cavalry_Defeated, etc.) defined in MissionOMatic data
- `obj_destroypoles.scar` calls `RovingArmy_SetTarget/SetTargets`, `SpawnUnitsToModule`, `ThreatArrow_CreateGroup` from MissionOMatic framework
- `obj_destroypoles.scar` calls `Mission_Complete()` and `Mission_Fail()` from MissionOMatic
- `training_liegnitz.scar` calls `Training_Goal`, `Training_GoalSequence`, `Training_AddGoalSequence`, `Training_EnableGoalSequenceByID` from campaigntraininggoals framework

### Notable Design Patterns
- **Withdraw-and-celebrate:** Every RovingArmy module has an `onWithdrawFunction` that calls `Liegnitz_WithdrawCleanup`, a generic handler that removes UI, plays celebration audio, and triggers VO events on group defeat milestones.
- **Progressive visibility:** Sub-objectives only start when the player first spots the corresponding enemy group via `DestroyPoles_CanPlayerSeeSGroups`.
- **Nest of Bees (Chinese unit on Mongol player):** A Chinese siege blueprint `UNIT_NEST_OF_BEES_4_CHI` is given to the Mongol player with a 1.4× speed modifier, reflecting the historical use of Chinese gunpowder technology.
- **Dynamic retargeting:** If the player moves their stables (Mongol buildings are mobile), all enemy modules retarget toward the new position.
