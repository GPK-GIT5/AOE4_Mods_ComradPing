# Angevin Chapter 4: Rochester

## OVERVIEW

Rochester is a siege mission where King John's Royalists (player1, English) must first capture the village of Chatham, then besiege and destroy the Barons' Rebels (player2) fortified Rochester Keep. The mission flows in two phases: an early village-capture objective that grants the player a base with villagers and economy, followed by a prolonged siege against a walled castle defended by dynamically-spawned RovingArmy modules. Side objectives to destroy enemy farms and trade carts trigger a "siege entropy" mechanic where 20% of AI defenders surrender and walk off-map, weakening the garrison. On Easy/Normal, an optional siege tutorial guides the player to age up, build a Siege Workshop, and construct trebuchets. Tutorial hints teach healing, holy sites, market construction, buy/sell, and trade.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp4_rochester_recipe.scar` | data | Defines mission recipe: locations, RovingArmy defender modules, dynamic marker-based garrison generation, title card, and campaign metadata. |
| `ang_chp4_rochester.scar` | core | Main mission script: player setup, difficulty tuning, restrictions, attack wave logic, siege counter-attack AI, surrender entropy, narrative/audio functions. |
| `obj_capturevillage.scar` | objectives | Capture Chatham village objective with location capture, rebel defeat, and village repopulation on completion. |
| `obj_destroyrochester.scar` | objectives | Primary objective to destroy Rochester Keep; triggers wall-breach events and mission completion at ≤15% keep health. |
| `obj_siegetutorial.scar` | objectives | Optional siege tutorial: age up → build Siege Workshop → construct 3 trebuchets (Easy/Normal only). |
| `obj_stopeconomy.scar` | objectives | Optional supply-cut objectives: burn farms (counter-tracked) and destroy 6 trade carts to trigger entropy surrenders. |
| `training_rochester.scar` | training | Tutorial goal sequences for monk healing, holy site capture, market construction, buy/sell resources, produce/assign traders. Xbox controller variants included. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `GetRecipe()` | recipe | Builds mission recipe with modules and dynamic defenders |
| `Mission_SetupPlayers()` | core | Configures 4 players, ages, relationships, colours |
| `Mission_SetDifficulty()` | core | Sets t_difficulty table via Util_DifVar |
| `Mission_SetRestrictions()` | core | Removes gunpowder units/upgrades from player1 |
| `Mission_Preset()` | core | Wall setup, upgrades, objective init, music, prefabs |
| `Mission_Start()` | core | Starts objectives, defenders, trade tracking, fishing |
| `Init_AttackWaves()` | core | Creates RovingArmy attack wave with Wave system |
| `ConstructWave()` | core | Builds dynamic wave composition scaling with game time |
| `QueueAttackWaves()` | core | Queues next wave after random downtime delay |
| `PrepAttackWaves()` | core | Resets wave module and prepares new unit batch |
| `SendPoke()` | core | Sends early probing attacks on timer |
| `DefendCountryside()` | core | Spawns cavalry patrol for farmland defense |
| `DefendTraderoute()` | core | Spawns cavalry patrol for trade route defense |
| `Init_EnemyTrade()` | core | Creates escalating trade cart convoys with escorts |
| `Init_DefendRochester()` | core | Initializes siege counter-attack RovingArmy module |
| `BesiegeRochester_EntityKilled()` | core | Handles outer wall breach: intel, wall-hole defense |
| `InnerRochester_EntityKilled()` | core | Handles inner wall breach: intel, repositioning |
| `SiegeCounter_OnDamageReceived()` | core | Tracks wall attackers for counter-siege response |
| `CounterSiegeHunt()` | core | Directs siege counter units at nearest wall attacker |
| `Init_FallenWallDefense()` | core | Pre-positions large garrison at breach point |
| `PushAttack()` | core | Sends nearest defenders to intercept player inside walls |
| `CounterMonks()` | core | Spawns monk+escort army to recapture holy sites |
| `SiegeEntropy()` | core | Makes 20% of AI forces surrender and leave map |
| `EntropyCTA()` | core | Fires call-to-action event cue for surrendering troops |
| `Delay_Detection()` | core | Disables auto-targeting until player selects units |
| `SetupOutro()` | core | Spawns parade units, disables keep weapons for outro |
| `CaptureVillage_InitObjectives()` | obj_capture | Registers village capture objectives |
| `CaptureVillage_PreComplete()` | obj_capture | Converts village, spawns villagers, monk counter timer |
| `CaptureVillage_OnComplete()` | obj_capture | Starts tutorials, attack waves, supply objectives |
| `VillageRepopulate()` | obj_capture | Deploys villagers assigned to food/wood/stone/gold |
| `DestroyRochester_InitObjectives()` | obj_destroy | Registers keep destruction objective |
| `DestroyRochester_PreStart()` | obj_destroy | Adds wall-kill and damage-received event listeners |
| `DestroyRochester_IsComplete()` | obj_destroy | Completes when keep health ≤ 15% |
| `SiegeTut_InitObjectives()` | obj_siege | Registers age-up, workshop, trebuchet sub-objectives |
| `Trebuchets_IsComplete()` | obj_siege | Tracks trebuchet count with counter UI (target: 3) |
| `RochesterSupply_InitObjectives()` | obj_economy | Registers farm and trade cart sub-objectives |
| `RochesterSupply_Init()` | obj_economy | Starts enemy trade and discovery monitoring rules |
| `DiscoverFarms()` | obj_economy | Triggers farm objective when player sees farm egroup |
| `DiscoverWagons()` | obj_economy | Triggers trade objective when player sees wagons |
| `WagonKilled_SquadKilled()` | obj_economy | Counts cart kills (6 to complete), spawns replacements |
| `RochesterSupply_Update()` | obj_economy | Updates farm destruction counter, triggers cavalry patrol |
| `StMargaretsMonitor()` | obj_economy | Reveals monastery/market hintpoints on discovery |
| `Rochester_Tutorials_Init()` | training | Initializes all tutorial goal sequences |
| `MissionTutorial_Healing()` | training | Healing tutorial: select monk → use heal → target wounded |
| `MissionTutorial_HolySite()` | training | Holy site tutorial: select monk → move to site |
| `MissionTutorial_Market()` | training | Market build tutorial: select villager → build market |
| `MissionTutorial_BuySell()` | training | Buy/sell tutorial: select market → hover resource ability |
| `MissionTutorial_ProduceTrader()` | training | Produce trader tutorial: select market → train trader |
| `MissionTutorial_AssignTrader()` | training | Assign trader tutorial: select trader → right-click settlement |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_CaptureVillage` | Primary | Capture the village of Chatham from rebels |
| `SOBJ_DefeatHamletRebels` | Sub | Defeat Chatham garrison defenders |
| `SOBJ_LocationHamlet` | Sub | Location capture tracker for Chatham |
| `OBJ_DestroyRochester` | Primary | Destroy Rochester Keep (health ≤ 15%) |
| `OBJ_RochesterSupply` | Optional | Cut off Rochester's supply lines |
| `SOBJ_FlamingFarms` | Sub | Burn all Rochester farms (counter-tracked) |
| `SOBJ_TroubledTrade` | Sub | Destroy 6 enemy trade carts |
| `OBJ_SiegeTut` | Optional | Build trebuchets to breach Rochester (Easy/Normal only) |
| `SOBJ_AgeUp` | Sub | Build a Landmark to age up |
| `SOBJ_SiegeWorkshop` | Sub | Build a Siege Workshop |
| `SOBJ_Trebuchets` | Sub | Construct 3 trebuchets (counter: 0/3) |
| `OBJ_DebugComplete` | Debug | Kills outro entities and completes mission |

