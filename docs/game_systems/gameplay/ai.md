# Gameplay: AI & Encounter Plans

## OVERVIEW

The AI & Encounter Plans system provides the scripted AI behavior layer for AoE4 campaigns. At its core, the **Army** system manages groups of AI-controlled units that attack, defend, or patrol through sequences of targets, delegating low-level behavior to **ArmyEncounterFamily** objects that wrap the engine's `AIStateTree` encounters. The **Encounter Plan** architecture (Attack, Defend, Move, DoNothing, TownLife) provides a phase-based framework for fine-grained control over AI combat behavior — configuring formation coordinators, attack-move styles, fallback conditions, and building engagement policies. Supporting systems include **WaveGenerator** for timed unit production and staged army launches, and **CombatFitness** utilities for simulating and evaluating unit matchups.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| ai_encounter_util.scar | core | String conversion helpers for AI encounter end-reasons and notification types |
| army_encounter.scar | core | ArmyEncounterFamily/ArmyEncounterChild classes — manages split encounters and state tree notifications |
| army.scar | core | Army class — high-level AI unit group management with target sequencing, attack/defend/transport lifecycle |
| combat_fitness_util.scar | automated | Combat fitness simulation — launches encounters, measures health, computes scores, spawns test combinations |
| combat_fitness_consts.scar | data | Filter list of SBPs excluded from combat fitness characterization |
| wave_generator.scar | core | WaveGenerator class — timed unit spawning with build-time simulation, staging/assault army integration |
| plan_attack.scar | core | Attack encounter plan — configures StateTree for attacking a target with full tuning support |
| plan_defend.scar | core | Defend encounter plan — idle-phase triggers, defensive StateTree configuration |
| plan_move.scar | core | Move encounter plan — FormUp/Move/Intercept phases using legacy FormationPhase encounters |
| plan_donothing.scar | core | Placeholder encounter plan — reserves an encounter ID without issuing commands |
| plan_townlife.scar | core | TownLife encounter plan — villager-style AI behavior in a defined area |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `AIFormationPhaseEncounter_EndReason_ToString` | ai_encounter_util | Convert end-reason enum to debug string |
| `AIFormationPhaseEncounter_NotificationType_ToString` | ai_encounter_util | Convert notification type enum to debug string |
| `ArmyEncounter_InitSystem` | army_encounter | Initialize global encounter family tracking tables |
| `ArmyEncounterFamily:new` | army_encounter | Create encounter family from army and state models |
| `ArmyEncounterFamily:start` | army_encounter | Cluster squads and launch parent/child StateTree encounters |
| `ArmyEncounterFamily:stop` | army_encounter | Cancel all encounters in family via AIEncounter_Cancel |
| `ArmyEncounterFamily:markDone` | army_encounter | Handle encounter completion, promote children to parent |
| `ArmyEncounterFamily:addAndTriggerParentOrChild` | army_encounter | Spawn a StateTree encounter for a squad subgroup |
| `ArmyEncounterFamily_NotificationFromStateTree` | army_encounter | Global callback dispatching StateTree notifications to armies |
| `Army_InitSystem` | army | Initialize building presets, encounter types, army parameter tables |
| `Army_Init` | army | Create and configure a new Army with units, spawn, targets |
| `NavalArmy_Init` | army | Shortcut for naval armies with appropriate building presets |
| `Army_Dissolve` | army | Destroy army, optionally return units to an SGroup |
| `Army_AddSGroup` | army | Add squads to army, restart encounter if active |
| `Army_RemoveSGroup` | army | Remove squads with async AI release callback |
| `Army_SetTarget` | army | Replace all targets with a single new target |
| `Army_SetTargets` | army | Replace all targets with a new target list |
| `Army_AddTarget` | army | Append a target to the army's target sequence |
| `Army_IsComplete` | army | Check if army finished all targets and is defending |
| `Army_IsDead` | army | Check if army has lost all units |
| `Army_IsAttacking` | army | Check if army is in attack state |
| `Army_IsDefending` | army | Check if army is in defend state |
| `Army_IsBlocked` | army | Check if army is blocked by walls |
| `_Army_AttackTarget` | army | Create attack StateTree encounter for a target index |
| `_Army_DefendCombatArena` | army | Create defend StateTree encounter for a combat arena |
| `_Army_NavalTransport` | army | Create naval transport encounter with transport ships |
| `_Army_Victory` | army | Handle target cleared — advance to next or complete |
| `_Army_Death` | army | Handle army death — callbacks, reset, or dissolve |
| `_Army_Blocked` | army | Handle path blocked — defend current position |
| `_Army_CreateCommonStateModels` | army | Build full state model tuning table for encounters |
| `LaunchEncounter` | combat_fitness_util | Launch a test attack encounter at a position |
| `FightIsFinished` | combat_fitness_util | Detect combat end via health tracking and timeout |
| `TotalHealthOfPlayer` | combat_fitness_util | Sum all squad and entity health for a player |
| `CreateSpawnCombination` | combat_fitness_util | Generate random unit compositions from BP options |
| `GenerateArchetypeMapping` | combat_fitness_util | Map SBPs to combat fitness archetype categories |
| `SpawnCombination` | combat_fitness_util | Instantiate a unit combination at a position |
| `TestCharacterization` | combat_fitness_util | Validate combat fitness data for all squad BPs |
| `WaveGenerator_Init` | wave_generator | Create a wave generator with spawn/staging/assault config |
| `WaveGenerator_SetUnits` | wave_generator | Set the unit table for future wave preparation |
| `WaveGenerator_Prepare` | wave_generator | Begin spawning a wave of units with build-time delays |
| `WaveGenerator_Launch` | wave_generator | Transfer staged units from staging army to assault army |
| `WaveGenerator_Monitor` | wave_generator | Tick function — spawn units, check readiness, auto-launch |
| `WaveGenerator_FilterUnitsByDifficulty` | wave_generator | Remove unit rows that don't match current difficulty |
| `AttackPlan_RegisterPlan` | plan_attack | Register the Attack plan with default goal data |
| `AttackPlan_MainPhase_Start` | plan_attack | Configure and launch attack StateTree encounter |
| `AttackPlan_MainPhase_Notification` | plan_attack | Route StateTree end-reasons to encounter finish states |
| `DefendPlan_RegisterPlan` | plan_defend | Register the Defend plan with idle/main phases |
| `DefendPlan_IdlePhase_Start` | plan_defend | Start idle monitoring — sight/engage/attack triggers |
| `DefendPlan_MainPhase_Start` | plan_defend | Configure and launch defend StateTree encounter |
| `MovePlan_RegisterPlan` | plan_move | Register the Move plan with FormUp/Move/Intercept phases |
| `MovePlan_FormUpPhase_Start` | plan_move | Create legacy FormationPhase encounter for grouping |
| `MovePlan_MovePhase_Start` | plan_move | Create move encounter with optional attack-move scanning |
| `MovePlan_InterceptPhase_Start` | plan_move | Create combat encounter for enemies met en route |
| `DoNothingPlan_RegisterPlan` | plan_donothing | Register placeholder plan — no AI commands issued |
| `TownLifePlan_RegisterPlan` | plan_townlife | Register TownLife plan for villager area behavior |
| `TownLifePlan_MainPhase_Start` | plan_townlife | Create TownLife encounter with optional build permission |

