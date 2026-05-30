# Gameplay: Training System

## OVERVIEW

The Training System is Age of Empires IV's dynamic in-game hint/tutorial framework that teaches players core mechanics and civilization-specific features during gameplay. It operates through a **Goal → GoalSequence** architecture: individual `Training_Goal` objects define single interactive steps (select a unit, click a building, issue a command), and `Training_GoalSequence` objects chain them into multi-step tutorials with trigger predicates, ignore/bypass conditions, regression support, and timer-based activation. The system is modular per-civilization — a core module handles universal controls and economy hints, while civ-specific modules (Abbasid, Chinese, English, French, Mongol, Rus, Sultanate) add unique mechanic tutorials. All hints adapt to three input modes: PC mouse/keyboard, Xbox controller, and Xbox KBM, with separate goal definitions and UI data templates for each.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| coretrainingconditions.scar | core/conditions | Defines universal predicate/condition functions for all training goals (selection, movement, gathering, construction, camera, timers) |
| coretraininggoals.scar | core/goals | Registers core control and economy goal sequences (select, move, gather, build villager/house/farm/landmark, siege setup) for all input modes |
| campaigntraininggoals.scar | training/campaign | Adds campaign-specific training (downed leader recovery, diplomacy panel hints, construction phase tracking) |
| abbasidtrainingconditions.scar | training/civ-conditions | Abbasid-specific conditions: House of Wisdom building, Wing upgrades, Golden Age menu |
| abbasidtraininggoals.scar | training/civ-goals | Abbasid goal sequences: build House of Wisdom, age up via Wings, view Golden Age tiers |
| chinesetrainingconditions.scar | training/civ-conditions | Chinese-specific conditions: Imperial Official tax collection, dynasty creation, pagoda garrisoning, granary farms |
| chinesetraininggoals.scar | training/civ-goals | Chinese goal sequences: tax gold collection, floating tax buildings, dynasty creation |
| englishtrainingconditions.scar | training/civ-conditions | English-specific conditions: Longbow Palings deployment, Setup Camp ability, farm enclosures |
| englishtraininggoals.scar | training/civ-goals | English goal sequences (all currently disabled/commented out) |
| frenchtraininggoals.scar | training/civ-goals | French goal sequences (stub — all goals disabled) |
| mongoltrainingconditions.scar | training/civ-conditions | Mongol-specific conditions: Ovoo construction on stone deposits, depleted Ovoo, Khan death, packed buildings |
| mongoltraininggoals.scar | training/civ-goals | Mongol goal sequences: build Ovoo, Ovoo depleted notification |
| rustrainingconditions.scar | training/civ-conditions | Rus-specific conditions: scout hunting bounty, Hunting Cabin placement, trade cart routing |
| rustraininggoals.scar | training/civ-goals | Rus goal sequences (all currently disabled/commented out) |
| sultanatetrainingconditions.scar | training/civ-conditions | Sultanate-specific conditions: scholar availability, mosque garrison, military building garrison, gristmill |
| sultanatetraininggoals.scar | training/civ-goals | Sultanate goal sequences: low/no scholar upgrades, idle scholar garrison into mosque |

## FUNCTION INDEX

### Core Condition Functions (coretrainingconditions.scar)

| Function | Purpose |
|----------|---------|
| `GetNumGatheringSquadsAny` | Count all resource-gathering squads |
| `GetNumGatheringSquadsFood` | Count food-gathering squads only |
| `FindVillagerInSight` | Find idle villager visible on screen |
| `FindDecorableFoodDepositInSight` | Find food deposit with visible UI decorators |
| `TimeHasPassedWithoutGathering` | Trigger: no food gathering after short interval |
| `TimeHasPassedWithoutBuildingAVillager` | Trigger: TC idle + resources available after moderate interval |
| `TimeHasPassedWithoutBuildingAHouse` | Trigger: pop cap reached + can build house |
| `TimeHasPassedAndUserCanBuildAWonder` | Trigger: landmark affordable + villager visible |
| `TimeHasPassedAndUserCannotBuildAWonder` | Trigger: can't afford landmark yet, show requirements |
| `HasAttachedScoutAndDropOffTownCenter` | Trigger: scout has 3+ sheep + idle + TC exists |
| `ShouldBuildDropOff` | Trigger: wood gatherer far from drop-off + no lumber camp |
| `SuggestBuildFarmCriteriaMet` | Trigger: no farms, no berries nearby, has resources |
| `UserHasSelectedAVillager` | Goal: player selected a villager |
| `UserIsGoingToBuildBuildingType` | Goal: construction modal active for building type |
| `UserHasStartedToBuildABuilding` | Goal: building placement issued for type |
| `OnConstructionPhaseChange` | Callback: tracks construction modal state (placing/issued/cancelled) |
| `OnAbilityPhaseChange` | Callback: tracks ability modal state |
| `OnHoverChange` | Callback: tracks current hover blueprint |
| `UserHasMultipleUnitsOnScreen` | Trigger: 2+ idle military units visible |
| `HasSiegeUnitPredicate` | Trigger: idle siege unit on screen |
| `UserHasRotatedCamera` | Goal: camera orbit changed by ≥10 degrees |
| `SelectNextIdleIfVillagersIdle` | Trigger: idle villagers exist for 60s |

