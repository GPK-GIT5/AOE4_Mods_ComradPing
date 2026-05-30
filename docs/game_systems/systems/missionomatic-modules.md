# MissionOMatic Module Reference

Cross-reference of the MissionOMatic framework architecture, module system, action/condition registries, and campaign usage patterns.

## Recipe Architecture

The recipe is a Lua table returned by `GetRecipe()` containing:

| Field | Purpose |
|-------|---------|
| `players` | Player definitions (civ, age, displayName); processed by `MissionOMatic_SetupPlayer` |
| `playAs` | Descriptor of the human player |
| `locations` | Location definitions (position, egroup, range); initialized as Location prefabs |
| `modules` | Behaviour module definitions with `type` dispatching to `<Type>_Init`; supports `difficulty` filtering |
| `battalions` | Unit group definitions for metagame reporting |
| `objectives` | Objective definitions with start/complete/fail conditions, actions, playbills, hintpoints |
| `metrics` | Custom metric definitions for post-mission reporting |
| `preStart.actions` | Actions run before mission starts (holds mission start) |
| `onStart.actions` | Actions run when mission begins |
| `introNIS` | Intro NIS event function |
| `audioSettings` | Campaign/mission name for audio system |
| `cameraStartMarker` | Initial camera position |
| `titlecard` | Mission title display |
| `shroud` | FOW configuration |

### Initialization Flow

1. `MissionOMatic_OnInit` — global SGroups, resources, subsystems
2. `MissionOMatic_Preset` — processes recipe: locations, modules, battalions, objectives
3. `MissionOMatic_PreStart` — runs `preStart.actions` and `introNIS`
4. `MissionOMatic_Start` — fades in, runs `onStart.actions`, triggers starting objectives

---

## Module System

### Module Lifecycle

All modules share: `Init → Monitor → GetSGroup/AddSGroup/RemoveSGroup → Disband → IsDefeated`

1. `<Type>_Init(data)` — Spawns units, creates Encounter, registers in `t_allModules` and type-specific list
2. `<Type>_Monitor` — Interval rule for reinforcement and state checks
3. `<Type>_GetSGroup` / `<Type>_AddSGroup` / `<Type>_RemoveSGroup` — Unit management
4. `<Type>_Disband` — Full teardown, returns units
5. `<Type>_IsDefeated` — Returns `true` if SGroup is empty
6. `<Type>_UnitRequest_ProvideEstimate` / `<Type>_UnitRequest_Start` — Unit provider interface

### Module Types

| Type | Purpose | Key Parameters | Monitor Interval |
|------|---------|---------------|-----------------|
| **TownLife** | AI economy (villagers, gathering, building). Uses skirmish AI via `AIPlayer_GetOrCreateHomebase`. Internal Wave manager for unit production. | `homebase`, `canBuild`, `unitSources` | 5s |
| **Defend** | Hold position with Defend encounter plan. Supports `withdrawData` (flee conditions). | `combatRange`, `leashRange`, `withdrawData`, `triggerOnSight/Engage/UnderAttack` | 1s |
| **Attack** | Assault target with Attack encounter plan. Dynamic target updates. | `target`, `attackMoveStyle`, `combatRange` | 5s |
| **RovingArmy** | Mobile force cycling through target waypoints. State machine with withdraw threshold. | `targets`, `targetOrder`, `withdrawThreshold`, `fallback` | 1s |
| **UnitSpawner** | Barebones spawner for pre-placed or off-map units. | `spawnRate`, `onlyRespondToTargetedRequests` | configurable |

### RovingArmy Targeting Modes

| Mode | Behavior |
|------|----------|
| `Discard` | Abandon target on completion, move to next |
| `Cycle` | Loop through targets sequentially |
| `Reverse` | Reverse direction at endpoints |
| `Proximity` | Target nearest waypoint |
| `Random` | Random next target |
| `RandomMeandering` | Random with meandering patrol behavior |

### RovingArmy States

`ARMY_STATUS_EMPTY` | `ATTACKING` | `DEFENDING` | `DISSOLVED` | `DISSOLVING_INTO_MODULE`

---

## Action & Condition Registries

### Built-in Actions

Actions follow `Action_<name>_Do(action, context)`. Return nothing (immediate) or `WAIT_FOR_ACTION_TO_FINISH` with `Action_Finish(context)` (async).