## KEY SYSTEMS

### Army System

The Army is the primary scripted AI abstraction. Key lifecycle:

1. **Initialization** — `Army_Init(params)` accepts player, units (spawned via `CreateUnits`), spawn location, targets, and combat arena parameters. Units are placed in an internal SGroup.
2. **Target Sequencing** — Armies process targets in order (`TARGET_ORDER_LINEAR`, `LOOP`, `PATROL`, `RANDOM`). On victory at a target, they advance; on completion of all targets, they defend the final one.
3. **State Machine** — States are `ENCOUNTER_TYPE_ATTACK`, `DEFEND`, `TRANSPORT`, `EMPTY`, `NONE`. Transitions are driven by StateTree notifications.
4. **Death/Revival** — When all units die, `onDeathFunction` fires. If `onDeathReset=true`, the army restarts from target 1 when refilled. `onDeathDissolve=true` permanently removes the army.
5. **CombatArena** — Targets can be positions, markers, or tables with per-target overrides for combat range, leash range, building engagement, idle time, and facing direction.

**Building Engagement Presets:**
- `BUILDINGS_NONE` — ignore all buildings
- `BUILDINGS_ALL` — attack all except settlements/walls
- `BUILDINGS_ALL_BUT_TC` — exclude town centers
- `BUILDINGS_THREATENING` — only attack defensive structures
- `BUILDINGS_IMPORTANT` — skip houses/farms