### Core Goal Registration (coretraininggoals.scar)

| Function | Purpose |
|----------|---------|
| `CoreTrainingGoals_OnInit` | Registers all core control + econ goal sequences |
| `CoreTrainingGoals_Start` | Enables goals after intro movies complete |
| `TrainingGoal_EnableCoreControlGoals` | Batch-enable control tutorial goals |
| `TrainingGoal_DisableCoreControlGoals` | Batch-disable control tutorial goals |
| `TrainingGoal_EnableCoreEconGoals` | Batch-enable economy tutorial goals |
| `TrainingGoal_DisableCoreEconGoals` | Batch-disable economy tutorial goals |
| `TrainingGoal_EnableAgeUpGoals` | Batch-enable age-up tutorial goals |
| `TrainingGoal_DisableAgeUpGoals` | Batch-disable age-up tutorial goals |

### Campaign Training (campaigntraininggoals.scar)

| Function | Purpose |
|----------|---------|
| `CampaignTrainingGoals_OnInit` | Defers to CoreTrainingGoals if registered, else sets up standalone |
| `TrainingGoal_AddLeaderRecovery` | Adds downed-leader rescue hint sequence |
| `LeaderDown` | Trigger: any leader squad ownership changed |
| `UserIsMovingToLeader` | Goal: selected unit moving within 12m of downed leader |
| `CampaignTraining_TimeoutIgnorePredicate` | Auto-disables goal after 60-120s timeout |
| `CampaignTraining_AddDiplomacyPanelHint` | Adds console-only diplomacy panel hint |
| `PredicateHelper_HasUserHoveredOverBP` | Checks hover time over blueprint (3s radial / 3s hover) |
| `TrainingContructionCallback` | Alternate construction phase logger for campaigns |
| `IsEntityBeingPlacedOrBuilt` | Check if specific blueprint in active placement |

### Civilization-Specific Functions

| Function | File | Purpose |
|----------|------|---------|
| `AbbasidTrainingGoals_OnInit` | abbasidtraininggoals | Register House of Wisdom, age-up, Golden Age goals |
| `TimeHasPassedWithoutBuildingAHouseOfWisdom` | abbasidtrainingconditions | Trigger: HoW not built + can afford + idle villager |
| `TimeHasPassedAndUserCanAgeUp` | abbasidtrainingconditions | Trigger: HoW exists + can afford Wing upgrade |
| `TimeHasPassedAndUserHasHouseOfWisdom` | abbasidtrainingconditions | Trigger: HoW exists for Golden Age hint |
| `UserHasBegunWingUpgrade` | abbasidtrainingconditions | Goal: Wing upgrade queued in HoW production |
| `ChineseTrainingGoals_OnInit` | chinesetraininggoals | Register tax gold, floating tax, dynasty goals |
| `HasTownCenterNoOfficial` | chinesetrainingconditions | Trigger: TC visible + tax > 50 + no official |
| `UserCanAffordSecondLandmark` | chinesetrainingconditions | Trigger: 1 dark-age wonder built + can afford 2nd |
| `UserHasBuildingWithTooMuchTax` | chinesetrainingconditions | Trigger: building on screen with tax > 70 |
| `MongolTrainingGoals_OnInit` | mongoltraininggoals | Register Ovoo build + depleted sequences |
| `TimeHasPassedWithoutBuildingAnOvoo` | mongoltrainingconditions | Trigger: stone deposit visible + can build Ovoo |
| `OvooHasDepletedAllStone` | mongoltrainingconditions | Trigger: Ovoo's stone deposit empty |
| `SultanateTrainingGoals_OnInit` | sultanatetraininggoals | Register scholar availability goal sequences |
| `HasActiveUpgradeWithLowScholarCount` | sultanatetrainingconditions | Trigger: researching + scholar level 1 |
| `HasActiveUpgradeWithNoScholarCount` | sultanatetrainingconditions | Trigger: researching + scholar level 0 |
| `HasIdleScholarWithMosque` | sultanatetrainingconditions | Trigger: idle scholar + mosque available |