| Name | Purpose |
|------|---------|
| `StartObjective` | Start an objective with optional sub-objectives |
| `CompleteObjective` | Complete an objective |
| `FailObjective` | Fail an objective |
| `Wait` | Delay action list for N seconds |
| `CallScarFunction` | Call arbitrary SCAR function by name |
| `PlaySpeechEvent` | Play intel speech event, wait for completion |
| `NotifyPlayer` | Create event cue, minimap blip, FOW reveal |
| `SpawnUnits` | Spawn units at a location |
| `SpawnUnitsToModule` | Spawn units into a behaviour module |
| `DissolveModuleIntoModule` | Transfer all units between modules |
| `MissionComplete` | Trigger mission victory |
| `MissionFail` | Trigger mission failure |
| `SetMusicIntensity` | Lock/unlock music intensity |
| `Loop` | Loop a playbill back to a given stage |
| `ExpositionCamera` | Play exposition camera sequence |
| `SnapCamera` | Snap camera to position |
| `BookmarkTime` | Create named game-time timestamp |
| `SetInvulnerable` | Set entity invulnerability |
| `MoveUnits` | Move units to a position |
| `AddResources` | Grant resources to player |

### Built-in Conditions

Conditions follow `Condition_<name>_Check(condition, context) → bool`.

**Combinators:** `CONDITION_LIST_ALL`, `CONDITION_LIST_ANY`, `CONDITION_LIST_NONE`

| Name | Purpose |
|------|---------|
| `Boolean` | ALL/ANY/NONE combinator |
| `GameTime` | Elapsed game time vs. threshold |
| `HasUnits` | Player unit count, optionally by type/tag |
| `HasBuildings` | Player building count by type |
| `HasResources` | Player resource amount check |
| `HasReachedAge` | Player age requirement |
| `UnitAtLocation` | Units near a marker/location |
| `TaggedUnitAtLocation` | Tagged units near location |
| `UnitsSpotted` | Player can see tagged/module units |
| `UnitsKilled` | Tagged/module units all dead |
| `ModuleDefeated` | Module's units all dead |
| `LocationCaptured` | Location has been captured |
| `LocationRazed` | Location has been razed |
| `ObjectiveIsComplete` | Objective completion status |
| `SubobjectivesAreComplete` | Child objectives complete |
| `ObjectiveCounter` | Objective counter threshold |
| `ObjectiveTimer` | Objective timer threshold |
| `AskScarFunction` | Arbitrary function as condition |

---

## Playbill System

Playbills are sequences of `{conditions, actions}` stages running in parallel (same ID).

- `Playbill_Start(id, sequences)` — launches parallel sequences
- `Playbill_Stop(id)` — stops all sequences with given ID
- `Playbill_Manager` — per-second rule checking conditions, running actions
- Supports looping via `Action_Loop_Do`

---

## Objective Lifecycle

**Register → Start → [Monitor conditions] → Complete/Fail**

### Recipe Objective Fields

| Field | Purpose |
|-------|---------|
| `descriptor` | String identifier |
| `title`, `description` | Display text |
| `type` | `OT_Primary` / `OT_Secondary` |
| `isStartingObjective` | Auto-start on mission begin |
| `parent` | Link as sub-objective |
| `start.actions` / `start.preactions` / `start.intelEvent` | On-start hooks |
| `complete.conditions` | ConditionList checked every second |
| `complete.actions` / `complete.preactions` | On-complete hooks |
| `fail.conditions` / `fail.actions` | Failure hooks |
| `playbill` | Attached playbill started/stopped with objective |
| `countDown` / `counterGoal` | Timer/counter display |
| `hintpoints` | UI elements (blips, arrows, reticules) |

---

## Unit Request Pipeline

Modules request reinforcements via `MissionOMatic_RequestUnits(requestingModule, requestData, unitSources)`.

1. Requesting module calls `Reinforcement_AreReinforcementsNeeded` (compares current vs ideal composition)
2. `MissionOMatic_RequestUnits` solicits estimates from potential providers
3. Best provider starts production (`UnitRequest_Start`)
4. On completion, `MissionOMatic_RequestComplete` delivers units to requester's `AddSGroup`

### Provider Priority
- **TownLife** — primary provider (spawns via internal wave manager)
- **Defend** — secondary provider (provides units, then backfills from TownLife)
- **Attack** — can provide units to other modules on request
- **UnitSpawner** — off-map provider with configurable spawn rate

---

## Wave System (`missionomatic_wave.scar`)

Waves spawn units from production buildings with per-unit-type build-time cooldowns.

1. `Wave_New(data)` — Creates wave with player, spawn (egroup/marker), units, staging/assault modules
2. `Wave_Prepare` — Begins spawning; units go into staging module first
3. `Wave_Launch` — Transfers staged units to assault module
4. `Wave_Monitor` — Checks available spawns, spawns units when cooldowns expire