### Difficulty

All values indexed by `{Story, Easy, Normal, Hard}`:

| Parameter | Values | Effect |
|-----------|--------|--------|
| `defenderValue` | {1, 1, 1.15, 1.25} | Multiplier on all defender squad counts across all RovingArmy modules |
| `baseWaveValue` | {5, 5, 5, 10} | Base size for attack waves |
| `easyWaveMod` | {0, 0, 1, 1} | Additional wave modifier |
| `waveDownTimeMin` | {180, 120, 0, 0} | Minimum seconds between attack waves |
| `waveDownTimeMax` | {180, 120, 60, 30} | Maximum seconds between attack waves (randomized) |
| `earlyPokes` | {2, 2, 3, 5} | Number of early probing attacks sent |
| `pokeTimer` | {3, 3, 4, 5} | Minutes between poke attacks |

Additional difficulty-scaled values:
- `VillageRepopulate()` gives extra wood villagers on Story (+6) vs other difficulties (+4), extra stone/gold villagers on Story (+1 each).
- `ConstructWave()` applies `Util_DifVar` to wave resource budget: Story/Easy capped at 15, Hard gets 1.5× multiplier.
- Attack waves only start on Normal+ difficulty; Story mode skips `Init_AttackWaves()` and `SendPoke()`.
- Siege tutorial (`OBJ_SiegeTut`) only starts on Easy/Normal.