## KEY SYSTEMS

### Training_Goal API Architecture

The system is built on two core data structures created by API functions:

**`Training_Goal(keyType, data, completionFunc)`**
- `keyType`: UI anchor type — `"Squad"`, `"Entity"`, `"PBG"`, `"Cursor"`, `"LooseReticle"`, `"ControlGroupButton1Tag"`, `"PopulationButton"`, `"CommandsCommandCardTab"`, `"EconomicCommandCardTab"`, `"MilitaryCommandCardTab"`, `"XboxAbbasidGoldenAgeWidget"`, `"DiplomacyButton"`, `"RadialDPadLeft"`, `"XboxLandMarkSelectMenuTag"`, `"CenterLeftSecondaryInfo"`, etc.
- `data`: Table with `ID` (debug string), `Message` (localization ID), `DataTemplate` (UI template name)
- `completionFunc`: Function returning `true` when goal is satisfied
- Each goal has a `.key` field dynamically set by the trigger predicate (entity ID, squad ID, blueprint, position, or UI element name)
- Goals have a `.temp` table for transient state and a `.timerID` for per-goal timing

**`Training_GoalSequence(id, repeatMax, remindMax, triggerPred, ignorePred, remindPred, bypassPred, canRegress, goals)`**
- `id`: String identifier (e.g., `"gather"`, `"build_house"`, `"age_up_abb"`)
- `repeatMax`: How many times sequence can repeat (1 = once, -1 = infinite)
- `remindMax`: How many reminders after initial display
- `triggerPred`: Function that returns `true` when sequence should activate; also responsible for setting goal `.key` fields
- `ignorePred`: Function that returns `true` to temporarily hide/cancel sequence (e.g., key entity goes off-screen)
- `remindPred`: Function for reminder activation (usually `nil`)
- `bypassPred`: Function that returns `true` to skip sequence entirely (player already knows this)
- `canRegress`: Boolean — whether sequence can go back to earlier goals
- `goals`: Ordered table of `Training_Goal` objects

**Registration flow:**
1. `Training_AddGoalSequence(sequence)` — registers with engine
2. `Training_EnableGoalSequenceByID(id, bool)` — enable/disable by string ID
3. `Training_EnableGoalSequence(sequence, bool)` — enable/disable by reference
4. `Training_ResetTimers()` — reset all training timers
5. `Training_GetNewTimerID()` — allocate timer for custom delays
6. `Training_InvalidateCurrentTag()` — force UI tag recreation
7. `Training_AddCallbacksToGoal(goal, startCb, completeCb)` — attach lifecycle callbacks

### Goal Sequence Categories

**Core Controls** (`training_goals_core_controls`):
- `single_selection` — select a unit (left-click / press A)
- `move_unit` — move selected unit (right-click / press A on ground)
- `pan_camera` — pan with middle mouse / right stick
- `bandbox_selection` — drag-select multiple military units
- `setup_siege` — setup siege weapon with right-click drag

**Core Economy** (`training_goals_core_econ`):
- `gather` — right-click villager on food resource
- `build_villager` — produce villager from TC
- `build_house` — build house when pop-capped (skipped for Mongol)
- `scout_returns_sheep` — scout drops off herded sheep at TC
- `build_drop_off` — build lumber camp near wood gatherers (skipped for Mongol)
- `goal_next_idle` — use idle villager button
- `goal_build_farm` — build farm near TC/mill (skipped for Mongol)