**Combat Arena Parameters (defaults):**
- `combatRangeAtTarget/EnRoute` = 35
- `leashBuffer` = 10
- `idleTime` = 0
- `ramsBuiltWhenBlocked` = 1
- `ramPassengerCount` = 8
- `siegeTowerPassengerCount` = 8
- `openPathThreshold` = 120
- `brokenWallThreshold` = 30

### ArmyEncounterFamily

Handles the case where an army's squads are too spread out to fit in one AI encounter:

1. `SGroup_DivideIntoClusters` splits squads into groups (50-unit threshold)
2. First cluster becomes the **parent** encounter; others become **children**
3. Each cluster gets its own `AIStateTree_SpawnRootControllerWithStateModelTunings` call
4. When a child completes, it's removed; when the parent completes, a child is promoted
5. When all encounters complete, `_Army_NotificationFromEncounterFamily` fires the army-level callback
6. Handles siege tower release (squads split mid-encounter) and field-constructed ram addition

**End Reasons** (from `AIFormationPhaseEncounter_EndReason`):
- `AtDestination` — arrived at target position
- `EnemiesAtTargetCleared` — all enemies in area defeated
- `Timeout` — preset timer expired
- `CombatThreshold` — remaining enemies too weak to engage
- `ShouldFallback` — fallback conditions met
- `SelfSquadsEmpty` — all squads destroyed
- `CannotReachDestination` — pathing blocked
- `Torndown` — encounter manually cancelled (for `Army_RemoveSGroup`)
- `WasAttacked` — units were attacked (used by Move plan)

### Encounter Plans

Plans are registered via `Encounter_RegisterPlan()` and define **phases** with start/notification/end callbacks plus **defaultGoalData**.

#### Attack Plan
- Single phase: `Main`
- Target types: position, marker, SGroup, EGroup
- Configures `Cardinal_CreateAIEncounterWithStateModelTunings` with branch `campaign_encounters\scar_encounters\AttackDefault`
- Tunings blueprint: `campaign_attack_default`
- Supports: form-up positioning, idle-at-end, fallback thresholds, archer repositioning, ram building, siege tower passengers
- **Attack-move styles** control en-route and at-target building engagement independently:
  - `attackMoveStyle_ignoreEverything` — bypass all buildings  
  - `attackMoveStyle_ignorePassive` — skip houses/farms/economy
  - `attackMoveStyle_normal` / `attackMoveStyle_aggressive` — default building engagement
  - `attackMoveStyle_attackEverything` — engage all except settlements/walls
  - `attackMoveStyle_excludeTC` — attack everything except town centers

#### Defend Plan
- Two phases: `Idle` → `Main`
- Idle phase monitors via `Rule_AddInterval` at 0.5s:
  - `triggerOnSight` — uses `Event_EncounterCanSeePlayerSquads`
  - `triggerOnEngage` — checks `SGroup_IsDoingAttack`
  - `triggerOnUnderAttack` — checks `SGroup_IsUnderAttack`
- `idleReactionTime` delays transition to Main phase
- Main phase uses `campaign_defend_default` tunings blueprint
- Defend encounters should not normally end; `AtDestination` is treated as a failure unless the target was destroyed

