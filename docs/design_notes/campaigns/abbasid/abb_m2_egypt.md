# Abbasid Mission 2: Egypt

## OVERVIEW

Abbasid Mission 2 is a tug-of-war control point battle set in the Nile Delta (1160s). The player (Damascenes/Ayyubids) competes against Crusader Franks for dominance over ~9 strategic points scattered across the map. A persistent `control_balance` meter (starting at 0.3, victory at 1.0, failure at ≤0) shifts based on which side holds more points, with an accelerating ramp over time. The AI uses a custom heatmap/quadrant system to evaluate targets and distribute armies dynamically. Both sides receive periodic 90-second reinforcement waves that scale in size, and the enemy spawns typed attack groups on a shrinking interval, with Templar elite units introduced after 5 minutes.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m2_egypt.scar` | core | Main mission file: player setup (7 players), relationships, restrictions, mission lifecycle, recipe |
| `abb_m2_egypt_objectives.scar` | objectives | Defines all objectives (OBJ_ControlPrimary, OBJ_Control tug-of-war, OBJ_Alexandria fail-state, OBJ_Reinforcements timer, tip) |
| `abb_m2_egypt_data.scar` | data | Difficulty tables (Util_DifVar), global data init, quadrant/army variable setup, enemy squad type rotation |
| `abb_m2_egypt_armycontrol.scar` | spawns | Enemy army creation, reinforcement wave sizing, typed squad spawning, army lifecycle management |
| `abb_m2_egypt_controlpoints.scar` | spawns/other | Control point init, ownership monitoring, village layout save/rebuild, garrison spawn/management, villager life |
| `abb_m2_egypt_quadrants.scar` | AI | Quadrant/heatmap targeting system: heat evaluation, best-target selection, occupancy slot management |
| `abb_m2_egypt_automated.scar` | automated | Automated testing: checkpoint registration, AI takeover, attack/defend logic for QA validation |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Distribute_Enemy_Army` | armycontrol | Assigns enemy sgroup to quadrant slot via Army_Init |
| `SpawnTypedEnemySquads` | armycontrol | Spawns cycling unit types using enemy budget |
| `Egypt_ReinforcementWave` | armycontrol | Spawns mixed reinforcement wave for given player |
| `Egypt_GetReinforcementWaveSize` | armycontrol | Calculates wave size with acceleration and pop cap |
| `Egypt_GetHeldPoints` | armycontrol | Counts control points owned by a player |
| `AssignOldestWaitingArmyToBestTarget` | armycontrol | Reassigns idle army to highest-heat quadrant |
| `Egypt_GetOldestWaitingArmy` | armycontrol | Finds army with longest time since assignment |
| `ApplyCaptureModifier` | armycontrol | Grants capture ability to non-monk squads |
| `Egypt_InitControlPointSystem` | controlpoints | Iterates eg_villagecenters to init all control points |
| `ControlPoint_Init` | controlpoints | Creates control point data: owner, layout, garrisons, marker |
| `_Egypt_ControlPoint_Monitor` | controlpoints | Polls ownership changes, triggers rebuild + conversion |
| `Egypt_ControlPoint_MissionStart` | controlpoints | Sets initial control point state at mission start |
| `SaveVillageLayout` | controlpoints | Saves entity blueprints/positions around a control point |
| `Rebuild_Location` | controlpoints | Rebuilds destroyed buildings and spawns new garrison |
| `SpawnNewGarrison` | controlpoints | Starts garrison spawn rule for captured control point |
| `_SpawnGarrisonOverTime` | controlpoints | Interval rule spawning 1 garrison member at a time |
| `SpawnGarrisonMember` | controlpoints | Spawns single garrison unit if under cap (15) |
| `Convert_Location_VillLife` | controlpoints | Transfers villager life ownership on capture |
| `Init_Egypt_Difficulty` | data | Populates t_difficulty with all Util_DifVar parameters |
| `Init_Egypt_Data` | data | Initializes quadrants, army tables, tuning constants |
| `Egypt_InitObjectives` | objectives | Registers all OBJ/TOBJ objectives |
| `Egypt_GetControlBalance` | objectives | Updates control_balance with trend, ramp, acceleration |
| `Egypt_GetControlTrend` | objectives | Returns player held points minus enemy held points |
| `Egypt_RaiseStakesSlow` | objectives | Every 600s: boosts control_acceleration and reinforcement size |
| `Egypt_RaiseStakesFast` | objectives | Every 300s: shrinks attack interval, grows attack group size |
| `Egypt_AddTemplars` | objectives | One-shot at 300s: adds templars to enemy spawn rotation |
| `_Egypt_ReinforcementWaves` | objectives | Checks 90s timer, spawns both-side waves, transport ships |
| `Quadrant_Init` | quadrants | Creates quadrant with occupancy table and distance from home |
| `Quadrants_Init` | quadrants | Builds all quadrants from controlPoints + CRUSADERHOME_QUADRANT |
| `_Monitor_ControlPointAttackValues` | quadrants | Recursive heatmap evaluator: aggression, hostiles, range |
| `Get_BestControlPointTarget_ForArmy` | quadrants | Selects highest-heat quadrant factoring range and assigned armies |
| `Quadrant_GetSlot` | quadrants | Finds first unoccupied layer/offset slot |
| `Quadrant_GetPositionFromLayerAndSlot` | quadrants | Converts layer+offset to world position around marker |
| `Mission_SetupPlayers` | egypt | Initializes 7 players with relationships and colours |
| `Mission_Start` | egypt | Starts objectives, enemy spawn intervals, applies capture mods |
| `Mission_Preset` | egypt | Inits control points, data, disables hold on outposts/TCs |
| `AutoTest_OnInit` | automated | Entry point for CampaignAutoTest arg; registers checkpoints |
| `AutomatedEgypt_Phase1_SetUpPhase1` | automated | Sets up AI-driven player armies for automated testing |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Alexandria` | Information | Fail-state guard — if `control_balance ≤ 0`, calls `Mission_Fail()` |
| `OBJ_ControlPrimary` | Primary | Root objective — hold area; completes when all sub-objectives done → `Mission_Complete()` |
| `OBJ_Control` | TugOfWar_WithVelocity | Sub-objective tracking `control_balance`; completes at `≥ 1.0`; displays held point counts |
| `OBJ_Reinforcements` | Primary | 90-second countdown timer for reinforcement waves |
| `TOBJ_ControlPointTip` | Tip | UI hint explaining control point mechanics (child of OBJ_Control) |

### Difficulty

All values follow `Util_DifVar({Easy, Normal, Hard, Expert})` format:

**Player Mods:**
| Parameter | Values | Scales |
|-----------|--------|--------|
| `STARTING_SPEARMEN` | 10/10/5/5 | Initial player spearmen count |
| `STARTING_ARCHERS` | 10/10/5/5 | Initial player archer count |
| `STARTING_HORSEMEN` | 10/10/5/5 | Initial player horsemen count |

**Enemy Mods:**
| Parameter | Values | Scales |
|-----------|--------|--------|
| `STARTING_SPEARMEN` | 40/40/50/80 | Initial enemy spearmen |
| `STARTING_ARCHERS` | 100/100/100/80 | Initial enemy archers |
| `STARTING_MANATARMS` | 20/30/40/50 | Initial enemy men-at-arms |
| `STARTING_HORSEMEN` | 20/50/40/50 | Initial enemy horsemen |
| `STARTING_ARMYBUDGET` | 20/30/50/75 | Initial enemy reinforcement budget |
| `attack_group_size` | 10/10/10/15 | Units per enemy attack wave |
| `ATTACK_GROUP_SIZE_ACCELERATION` | 0/5/5/10 | Group size increase per 300s escalation |
| `ATTACK_GROUP_SIZE_CEILING` | 10/20/40/50 | Max attack group size |
| `ATTACK_INTERVAL` | 20/20/20/15 | Seconds between enemy squad spawns |
| `ATTACK_ACCELERATION` | 5/5/10/5 | Interval reduction per 300s escalation |
| `ATTACK_INTERVAL_FLOOR` | 15/10/5/5 | Minimum attack interval |
| `QUADRANT_COOLDOWN` | 90/90/30/10 | Cooldown between reassignments to same quadrant |
| `HOSTILECHECK_RADIUS` | 100/100/100/100 | Scan radius for heatmap evaluation |
| `AVOID_HOSTILE_COUNT_MULITPLIER` | 0/1/1.5/2 | Weight of hostile presence in heat calc |
| `RANGE_PRIORITY_MULTIPLIER` | 1.5/1/0.5/0 | Weight of distance-from-home in targeting |
| `AI_AGGRESSION_EMPTYLOCATION` | 200/1200/2000/10 | Heat bonus for undefended player points |
| `AI_AGGRESSION_WEAKLOCATION` | 200/400/800/1200 | Heat bonus for weakly defended points |
| `AI_AGGRESSION_FORTIFIEDLOCATION` | 200/400/400/800 | Heat bonus for heavily defended points |
| `AI_AGGRESSION_LOSINGMULTIPLIER` | 1/1.2/2/3 | Aggression multiplier when AI holds <5 points |

### Spawns

- **Player reinforcements**: Mixed composition (spearman/archer/horseman split ~⅓ each). Wave size = `12 + reinforcements_acceleration + 3 × wave_count`. Capped by pop capacity (200).
- **Enemy reinforcements**: Budget-based system. Each wave adds `wave_size` to `enemy_reinforcementbudget`. Budget is consumed by `SpawnTypedEnemySquads` which spawns `attack_group_size` units per call.
- **Enemy squad type rotation**: Cycles through `scar_archer → scar_spearman → scar_horseman → scar_militia`. After 300s, `templars` added (2+⌊size/3⌋ Templars + 1 Templar Master).
- **Garrison spawns**: When a control point is captured, the owning side spawns garrison units every 10s (1 at a time, capped at 15). Unit type determined by nearby buildings: stable→horseman, barracks→spearman, archery range→archer, town center→militia.
- **Transport ships**: 2 ships (player7) spawn at `mkr_player_boat_spawn` 10s before wave timer expires, sail to landing zone, then return.

### AI

- **No standard AI_Enable** for enemy player — entirely custom script-driven behavior via the quadrant heatmap system.
- **Heatmap evaluation** (`_Monitor_ControlPointAttackValues`): Runs recursively every 0.125s, cycling through all quadrants. Computes heat per control point based on:
  - `aiAgressionFactor`: Rewards attacking player-owned points (empty > weak > fortified). Boosted by `AI_AGGRESSION_LOSINGMULTIPLIER` when AI holds <5 points.
  - `hostileCountFactor`: Penalizes or rewards based on player unit presence, scaled by `AVOID_HOSTILE_COUNT_MULITPLIER`.
  - `CRUSADERHOME_QUADRANT`: Permanent heat of -10000 (never targeted).
- **Army targeting** (`Get_BestControlPointTarget_ForArmy`): For each army, picks highest-heat quadrant after applying range penalty (`distance² × -0.001`) and assigned-army penalty (`count × -200`).
- **Army assignment** (`AssignOldestWaitingArmyToBestTarget`): Runs every 1s. Selects army with longest idle time. If its current control point is contested, stays; otherwise reassigns to best target.
- **Automated testing**: `AutoTest_OnInit` enables `AI_Enable(player1, true)` to give AI control of the player, with attack/defend logic and ability usage (Saladin armor, Shirkuh speed).

### Timers

| Rule | Type | Interval | Purpose |
|------|------|----------|---------|
| `SpawnTypedEnemySquads` | Interval | ATTACK_INTERVAL (20/20/20/15s, decreasing) | Spawns enemy attack groups from budget |
| `AssignOldestWaitingArmyToBestTarget` | Interval | 1s | Reassigns idle enemy armies to targets |
| `_Egypt_ControlPoint_Monitor` | Interval | 1s | Polls control point ownership changes |
| `_Monitor_ControlPointAttackValues` | Recursive OneShot | 0.125s | Cycles heatmap evaluation across quadrants |
| `Egypt_GetControlBalance` | Interval | 1s | Updates tug-of-war control_balance value |
| `_Egypt_ReinforcementWaves` | Interval | 0.5s | Checks 90s countdown, triggers waves |
| `Egypt_RaiseStakesSlow` | Interval | 600s | Boosts control_acceleration (+0.5) and reinforcements_acceleration (+12) |
| `Egypt_RaiseStakesFast` | Interval | 300s | Shrinks attack interval, grows attack group size |
| `Egypt_AddTemplars` | OneShot | 300s | Adds templars to enemy spawn rotation |
| `_SpawnGarrisonOverTime` | Interval | 10s | Spawns 1 garrison unit per tick (cap 15) |
| `Egypt_AutoSaveInterval` | Interval | 600s | Triggers autosave |
| `SpawnTypedEnemySquads` (extra) | OneShot | 5/10/15s | Bonus early spawns on Normal/Hard/Expert |
| `VOCue_ControlUp_Query` | Interval | 1s | VO cue when control rising |
| `VOCue_ControlDown_Query` | Interval | 1s | VO cue when control falling |

## CROSS-REFERENCES

### Imports
| File | Imports |
|------|---------|
| `abb_m2_egypt.scar` | `MissionOMatic.scar`, `abb_m2_egypt_objectives.scar`, `villagerlife.scar`, `module_rovingarmy.scar`, `abb_m2_egypt_data.scar`, `abb_m2_egypt_quadrants.scar`, `abb_m2_egypt_armycontrol.scar`, `abb_m2_egypt_controlpoints.scar`, `abb_m2_egypt.events`, `abb_m2_egypt_automated.scar` |
| `abb_m2_egypt_armycontrol.scar` | `MissionOMatic.scar`, `abb_m2_egypt_quadrants.scar` |
| `abb_m2_egypt_controlpoints.scar` | `MissionOMatic.scar`, `abb_m2_egypt_data.scar`, `abb_m2_egypt_quadrants.scar`, `abb_m2_egypt_armycontrol.scar` |
| `abb_m2_egypt_data.scar` | `MissionOMatic.scar`, `module_rovingarmy.scar`, `abb_m2_egypt_quadrants.scar` |
| `abb_m2_egypt_objectives.scar` | `MissionOMatic.scar` |
| `abb_m2_egypt_quadrants.scar` | `MissionOMatic.scar`, `abb_m2_egypt_armycontrol.scar` |
| `abb_m2_egypt_automated.scar` | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic.scar`, `module_rovingarmy.scar`, `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals
- `control_balance` — written in `egypt.scar` (init 0.3), updated in `objectives.scar` (`Egypt_GetControlBalance`), read in objectives for win/fail
- `t_difficulty` — created in `data.scar`, read by `armycontrol.scar`, `quadrants.scar`, `objectives.scar`, `egypt.scar`
- `controlPoints` — created in `controlpoints.scar`, iterated by `quadrants.scar` (`Quadrants_Init`)
- `t_AllQuadrants` — created in `quadrants.scar`, read by `quadrants.scar` (heat eval, best target)
- `CRUSADERHOME_QUADRANT` — created in `quadrants.scar`, used by `armycontrol.scar` for army init
- `t_enemy_armies` / `t_enemy_armies_atCamp` — created in `data.scar`, managed by `armycontrol.scar`
- `enemy_reinforcementbudget` — init in `egypt.scar`, incremented in `armycontrol.scar`, consumed by `SpawnTypedEnemySquads`
- `reinforcement_wave_count` — init in `egypt.scar`, incremented in `objectives.scar`
- `reinforcements_acceleration` — incremented in `objectives.scar` (`Egypt_RaiseStakesSlow`), read in `armycontrol.scar`
- `ENEMY_SQUAD_TYPES` — init in `data.scar`, modified in `objectives.scar` (`Egypt_AddTemplars`), consumed in `armycontrol.scar`
- `eg_villagecenters`, `eg_controlpoints` — editor-placed EGroups referenced across multiple files
- `player1`–`player7` — 7-player setup in `egypt.scar`, referenced everywhere

### Inter-file Function Calls
- `egypt.scar` → `Egypt_InitControlPointSystem()`, `Init_Egypt_Data()`, `Init_Egypt_Difficulty()`, `Egypt_InitObjectives()`, `SpawnTypedEnemySquads()`, `AssignOldestWaitingArmyToBestTarget()`, `Egypt_ControlPoint_MissionStart()`, `AutoTest_OnInit()`, `_Monitor_ControlPointAttackValues()`, `ApplyCaptureModifier()`
- `objectives.scar` → `Egypt_GetHeldPoints()`, `Egypt_ReinforcementWave()`, `Distribute_Enemy_Army()`, `ApplyCaptureModifier()`, `AssignOldestWaitingArmyToBestTarget()`
- `controlpoints.scar` → `Quadrant_Init()`, `Quadrant_ReleaseSlot()`, `Army_Init()`, `VillagerLife_Find()`, `VillagerLife_GoToWork()`
- `armycontrol.scar` → `Quadrant_GetSlot()`, `Quadrant_GetPositionFromLayerAndSlot()`, `Quadrant_ReleaseSlot()`, `Army_Init()`, `Army_AddSGroup()`, `Army_SetTarget()`, `Get_BestControlPointTarget_ForArmy()`

### External Module Dependencies
- `module_rovingarmy.scar` — provides `Army_Init()`, `Army_AddSGroup()`, `Army_SetTarget()` used throughout army management
- `MissionOMatic.scar` — mission lifecycle framework (`Missionomatic_InitPlayer`, `Objective_Register/Start`, `Mission_Complete/Fail`)
- `villagerlife.scar` — `VillagerLife_Find()`, `VillagerLife_GoToWork()`, `VillagerLife_Create()` (commented out)
- `test/test_framework.scar` — `CampaignAutotest_RegisterCheckpoint()`, `CampaignAutotest_SetCheckpointStatus()` for automated QA