**Age Up** (`training_goals_age_up`):
- `build_towards_wonder` — view landmark requirements when can't afford
- `build_wonder` — build landmark when affordable (skipped for Abbasid)

### Timer Constants

| Constant | Value | Purpose |
|----------|-------|---------|
| `__t_trainingBriefInterval` | 1s | Minimal delay before hint |
| `__t_trainingShortInterval` | 15s (core), 10s (Mongol) | Short delay triggers |
| `__t_trainingModerateInterval` | 30s | Standard delay for most hints |
| `__t_trainingLongInterval` | 60s | Extended delay for complex hints |
| `__t_trainingWonderInterval` | 15s | Landmark requirements hint delay |
| `__t_trainingHoverInterval` | 3s | Required hover time to "learn" item |
| `__t_trainingRadialInterval` | 5s | Controller radial menu view time |
| `__t_trainingLongDistance` | 50 | Distance threshold for invalidating goals |

### Input Mode Adaptation

Each `*TrainingGoals_OnInit` function branches on three paths:
- **`UI_IsXboxControllerUI()`** — Controller goals use `"LooseReticle"`, `"Squad"` keys, radial menu steps (`UserHasOpenedContextualRadial`, `UI_GetActiveRelicRadialMenuDirection`), and `"GenericTrainingDataTemplate"` / `"RadialTrainingDataTemplate"`
- **`UI_IsXboxKBMUI()`** — Xbox KBM adds command card tab navigation steps (`EconomicCommandCardTab`, `CommandsCommandCardTab`, `MilitaryCommandCardTab`) as intermediate goals
- **PC (default)** — Uses `"Cursor"` key type, `"LeftClickTrainingDataTemplate"` / `"RightClickTrainingDataTemplate"`, fewest goals per sequence

### Data Templates

| Template | Usage |
|----------|-------|
| `GenericTrainingDataTemplate` | Default hint display |
| `LeftClickTrainingDataTemplate` | PC left-click instruction |
| `RightClickTrainingDataTemplate` | PC right-click instruction |
| `PanCameraTrainingDataTemplate` | Camera pan instruction |
| `RadialTrainingDataTemplate` | Controller radial menu instruction |

### Construction Phase Tracking

The system hooks into the game's construction modal via `UI_SetModalConstructionPhaseCallback(OnConstructionPhaseChange)`:
- **TP_Position / TP_Facing** → `training_currentConstructionBlueprint` set (player choosing location)
- **TP_Issued** → `training_previousConstructionBlueprint` set (build command confirmed), current cleared
- **TP_Cancelled** → both cleared

Similarly, `UI_SetModalAbilityPhaseCallback` and `UI_SetModalHoverCallback` track ability targeting and blueprint hovering.

### Civilization-Specific Goal Sequences

| Civ | Sequence ID | Mechanic |
|-----|------------|----------|
| Abbasid | `build_house_of_wisdom` | Build the House of Wisdom landmark |
| Abbasid | `age_up_abb` | Age up via Wing upgrades on HoW |
| Abbasid | `golden_age_abb` | View Golden Age tier requirements |
| Chinese | `tax_gold_chi` | Build Imperial Official from TC when tax accumulates |
| Chinese | `goal_floating_tax_chi` | Select building with excess tax gold (>70) |
| Chinese | `create_dynasty_chi` | Build 2nd landmark to create dynasty |
| Mongol | `build_ovoo` | Build Ovoo on stone deposit |
| Mongol | `ovoo_depleted` | Notification when Ovoo's stone is exhausted |
| Sultanate | `scholar_low_count_upgrade_sul` | Train more scholars when researching (level 1) |
| Sultanate | `scholar_no_count_upgrade_sul` | Train scholars urgently (level 0, research halted) |
| Sultanate | `scholar_idle_sul` | Garrison idle scholar in mosque |
| English | *(all disabled)* | Palings, Setup Camp, Enclosures — commented out |
| French | *(all disabled)* | Pavise, Toggle Resource — stub only |
| Rus | *(all disabled)* | Hunting Bounty, Hunting Cabin — commented out |

### Campaign-Specific Features