### Spawns

**Static Defenders (Recipe):**
- 3 named RovingArmy modules: DefendVillage (spearman + archer × defenderValue), DefendRochester (crossbowman × defenderValue), DefendKeep (men-at-arms + knight + crossbowman × defenderValue).
- Dynamic marker-based defenders generated via `AllMarkers_FromName()`:
  - `mkr_wall_archer` → archer ×4 per marker
  - `mkr_infantry_defender` → spearman ×8 + 1 men-at-arms per marker
  - `mkr_elite_defender` → men-at-arms ×7 + crossbowman ×5 per marker
  - `mkr_cavalry_defender` → horseman ×6 + 1 knight per marker
  - `mkr_siege_defender` → 4 men-at-arms + 1 springald per marker
- All dynamic defenders use `onDeathDissolve = true` (don't respawn).

**Attack Waves:**
- `ConstructWave()` uses a time-based power formula: `wavePower = (gameTime/4) + (gameTime^6 / 10^9)` capped at 66 after 60 minutes.
- Unit pool: archer, horseman, men-at-arms, crossbowman, knight, ram, mangonel — pool shrinks over time as cheaper units removed.
- Unit costs: mangonel=4, ram=3, knight/crossbowman=2, others=1. Spearmen fill remaining budget (+4 base).
- Spawns from `mkr_rochester_keep_spawn`, targets Chatham and Rochester.

**Poke Waves:**
- Early harassment: spearman (5+i), 5 men-at-arms, 3 horsemen per poke.
- Sent every `pokeTimer` minutes, up to `earlyPokes` count.

**Wall Breach Defenders:**
- `WallHoleDefense`: 8× men-at-arms, 16× spearman, 16× archer (all × defenderValue).
- Repositions to breach point dynamically.

**Siege Counter:**
- `SiegeCounter`: 1 knight, 9 horsemen, 12 spearmen, 10 archers, 5 crossbowmen (× defenderValue).
- Reactively hunts player units damaging walls.

**Enemy Trade:**
- Escalating escort strength: rounds 1-2 (2 horsemen), 3-4 (8 horsemen), 5+ (12 horsemen + 2 knights).
- Each convoy includes 1 supply cart.

### AI

- No `AI_Enable()` calls — all AI behavior is scripted via RovingArmy modules and event-driven rules.
- **Counter-siege**: `SiegeCounter_OnDamageReceived` tracks attackers hitting walls → `CounterSiegeHunt` sends siege counter force to nearest attacker.
- **Holy site counter**: `CounterMonks()` spawns monk + escort army every 480s to recapture player-held holy sites.
- **Countryside/trade patrol**: `DefendCountryside()` and `DefendTraderoute()` activate when player destroys farms or trade carts (triggered at ≤3 farms or first cart kill).
- **PushAttack**: Every 30s after wall breach, finds closest defender module to player units inside Rochester and redirects them.
- **Siege entropy**: On side objective completion, 20% of non-critical AI units transfer to player4 (ally) and walk off-map. Reduces `i_entropyImpact` by 0.8× for future waves.
- **Detection delay**: `Delay_Detection()` disables auto-targeting until player first selects units (narrative control).
- Outposts upgraded with arrow slits; towers upgraded with springalds at mission start.
- `Wave_OverrideBuildingSpawnType("castle", {...})` enables castle-based spawning for infantry, ranged, cavalry, siege, TC, religious.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `SendPoke` | OneShot, `60 × pokeTimer` (180-300s) | Sends early harassment waves, recurses up to earlyPokes count |
| `QueueAttackWaves` → `PrepAttackWaves` | OneShot, `Rand(waveDownTimeMin, waveDownTimeMax)` | Delays between attack waves (0-180s depending on difficulty) |
| `CounterMonks` | Interval, 480s | Spawns monk recapture force every 8 minutes |
| `PushAttack` | Interval, 30s | Redirects defenders at player units inside walls (post-breach) |
| `KeepReveal` | Interval, 1s | Checks if player units are near keep to reveal FOW |
| `AttackWave_Intel` | Interval, 1s | Checks if player can see attack wave to trigger intel event |
| `DiscoverFarms` | Interval, 1s | Monitors if player sees farm egroup to start objective |
| `DiscoverWagons` | Interval, 1s | Monitors if player sees trade wagons to start objective |
| `RochesterSupply_Update` | Interval, 0.5s | Updates farm destruction counter and UI |
| `StMargaretsMonitor` | Interval, 2s (0.5s delay) | Detects player discovering St Margaret's monastery |
| `Rochester_Tutorials_Init` | OneShot, 30s | Initializes tutorial sequences after village capture |
| `Cycle_Fish` | Interval, 30s | Restocks shore fish to 2000 resources |
| `SurrenderEnsure` | Interval, 5s | Ensures surrendered units continue moving off-map |
| `Init_EnemyTrade` (2nd) | OneShot, 35s | Spawns second trade convoy shortly after first |
| `CounterSiegeHunt` | Interval, 1s | Directs siege counter to wall attackers (event-driven start) |
| `Reset_Detection` | Interval, 1s | Re-enables auto-targeting after player selects units |
| `_Hint_SiegeSetup` | Interval, 3s | Shows trebuchet setup hint when player selects one |
| `_RemoveHint_SiegeSetup` | OneShot, 12s | Removes siege setup hintpoint |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Cardinal campaign framework (provides `MissionOMatic_FindModule`, `Prefab_DoAction`, `RovingArmy_*`, `Wave_*`, `Location_*`, `Objective_*`, etc.)
- `training/campaigntraininggoals.scar` — Shared training system (`Training_Goal`, `Training_GoalSequence`, `Training_AddGoalSequence`, `CampaignTraining_TimeoutIgnorePredicate`)
- `obj_capturevillage.scar`, `obj_destroyrochester.scar`, `obj_stopeconomy.scar`, `obj_siegetutorial.scar` — Objective modules imported by core
- `training_rochester.scar` — Training module imported by core

### Shared Globals
- `t_difficulty` — Difficulty table used across all files for scaling
- `t_allRochesterRecipeModNames` / `t_allRochesterModules` — Lists of dynamic defender module names/references, populated in recipe, consumed in core
- `sg_trade_wagons` — Trade cart sgroup shared between core (`Init_EnemyTrade`) and economy objectives (`WagonKilled_SquadKilled`)
- `sg_attack_wave` / `sg_attack_poke` — Attack wave sgroups used in core and referenced in intel checks
- `eg_rochester_walls` / `eg_rochester_walls_notowers` / `eg_rochester_innerwalls` — Wall egroups set up in `Mission_Preset`, consumed in destroy objective events
- `eg_rochestersupply` — Farm egroup tracked in economy objective
- `eg_holysites` — Holy site egroup used in training (holy site tutorial) and core (`CounterMonks`)
- `b_WallsBreached` — Boolean flag set by wall-kill events, checked in supply objective completion logic
- `i_entropyImpact` — Entropy multiplier reducing wave strength after surrenders (starts at 1, ×0.8 per entropy event)
- `wave` — Global Wave object created in `Init_AttackWaves`, updated in `PrepAttackWaves`

### Inter-File Function Calls
- Core calls: `DestroyRochester_InitObjectives()`, `CaptureVillage_InitObjectives()`, `RochesterSupply_InitObjectives()`, `SiegeTut_InitObjectives()`, `Rochester_Tutorials_Init()`
- `CaptureVillage_OnComplete()` calls `Init_AttackWaves()`, `SendPoke()`, `RochesterSupply_Init()`, triggers `Rochester_Tutorials_Init` via OneShot
- `RochesterSupply_EntropyIfFirst()` calls `SiegeEntropy()` (core) on first sub-objective completion
- `OBJ_RochesterSupply.OnComplete` directly references `SiegeEntropy` function
- `BesiegeRochester_EntityKilled()` and `InnerRochester_EntityKilled()` call `Halt_ExtraActivities()` which stops trade objective monitoring
- `DestroyRochester_OnComplete()` calls `Mission_Complete()`; fail handlers call `Mission_Fail()`

### Blueprint References
- `SBP.ENGLISH.UNIT_MANATARMS_2_ENG` — Player starting men-at-arms
- `EBP.ENGLISH.BUILDING_ECON_MARKET_CONTROL_ENG` — Market (training tutorials)
- `EBP.ENGLISH.BUILDING_UNIT_SIEGE_CONTROL_ENG` — Siege Workshop (siege tutorial)
- `SBP.ENGLISH.UNIT_TRADE_CART_ENG` — Trade cart production check
- `BP_GetAbilityBlueprint("monk_heal_target")` — Healing ability for tutorial
- `UPG.COMMON.UPGRADE_OUTPOST_ARROWSLITS` — Applied to all player2 outposts at start
- `UPG.COMMON.UPGRADE_TOWER_SPRINGALD` — Applied to all player2 towers at start
- Various gunpowder upgrades/units removed from player1 via `ITEM_REMOVED`