#### Move Plan
- Three phases: `FormUp` → `Move` → `Intercept`
- Uses **legacy** `AI_CreateRestoreEncounter` with `AIEncounterType_FormationPhase` (not StateTree)
- FormUp: gathers units within `formUpRange`, requires 90% at position
- Move: navigates to target with optional attack-move scanning
- Intercept: triggered when combat encountered en route; clears enemies then returns to FormUp
- Archer min-range tactic with priority 1

#### DoNothing Plan
- Single empty phase; reserves an encounter ID for later use

#### TownLife Plan
- Uses `AIEncounterType_TownLife` (legacy encounter)
- Villagers work in area around target; optional `canBuild` flag
- No StateTree — direct encounter API calls

### WaveGenerator System

Manages timed unit production for campaign AI waves:

1. **Init** — requires player, spawn location, assault army (and optional staging army)
2. **SetUnits** — defines unit composition with `type`, `sbp`, `numSquads`, optional `difficulty` filter
3. **Prepare** — begins spawning. Units are created one at a time with build-time delays
4. **Launch** — transfers all staged units from staging army to assault army via `Army_RemoveSGroup`/`Army_AddSGroup`
5. **Monitor** — runs every 1s via `Rule_AddInterval`, handles spawn timing and auto-launch

**Build Times** (simulated, not real production):
- Villager/Scout: 20s | Spearman/Archer/Militia: 15s | MAA/Crossbow/Horseman/Landsknecht: 22s
- Knight/Camel/Horse Archer: 35s | Handcannoneer: 35s | Monk: 30s
- Ram/Springald/Siege Tower: 30s | Mangonel/Trebuchet: 40s | Cannon/Bombard/Culverin/Ribauldequin: 45s

**Spawn Types** — buildings map to unit categories:
- barracks → infantry | archery_range → ranged | stable → cavalry
- siege_workshop → siege | town_center → town_center | monastery → religious
- universal → all categories

**Auto-launch** options:
- `auto_launch_after_prepare` — launch immediately or after N seconds from prepare
- `auto_launch_after_ready` — launch when all units are spawned, with optional delay

### Combat Fitness System

An automated testing/simulation framework, not used in gameplay:

- `LaunchEncounter` — spawns a test attack encounter with hardcoded tunings
- `CreateSpawnCombination` — generates randomized unit compositions from available BPs
- `GenerateArchetypeMapping` — maps BPs to AI combat archetypes via `AI_CombatFitnessGetSquadArchetypeNames`
- `TestCharacterization` — validates that all BPs have combat fitness data
- `ComputeScore` — calculates win/loss ratio from initial/final health values
- `CombatFitness_characterizationFilters` — ~100 BP name patterns excluded from testing (dev units, campaign units, prototypes, duplicates)

### StateTree Tuning Parameters

Both Attack and Defend plans configure the same comprehensive set of tunings:

**Boolean Tunings:**
- `ai_phase_encounter_clear_enemy_squads/buildings` — whether to engage units/buildings
- `ai_phase_encounter_exit_on_path_blocker_detected` — exit when walls block path
- `ai_phase_encounter_disable_cavalry_build_rams` — prevent auto-ram construction
- `ai_phase_encounter_should_hold_position` — hold position while idle at target
- `ai_phase_encounter_attack_final_target` — attack-move to final target (SGroup/EGroup targets)
- `ai_phase_encounter_allow_attack_move` — use attack-move vs forced attack

**Float Tunings:**
- `ai_phase_encounter_combat_area` — fight-continuation radius (default 30)
- `ai_phase_encounter_combat_leash` — max pursuit distance
- `ai_phase_encounter_destination_combat_area` — transition radius from en-route to at-target
- `ai_phase_encounter_destination_area` — arrival threshold (based on formation dimensions)
- `ai_phase_encounter_enemy_scan_range` — enemy detection radius
- `ai_phase_encounter_idle_at_end_seconds` — post-arrival idle time
- `ai_phase_encounter_fallback_combat_rating` — combat rating retreat threshold
- `ai_phase_encounter_fallback_squad_health_threshold` — health-based retreat
- `ai_phase_encounter_archer_reposition_time_interval` — archer micro timing
- `ai_phase_encounter_open_path_length_to_look_for_siege_path` — wall detour threshold (default 120)