- **Leader Recovery**: `TrainingGoal_AddLeaderRecovery()` — detects downed leader via ownership change, prompts moving units within 12m
- **Timeout Ignore**: `CampaignTraining_TimeoutIgnorePredicate` — auto-disables sequences after 60-120s of inactivity
- **Diplomacy Panel**: `CampaignTraining_AddDiplomacyPanelHint` — console-only hint to open diplomacy/tribute panel
- **Infinite Timer**: Uses `__t_trainingInfiniteTimerDuration` for long-running timeout tracking

### Module Registration

All training modules use `Core_RegisterModule()`:
- `CoreTrainingGoals` — universal controls + economy
- `CampaignTrainingGoals` — campaign overlays (defers to Core if registered)
- `AbbasidTrainingGoals`, `ChineseTrainingGoals`, `EnglishTrainingGoals`, `FrenchTrainingGoals`, `MongolTrainingGoals`, `RusTrainingGoals`, `SultanateTrainingGoals`

Each module follows the `{Name}_OnInit` / `{Name}_OnGameOver` pattern. Civ modules gate on `Player_GetRaceName(Game_GetLocalPlayer())` matching their civilization.

### Goal Lifecycle

1. Module `_OnInit` creates goals and sequences, calls `Training_AddGoalSequence`
2. Goals initially disabled; `CoreTrainingGoals_Start` enables after intro
3. Engine polls `triggerPred` — when true, activates sequence and shows first goal's UI tag
4. Engine polls each goal's `completionFunc` — on success, advances `currentGoalIndex`
5. If `canRegress` is true and earlier conditions become unmet, sequence steps back
6. `ignorePred` returning true suspends display (e.g., entity moved offscreen)
7. `bypassPred` returning true completes entire sequence (player already demonstrated skill)
8. After `repeatMax` completions, sequence permanently retires

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| All condition files | `training.scar`, `cardinal.scar` |
| coretraininggoals.scar | `training.scar`, `training/coretrainingconditions.scar` |
| campaigntraininggoals.scar | `training.scar`, `training/coretrainingconditions.scar` |
| abbasidtraininggoals.scar | `training.scar`, `training/abbasidtrainingconditions.scar`, `training/coretraininggoals.scar`, `training/coretrainingconditions.scar` |
| chinesetraininggoals.scar | `training.scar`, `training/chinesetrainingconditions.scar`, `training/coretrainingconditions.scar` |
| mongoltraininggoals.scar | `training.scar`, `training/mongoltrainingconditions.scar` |
| sultanatetraininggoals.scar | `training.scar`, `training/sultanatetrainingconditions.scar`, `training/coretrainingconditions.scar` |

### Shared Globals

- `training_currentConstructionBlueprint` / `training_previousConstructionBlueprint` — active/last construction blueprint
- `training_currentAbilityBlueprint` / `training_previousAbilityBlueprint` — active/last ability blueprint
- `training_currentHoverBlueprint` — currently hovered blueprint
- `sg_currentSelection` / `eg_currentSelection` — reusable selection groups
- `eg_nearbyDeposits` — reusable deposit group
- `eg_allentities` / `sg_allsquads` — player entity/squad collections from `Player_GetAll`
- `t_allLeaders` — campaign leader data table (from campaign scripts)
- `_diplomacy` — diplomacy UI state (from diplomacy system)

### Key API Dependencies (training.scar — not in batch)

- `Training_Goal()`, `Training_GoalSequence()`, `Training_AddGoalSequence()`
- `Training_EnableGoalSequenceByID()`, `Training_EnableGoalSequence()`
- `Training_ResetTimers()`, `Training_GetNewTimerID()`
- `Training_InvalidateCurrentTag()`, `Training_AddCallbacksToGoal()`

### Cardinal System Dependencies

- `Cardinal_ConvertTypeToEntityBlueprint()` / `Cardinal_ConvertTypeToSquadBlueprint()` — type-string to blueprint resolution
- `Core_RegisterModule()` / `Core_UnregisterModule()` / `Core_IsModuleRegistered()`

### Inter-File Function Usage

- Civ condition files call core condition functions: `UserIsGoingToBuildBuildingType()`, `UserHasStartedToBuildABuilding()`, `FindVillagerInSight()`, `UserHasSelectedAVillager()`
- `mongoltrainingconditions.scar` redefines `OnConstructionPhaseChange` (slightly different logic — no separate issued/cancelled clearing)
- `campaigntraininggoals.scar` defers entirely to `CoreTrainingGoals` when that module is registered