**Options:** `auto_launch` (automatic when all spawned), `use_separate_spawns` (per-building), difficulty filtering via `Wave_FilterUnitsByDifficulty`

**Unit type categories:** infantry, ranged, cavalry, siege, town_center, religious

---

## Raiding System (`missionomatic_raiding.scar`)

Autonomous AI raiding via `Raiding_Init`:
- RovingArmy-based raid parties with exclusion radius/timer
- Party limit and size controls
- Scout probes for map awareness
- Proximity-based target assignment
- `raiderComposition` with ratio-based unit generation
- `Util_DifVar`-scaled timing: `{120, 120, 90, 60}` cooldown, `{80, 80, 70, 60}` scout timing

---

## Leader System (`missionomatic_leader.scar`)

Hero/leader downed/recovery mechanic:
- On low health: transfer to `neutralHolder`, become immobile, lose LoS
- Recovery objective `OBJ_RecoverDownedLeader` with UI hintpoints
- On recovery: return to owner, health restored to `Util_DifVar({1.0, 0.5, 0.4, 0.3})`
- Handles control group preservation, selection clearing, music stingers

---

## Upgrade System (`missionomatic_upgrades.scar`)

Per-civ tables organized by age (AGE_DARK/FEUDAL/CASTLE/IMPERIAL) plus `ALWAYS_REMOVE`.

**Supported civs:** English, Normans, French, Rus, Mongol (standard/improved/double variants), HRE, Chinese

Activated via `PlayerUpgrades_Auto(player, bool)`.

---

## Shared Globals

| Global | Type | Purpose |
|--------|------|---------|
| `MissionRecipe` | Table | Active mission recipe |
| `t_allModules` | Table | All initialized modules |
| `t_attackModules` | Table | Attack module instances |
| `t_defendModules` | Table | Defend module instances |
| `t_rovingArmyModules` | Table | RovingArmy module instances |
| `t_townLifeModules` | Table | TownLife module instances |
| `t_unitSpawnerModules` | Table | UnitSpawner module instances |
| `g_missionObjectives` | Table | All registered objectives |
| `g_waves` | Table | All active waves |
| `g_raidSystem` | Table | Active raid system state |
| `t_allLeaders` | Table | All leader instances |
| `g_allied_banner_armies` | Table | Allied banner armies |
| `sg_startingUnits` | SGroup | Units at mission start |
| `eg_startingBuildings` | EGroup | Buildings at mission start |
| `sg_scriptSpawnedUnits` | SGroup | Script-spawned units |
| `sg_waveManagerStagedUnits` | SGroup | Units in wave staging |
| `PLAYERS` | Table | Player data |
| `EVENTS` | Table | Speech/intel event functions |
| `g_timeStamps` | Table | Named time bookmarks |
| `content_pack` | Number | Campaign ID (1=Vanilla, 2=AoW, 3=Abbasid, 4=Rogue) |

---

## Timers

| Timer | Interval | Purpose |
|-------|----------|---------|
| `ActionList_Manager` | every frame | Process running action lists |
| `Playbill_Manager` | 1s | Check playbill conditions per stage |
| `Wave_MonitorAllWaves` | 1s | Spawn units when build times expire |
| `Attack_Monitor` | 5s | Attack module reinforcement requests |
| `Defend_Monitor` | 1s | Flee conditions & reinforcement checks |
| `_RovingArmy_Monitor` | 1s | Withdraw threshold & reinforcement checks |
| `TownLife_Monitor` | 5s | TownLife reinforcement requests |
| `Missionomatic_CheckLeader` | 0.125s | Leader surrender/recovery state |
| `_Raiding_Monitor` | 1s | Raid timer, scout spawning, idle check |
| `_MonitorAllyArmy` | 15s | Allied banner reinforcement |

---

## Campaign Recipe Patterns

### Module Count Ranges

| Campaign | Defend | RovingArmy | TownLife | UnitSpawner | Complexity |
|----------|--------|------------|---------|-------------|------------|
| Abbasid | 6–34 | 2–6 | 0 | Yes | Medium |
| Angevin | 3–7+ dynamic | 7–12 | 0 | Yes (dynamic) | High |
| Challenges | 0 | 0–4 | 0 | 0 | Minimal |
| Hundred | 10–19 | 12–26 | 0 | Yes (8) | Full |
| Mongol | 7–16 | 4–16 | Yes (3) | Yes (6–9) | Full |
| Rogue | 0 | 2–8 | 0 | 0 | Framework |
| Russia | 12–25 | 4–5 | Yes (1) | Yes | Full |
| Salisbury | 5–20 | 2 | 0 | 0 | Minimal |