**Integer Tunings:**
- `ai_phase_encounter_override_encounter_id` — SCAR-assigned encounter ID
- `ai_phase_encounter_notify_rule_id` — callback rule ID for notifications
- `ai_phase_encounter_ram_max_passenger_count` — units per ram
- `ai_phase_encounter_ram_number_to_build` — rams to construct when blocked

## CROSS-REFERENCES

### Import Chain
```
plan_attack.scar  ──→ ai_encounter_util.scar, cardinal_encounter.scar
plan_defend.scar  ──→ cardinal_encounter.scar
plan_move.scar    ──→ (no explicit imports shown)
combat_fitness_util.scar ──→ Cardinal.scar, ai/ai_encounter_util.scar
army_encounter.scar ──→ scarutil.scar
army.scar ──→ ai/army_encounter.scar
wave_generator.scar ──→ ai/army.scar
```

### Key Engine API Dependencies
- `AIStateTree_SpawnRootControllerWithStateModelTunings` — core StateTree encounter creation (army_encounter, combat_fitness_util)
- `Cardinal_CreateAIEncounterWithStateModelTunings` — encounter plan StateTree creation (plan_attack, plan_defend)
- `Cardinal_CleanupAIEncounter` — encounter teardown (plan_attack, plan_defend)
- `AI_CreateRestoreEncounter` / `AIEncounter_Trigger` — legacy encounter API (plan_move, plan_townlife)
- `AI_GetAndReserveNextTaskID` — allocate encounter IDs
- `EventRule_GetNextUniqueRuleID` — allocate callback rule IDs
- `UnsavedEventRule_AddRuleIDEvent` — register for `GE_AIPlayer_EncounterNotification`
- `BP_GetAIFormationCoordinatorBlueprint` — load formation coordinator BPs
- `BP_GetAIStateModelTuningsBlueprint` — load tuning pack BPs
- `SGroup_DivideIntoClusters` — cluster squads for encounter splitting
- `Formation_GetDimensionsAndOffset` — calculate formation size for destination area
- `AI_CombatFitnessGetSquadArchetypeNames` / `AI_CombatFitnessGetSquadArchetypePBGs` — combat fitness archetype API
- `AI_CalculateCombatFitnessEstimate` — engine-level combat prediction

### Shared Globals
- `t_armyEncounterFamily_allFamilies` — all active encounter families
- `t_armyEncounterFamily_releasedSquadInfo` / `addedSquadInfo` — pending squad notifications
- `t_allArmies` — all active armies
- `t_allModules` — shared module tracking (army is also a module)
- `g_wave_generators` — all active wave generators
- `g_wave_generator_unit_type_info` — unit type → category + build time mapping
- `g_wave_generator_spawn_type_info` — building type → spawnable categories mapping
- `t_cardinalEncounters_allAddedSquadsInfo` — pending squad-add tracking (encounter plans)
- `sg_waveManagerStagedUnits` — intermediate SGroup for staged wave units
- `_b_debugEncounterPlans` — global debug flag for encounter plan logging
- `DEBUG_ARMY` / `DEBUG_ARMY_ENCOUNTER` — debug flags (set via `army_debug` / `army_encounter_debug` command line)
- `DEBUG_WG` — wave generator debug flag (set via `wave_generator_debug` command line)

### Campaign Usage Pattern
Campaigns typically:
1. Call `Army_Init` with player, unit table, spawn marker, and target markers
2. Set `attackBuildings`, `combatRange`, `targetOrder` per army
3. Use `WaveGenerator_Init` for repeating attack waves with `auto_launch_after_ready`
4. Use encounter plans indirectly via `cardinal_encounter.scar` (not shown in these files)
5. Monitor army state via `Army_IsComplete`, `Army_IsDead`, `Army_IsBlocked` callbacks