### Recipe Complexity by Campaign

| Level | Campaigns | Characteristics |
|-------|-----------|----------------|
| **Minimal** | Challenges, Salisbury | No recipe modules/locations; all behavior scripted via custom functions or training system |
| **Medium** | Abbasid | Modules in recipe but objectives registered manually; custom Army_Init systems |
| **Full** | Angevin, Hundred, Mongol, Russia | Complete recipe with locations, modules, objectives, playbills; `Wave_New` pipeline |
| **Framework** | Rogue | Delegates to `rogue.scar` infrastructure; `Rogue_AddLane`/`Rogue_UseDefaultSchedule` replaces modules |

### Common Location Wiring Patterns

| Pattern | Usage | Campaigns |
|---------|-------|-----------|
| **Marker-based** (`mkr_*`) | Module spawn/target positions, patrol waypoints | All |
| **EGroup-based** | Wall/building collections for destruction tracking | Angevin, Mongol, Russia |
| **Dynamic marker generation** | `AllMarkers_FromName()` → auto-create modules | Angevin (Rochester) |
| **Lane-based** | Wave spawn → staging → assault target chains | Hundred, Russia, Rogue |
| **Proximity zones** | Trigger defender spawning on player approach | Mongol (Kiev sprawl) |
| **Named locations** | Recipe `locations` field with capture objectives | Russia (Smolensk) |

### Objective → Module Dependency Patterns

| Pattern | Description | Example |
|---------|-------------|---------|
| **Module defeat = objective complete** | `ModuleDefeated` condition on Defend module | Most garrison missions |
| **Objective gates module spawn** | Completing an objective activates new wave/module | Mongol gate breach → defenders |
| **Objective disables module** | Completing side objective stops attack waves | Angevin outpost destruction |
| **Module strength triggers reinforcement** | Defenders below 50% → dissolve reinforcements into module | Angevin Wallingford |
| **Objective modifies wave power** | Fort destruction increases wave interval | Hundred Orleans (+20s per fort) |
| **Event-driven module activation** | Building destruction/capture triggers new module phase | Russia village capture |
| **Sequential objective chains** | Linear progression through build → produce → march → destroy | Salisbury tutorials |

### Most Common MissionOMatic API Calls

1. `MissionOMatic_FindModule()` — locate modules by descriptor
2. `UnitEntry_DeploySquads()` — spawn unit groups
3. `Objective_Register/Start/Complete()` — objective lifecycle
4. `Army_Init()` / `RovingArmy_Init()` / `Defend_Init()` — module creation
5. `Wave_New()` / `Wave_Prepare()` — wave pipeline
6. `PlayerUpgrades_Auto()` — auto-upgrade system
7. `Missionomatic_InitializeLeader()` — hero setup
8. `DissolveModuleIntoModule()` / `TransferModuleIntoModule()` — unit transfer
9. `Rule_AddOneShot()` / `Rule_AddInterval()` — timer scheduling
10. `Raiding_Init()` — cavalry raid system

---

## Import Chain

```
missionomatic.scar
  ├── cardinal.scar
  ├── scarutil.scar
  ├── training.scar + training/core*
  ├── gathering_utility.scar
  ├── core_encounter.scar
  ├── ai/wave_generator.scar
  ├── ai/army.scar
  ├── gameplay/currentageui.scar
  ├── GroupCallers.scar
  ├── formation.scar
  └── unit_trainer.scar
```

### Inter-file Function Calls

| Function | Called By |
|----------|----------|
| `MissionOMatic_FindModule` | Actions, conditions, wave spawning, dissolve utilities |
| `MissionOMatic_FindObjective` | Objective actions and conditions |
| `MissionOMatic_RequestUnits` / `RequestComplete` | All module monitors and unit providers |
| `Reinforcement_AreReinforcementsNeeded` | All module monitors |
| `Prefab_DoAction(module, "ActionName")` | Universal module dispatch |
| `ActionList_PlayActions` | Objectives, playbills, utility wrappers |
| `ConditionList_CheckList` | Objectives and playbill manager |
| `Encounter_Create` / `SetGoalData` / `Stop` | All combat modules |
| `ResolveSpawnLocation` | Modules, waves, raiding |
| `UnitEntry_DeploySquads` | All modules, waves, raiding |
| `DissolveModuleIntoModule` | Actions, RovingArmy fallback, Defend withdrawal |
| `AI_Module_ResolveCombatArea` | Defend, RovingArmy, Attack |
