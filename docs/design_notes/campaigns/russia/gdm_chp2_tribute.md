# Russia Chapter 2: Tribute

## OVERVIEW

Tribute (Moscow 1375) is a Russian campaign economic/defense mission. The player (Muscovites, Feudal Age) must pay recurring gold tribute to the Mongols on a timed cycle (7.5 minutes per cycle) while building an economic engine through trade routes with nearby settlements. Gold is earned by sending trade carts to settlements scattered across the map; once enough trade has been conducted with a settlement, the player can purchase it via a custom UI panel to gain passive gold income. Bandits roam the map in dynamically-scaled groups that threaten trade routes, with optional bandit camp destruction objectives. Victory requires purchasing a difficulty-scaled number of settlements (3–5); failure occurs if the Mongol tribute timer expires without payment (triggering a massive punitive Mongol army) or if all important buildings are destroyed. The mission features a heavily customized diplomacy/tribute UI with an integrated "Buy Settlements" panel.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp2_tribute.scar` | core | Main mission setup: 4 players, recipe, difficulty, intro/outro, unit spawning, atmosphere cycling |
| `diplomacy_tribute.scar` | other | Customized diplomacy and tribute UI system with WPF XAML, Buy Settlements panel, Xbox support |
| `obj_collecttaxes.scar` | objectives | Collect taxes objective, settlement discovery system, bandit spawning/AI via RovingArmy modules |
| `obj_paythemongols.scar` | objectives | Recurring Mongol tribute payment cycles, timer, auto-pay system, punitive Mongol army on failure |
| `obj_buysettlements.scar` | objectives | Settlement purchasing logic, trade tracking, income collection, custom UI data updates |
| `obj_banditcamps.scar` | objectives | Optional objective: discover and destroy randomly-selected bandit camps with Defend modules |
| `obj_buildcabins.scar` | objectives | Optional objective (Easy/Normal): build 3 Hunting Cabins near forests for gold income |
| `training_tribute.scar` | training | Tutorial goal sequences for Dmitry ability, tribute menu, market usage, trader production, settlement defense |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_OnGameSetup` | gdm_chp2_tribute | Set up 4 players with display names |
| `Mission_SetupPlayers` | gdm_chp2_tribute | Configure ages, relationships, colours, upgrades, disable AI for player4 |
| `Mission_SetupVariables` | gdm_chp2_tribute | Initialize SGroups, leader, atmosphere, call all objective inits |
| `Mission_SetDifficulty` | gdm_chp2_tribute | Define all Util_DifVar difficulty parameters |
| `Mission_Preset` | gdm_chp2_tribute | Complete upgrades, assign villagers, mark starting settlements, spawn fort garrisons |
| `Mission_Start` | gdm_chp2_tribute | Start PayTheMongols, configure diplomacy UI, start Buy Settlements panel updates |
| `Mission_Start_PartB` | gdm_chp2_tribute | Start CollectTaxes and tip objectives, trigger cabin objective after 60s |
| `GetRecipe` | gdm_chp2_tribute | Define recipe: NIS, audio, title card, unit spawner modules |
| `Mission_CheckForFail` | gdm_chp2_tribute | Fail mission if all important buildings destroyed |
| `Mission_AdjustPlayerMaxPopCap` | gdm_chp2_tribute | Modify player max pop cap with tracked Modifier system |
| `Mission_PrepareForOutro` | gdm_chp2_tribute | Spawn static outro units and cavalry parade |
| `Mission_OnTributeSent` | gdm_chp2_tribute | Track gold sent to Mongols via tribute system |
| `Tribute_FancyAtmosphere` | gdm_chp2_tribute | Cycle day/sunset/evening atmospheres on timer |
| `Diplomacy_DiplomacyEnabled` | diplomacy_tribute | Initialize full diplomacy data context and state |
| `Diplomacy_CreateUI` | diplomacy_tribute | Build WPF XAML UI for tribute panel and buy settlements |
| `Diplomacy_UpdateDataContext` | diplomacy_tribute | Refresh all tribute enabled/visibility/resource states |
| `Diplomacy_OverrideSettings` | diplomacy_tribute | Override tribute enabled, subtotal, score, team visibility |
| `Diplomacy_OverridePlayerSettings` | diplomacy_tribute | Override per-player visibility and per-resource enabled states |
| `Diplomacy_SendTributeNtw` | diplomacy_tribute | Network callback: transfer resources, apply tax, show cues |
| `Diplomacy_AddTribute` | diplomacy_tribute | Increment/decrement tribute allotment with capacity checks |
| `Diplomacy_SetTaxRate` | diplomacy_tribute | Set tribute tax rate (set to 0% for this mission) |
| `CollectTaxes_Start` | obj_collecttaxes | Start bandit system, settlement discovery monitoring |
| `CollectTaxes_DiscoverNewSettlements` | obj_collecttaxes | Check player FOW visibility of unseen settlements, add hints |
| `CollectTaxes_MarkSettlementAsSeen` | obj_collecttaxes | Add hintpoint, reveal area, track discovery order |
| `CollectTaxes_MonitorBanditsSpotted` | obj_collecttaxes | Start SOBJ_Bandits when player first sees enemy units |
| `CollectTaxes_TriggerTraderHint` | obj_collecttaxes | Show hint to build traders if none built after 13 min |
| `Bandits_Init` | obj_collecttaxes | Set up 7 settlement zones + wanderer zone, strength tables, loadouts |
| `Bandits_Start` | obj_collecttaxes | Start monitor, pause, and extra marker rules |
| `Bandits_Monitor` | obj_collecttaxes | Per-zone: compare desired vs actual groups, create or retire bandits |
| `Bandits_CreateNewGroup` | obj_collecttaxes | Spawn RovingArmy bandit group at chosen edge spawn location |
| `Bandits_PauseWhileCombatIsHappening` | obj_collecttaxes | Pause non-combat zones during fights, release after timer |
| `Bandits_GetDesiredBanditData` | obj_collecttaxes | Calculate strength level and group count for zone |
| `Bandits_ChooseLoadout` | obj_collecttaxes | Select unit composition, preferring unused loadouts |
| `Bandits_ChooseSpawnLocation` | obj_collecttaxes | Pick edge spawn nearest to destination, away from player |
| `Bandits_AddExtraWandererMarkers` | obj_collecttaxes | Expand wanderer patrol area as settlements are purchased |
| `PayTheMongols_StartObjective` | obj_paythemongols | Calculate demand, start payment cycle, queue next cycle |
| `PayTheMongols_Monitor` | obj_paythemongols | Check payment status, show warnings, trigger grace period |
| `PayTheMongols_AttemptAutoPay` | obj_paythemongols | Auto-deduct gold if player has enough when timer expires |
| `MongolArmy_Start` | obj_paythemongols | Trigger punitive Mongol attack on payment failure |
| `MongolArmy_Spawn` | obj_paythemongols | Spawn RovingArmy wave targeting town center from hidden position |
| `MongolArmy_Finish` | obj_paythemongols | Fail the mission after all waves spawned |
| `BuySettlements_Start` | obj_buysettlements | Start buy objective, swap tip objective |
| `BuySettlements_OnTradeEvent` | obj_buysettlements | Track gold received per settlement from GE_TradeRouteCompleted |
| `BuySettlements_Monitor` | obj_buysettlements | Track trade carts, manage threat arrows for carts under attack |
| `BuySettlements_Purchase` | obj_buysettlements | Buy settlement: charge gold, replace TC, spawn villagers/towers, check win |
| `BuySettlements_CollectIncome` | obj_buysettlements | Pay passive gold income from purchased settlements every 6s |
| `BuySettlements_FindSettlement` | obj_buysettlements | Look up settlement data by entity, ID, or string |
| `UI_BuySettlementsPanel_UpdateData` | obj_buysettlements | Refresh Buy Settlements panel UI data every 1s |
| `UI_BuySettlementsPanel_BuyButtonCallback` | obj_buysettlements | Handle buy button click from UI |
| `BanditCamps_Init` | obj_banditcamps | Randomly select camps, create Defend modules, spawn defenders |
| `BanditCamps_Monitor` | obj_banditcamps | Detect camp visibility and destruction, update counter, drop gold pickup |
| `BanditCamps_CampEntityDestroyed` | obj_banditcamps | Spawn gold resource pickup when camp tent destroyed |
| `BuildCabins_TriggerObjective` | obj_buildcabins | Start cabin objective on Easy/Normal only |
| `BuildCabins_Monitor` | obj_buildcabins | Detect new hunting cabins, check if near trees |
| `BuildCabins_NewCabinBuilt` | obj_buildcabins | Validate cabin placement, show feedback tag, update counter |
| `MissionTutorial_AddHintToDmitry` | training_tribute | Training sequence: select Dmitry, view healing ability |
| `MissionTutorial_AddHintToPayMongols` | training_tribute | Training: open diplomacy menu to pay tribute |
| `MissionTutorial_AddHintToBuySettlements` | training_tribute | Training: open diplomacy menu to buy settlements |
| `MissionTutorial_AddHintToBuildTraders` | training_tribute | Training: select market, produce trade cart |
| `MissionTutorial_AddHintToUseMarket` | training_tribute | Training: select market, sell resources for gold |
| `MissionTutorial_AddHintToBuildDefencesAroundSettlement` | training_tribute | Training: build palisades/forts near new settlement |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_PayTheMongols` | Primary | Pay gold tribute to Mongols within 7.5-minute timer |
| `SOBJ_PayTheMongols_GoldAmount` | Primary (sub) | Counter showing gold paid vs gold demanded |
| `OBJ_CollectTaxes` | Primary | Collect taxes from neighboring settlements via trade |
| `SOBJ_MaintainTradeRoutes` | Primary (sub) | Maintain trade routes with settlements |
| `SOBJ_Bandits` | Primary (sub) | Protect trade routes from bandits (starts when first spotted) |
| `OBJ_BuySettlements` | Primary | Buy N settlements to expand Moscow (victory condition) |
| `SOBJ_FindMoreSettlements` | Primary (sub) | Find more settlements if all discovered ones are purchased |
| `OBJ_BanditCamps` | Optional | Destroy randomly-selected bandit camps (counter: destroyed/total) |
| `OBJ_BuildCabins` | Optional | Build 3 Hunting Cabins near forests (Easy/Normal only) |
| `OBJ_TipTradeRouteLengths` | Tip | Longer trade routes generate more gold per trip |
| `OBJ_TipManageGold` | Tip | Manage gold for both settlements and Mongol payments |
| `OBJ_DebugComplete` | Primary (hidden) | Debug cheat: instantly complete mission |

### Difficulty

| Parameter | Easy | Normal | Hard | Expert | What It Scales |
|-----------|------|--------|------|--------|----------------|
| `bandits_GlobalCreationFrequency` | 45 | 35 | 30 | 25 | Seconds between any new bandit group globally |
| `bandits_ZoneCreationFrequency` | 90 | 90 | 75 | 55 | Seconds per zone between bandit spawns |
| `bandits_CreationFrequency_CampBonus` | 10 | 10 | 10 | 10 | Added delay per destroyed camp |
| `bandits_PauseReleaseTimer` | 25 | 25 | 15 | 15 | Seconds after combat before paused bandits resume |
| `bandits_SettlementsModifier` | -1 | 0 | 1 | 2 | Modifier to settlement "value" for bandit strength |
| `bandits_WanderersModifier` | -2 | -1 | 0 | 1 | Extra wandering bandit groups |
| `bandits_NumCamps` | 6 | 6 | 6 | 6 | Number of bandit camps placed |
| `bandits_CampDestructionBonusModifier` | -2 | -1 | -1 | -1 | Strength reduction after destroying a camp |
| `bandits_CampDestructionBonusPeriod` | 150 | 150 | 120 | 90 | Duration of camp destruction bonus (seconds) |
| `payTheMongols_BaseAmount` | 1300 | 1300 | 1500 | 1700 | Initial Mongol gold demand |
| `payTheMongols_ExtraAmountPerCycle` | 100 | 200 | 200 | 300 | Extra gold per cycle (from cycle 3+) |
| `buySettlements_TradeAmountNeededToBuy` | 500 | 500 | 750 | 1000 | Gold earned from trade before purchase unlocks |
| `buySettlements_PurchasePrice` | 300 | 300 | 500 | 700 | Gold cost to purchase a settlement |
| `buySettlements_NumSettlementsNeeded` | 3 | 3 | 4 | 5 | Settlements required for victory |
| `findSettlements_NearbyDistance` | 125 | 125 | 75 | 0 | Proximity hint radius for undiscovered settlements |

Additional difficulty scaling in unit compositions:
- Bandit loadouts (Strength1–5) scale squad counts per `Util_DifVar`
- Starting villagers at town center: Easy gets 4, others get 2
- Easy gets +500 starting gold
- Bandit camp defenders: 7 spearmen base; Hard/Expert add +3 spearmen +4 archers; Expert adds +2 more spearmen +8 archers

### Spawns

**Bandit system** — dynamic, zone-based roaming patrols:
- **7 settlement zones** (one per settlement) + **1 wanderer zone** covering the whole map
- Each zone maintains a target number of bandit groups based on a **strength threshold** system
- Settlement zone thresholds scale with: active trade carts + settlements bought + difficulty modifier + payment cycle escalation
- Wanderer thresholds scale with: settlements purchased + payment cycle
- **10 strength levels** for settlements (0–9 threshold, 1–4 groups) and **11 for wanderers** (-4 to 6, 3–11 groups)
- **5 loadout tiers** (Strength1–5), each with 3 random composition variants using spearmen, archers, horsemen
- Groups spawn as `RovingArmy` modules with `ARMY_TARGETING_RANDOM_MEANDERING` at edge spawn markers (18 spawn points)
- Creation is throttled globally and per-zone with configurable delays
- **Combat pause**: when player engages bandits, all other zones pause and resume after a configurable delay
- Post-purchase: settlement zones gain extra patrol markers; creation delay doubles
- Bandit camp destruction temporarily reduces zone strength via `i_banditCampBonus_QuietModifier`

**Bandit camps** — static defense encounters:
- 11 potential camp locations; 6 randomly selected per session
- Each camp gets a `Defend` module with 7+ spearmen (scaling with difficulty)
- Nearby camps are culled to ensure spread; unused camps are destroyed
- Destroying a camp drops a gold resource pickup and removes it as a bandit spawn point

**Mongol punitive army** (on payment failure):
- 12 attack waves of player3 (Mongol) units spawned 2.5s apart
- Wave 1: Khan ×1, Knight ×8, HorseArcher ×15
- Waves 2–12: alternating compositions of 15 squads each (spearman/archer, horseman/horsearcher, knight/spearman mixes)
- All use `RovingArmy` targeting `mkr_common_town_center` with `attackMoveStyle_normal` or `attackMoveStyle_aggressive`
- Spawns at farthest edge spawn points from player, preferring hidden FOW positions
- Mission fails 20s after last wave spawns

**Initial unit spawning** (via recipe UnitSpawner):
- 2 trade carts (pre-assigned to settlements 2 and 7)
- 12 villagers at resource points (food/wood)
- Prince Dmitry + scout + 2 horsemen + 6 spearmen + 4 archers + 2–4 villagers in Moscow
- Gate guards: spearmen and archers at 4 outer gates
- 1 spearman garrisoned in each wooden fort

### AI

- `AI_Enable(player4, false)` — disables AI for Dmitry's downed-state holder player
- `PlayerUpgrades_Auto` enabled for all 4 players
- Bandits (player2) and Mongols (player3) are allied to ignore each other
- No standard AI plans — all combat behavior driven by `RovingArmy` and `Defend` prefab modules
- Bandit `RovingArmy` modules use `ARMY_TARGETING_RANDOM_MEANDERING` for patrol behavior
- Mongol punitive army uses `RovingArmy` with direct targeting at town center

### Timers

| Timer/Rule | Delay/Interval | Purpose |
|------------|---------------|---------|
| `PayTheMongols_StartObjective` (OneShot, recurring) | 9 min (7.5 + 1.5) | Start next Mongol payment cycle |
| `PayTheMongols_Monitor` (Interval) | 0.25s | Check payment progress, warnings at 60s, auto-pay at 0s |
| `PAYMONGOLS_TIMELIMIT` | 7.5 min | Payment countdown timer per cycle |
| `PAYMONGOLS_GRACEPERIOD` | 25s | Grace period after timer expires before failure |
| `PAYMONGOLS_TIMEBETWEENCYCLES` | 1.5 min | Gap between payment cycles |
| `Bandits_Monitor` (Interval) | 1s | Check all zones, create/retire bandit groups |
| `Bandits_PauseWhileCombatIsHappening` (Interval) | 1s | Pause/unpause bandit zones during combat |
| `Bandits_AddExtraWandererMarkers` (Interval) | 5s | Expand wanderer patrol area based on purchases |
| `BanditCamps_Monitor` (Interval) | 1s | Check camp visibility and destruction |
| `BuySettlements_Monitor` (Interval) | 0.5s | Track all trade carts, manage threat arrows |
| `BuySettlements_CollectIncome` (Interval) | 6s | Distribute passive gold from purchased settlements |
| `UI_BuySettlementsPanel_UpdateData` (Interval) | 1s | Refresh settlement UI panel data |
| `CollectTaxes_DiscoverNewSettlements` (Interval) | 1s | Check for newly visible settlements |
| `CollectTaxes_MonitorBanditsSpotted` (Interval) | 1s | Detect first bandit sighting |
| `CollectTaxes_NewSettlementsIntro` (OneShot) | 15s | Trigger settlement search intel event |
| `CollectTaxes_RemindPlayerToSearchForSettlements` (OneShot) | 4 min | Hint if no new settlements found |
| `CollectTaxes_TriggerTraderHint` (OneShot) | 13 min | Hint to build traders if none built |
| `BuildCabins_TriggerObjective` (OneShot) | 60s | Start cabin objective (Easy/Normal only) |
| `BuildCabins_Monitor` (Interval) | 1s | Detect new hunting cabins |
| `Mission_CheckForFail` (Interval) | 1s | Check if important buildings destroyed |
| `Mission_Start_PartB` (OneShot) | 10s | Start CollectTaxes and tips after intro |
| `Tribute_FancyAtmosphere` (OneShot, recurring) | 60s stable + 300s transition | Cycle through day/sunset/evening atmospheres |
| `MongolArmy_Spawn` (OneShot, staggered) | 6–36s | Spawn 12 punitive Mongol waves 2.5s apart |
| `MongolArmy_Finish` (OneShot) | ~56s after start | Fail mission after Mongol army deploys |
| `Rule_Diplomacy_UpdateUI` (OneShot) | 0.125s | Debounced UI data context refresh |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `gdm_chp2_tribute.scar` | `MissionOMatic/MissionOMatic.scar`, `obj_PayTheMongols.scar`, `obj_CollectTaxes.scar`, `obj_BuySettlements.scar`, `obj_BuildCabins.scar`, `obj_BanditCamps.scar`, `Diplomacy_Tribute.scar`, `Training_Tribute.scar` |
| `diplomacy_tribute.scar` | `gameplay/xbox_diplomacy_menus.scar` (conditional, Xbox only) |
| `obj_buysettlements.scar` | `gdm_chp2_tribute.scar` (circular reference for shared globals) |
| `training_tribute.scar` | `training/campaigntraininggoals.scar` |

### Shared Globals

- `player1`–`player4`: Player references (Muscovites, Bandits, Mongols, Dmitry holder)
- `t_difficulty`: Central difficulty table read by all objective files
- `t_settlementData`: 7-settlement array with trade amounts, income, purchase state — shared between collecttaxes, buysettlements, and UI
- `t_banditZones`, `t_banditWanderers`: Bandit zone definitions shared between collecttaxes and banditcamps
- `t_banditSpawnMarkers`, `t_banditExitMarkers`: Edge spawn/exit markers used by bandits and Mongol army
- `t_banditCampData`: Camp data shared between banditcamps init and monitor
- `i_numSettlementsBought`: Settlement purchase counter used by buysettlements, bandits, and wanderers
- `i_mongolPaymentCycle`: Payment cycle counter; escalates bandit strength and tribute demands
- `i_mongolTributePaid`, `i_mongolTributeDemanded`: Tribute tracking shared between paythemongols and core
- `g_leaderDmitry`: Leader SGroup (MissionOMatic leader pattern)
- `sg_dmitry`: Dmitry SGroup used by training hints
- `_diplomacy`: Full diplomacy state table shared between diplomacy_tribute and all UI callers
- `b_enableBuySettlementsUI`: Flag toggled by buysettlements, read by UI update function
- `eg_importantBuildings`: EGroup monitored for mission fail condition
- `OBJ_*` / `SOBJ_*`: Objective constants registered in init functions, started/completed across files
- `EVENTS.*`: Intel event constants referenced by objectives for narrative triggers

### Inter-File Function Calls

| Caller File | Called Function | Defined In |
|-------------|----------------|------------|
| gdm_chp2_tribute | `PayTheMongols_InitObjectives()` | obj_paythemongols |
| gdm_chp2_tribute | `CollectTaxes_InitObjectives()` | obj_collecttaxes |
| gdm_chp2_tribute | `BuySettlements_InitObjectives()` | obj_buysettlements |
| gdm_chp2_tribute | `BuildCabins_InitObjectives()` | obj_buildcabins |
| gdm_chp2_tribute | `BanditCamps_InitObjectives()` | obj_banditcamps |
| gdm_chp2_tribute | `Tips_InitObjectives()` | training_tribute |
| gdm_chp2_tribute | `PayTheMongols_StartObjective()` | obj_paythemongols |
| gdm_chp2_tribute | `Diplomacy_OverrideSettings()` | diplomacy_tribute |
| gdm_chp2_tribute | `Diplomacy_OverridePlayerSettings()` | diplomacy_tribute |
| gdm_chp2_tribute | `Diplomacy_SetTaxRate()` | diplomacy_tribute |
| gdm_chp2_tribute | `Diplomacy_ShowUI()` | diplomacy_tribute |
| gdm_chp2_tribute | `Diplomacy_ShowDiplomacyUI()` | diplomacy_tribute |
| gdm_chp2_tribute | `UI_BuySettlementsPanel_UpdateData()` | obj_buysettlements |
| gdm_chp2_tribute | `Bandits_Init()` | obj_collecttaxes |
| gdm_chp2_tribute | `BanditCamps_Init()` | obj_banditcamps |
| gdm_chp2_tribute | `CollectTaxes_MarkSettlementAsSeen()` | obj_collecttaxes |
| gdm_chp2_tribute | `MissionTutorial_AddHintToDmitry()` | training_tribute |
| gdm_chp2_tribute (delegate) | `Mission_OnTributeSent()` | gdm_chp2_tribute (via Core_CallDelegateFunctions) |
| obj_collecttaxes | `Bandits_Start()` | obj_collecttaxes (self) |
| obj_collecttaxes | `BuySettlements_FindSettlement()` | obj_buysettlements |
| obj_collecttaxes | `BuySettlements_GetActiveTraderCount()` | obj_buysettlements |
| obj_collecttaxes | `MissionTutorial_AddHintToBuildTraders()` | training_tribute |
| obj_paythemongols | `BuySettlements_Start()` | obj_buysettlements |
| obj_paythemongols | `MongolArmy_Start()` | obj_paythemongols (self) |
| obj_paythemongols | `Diplomacy_ShowDiplomacyUI()` | diplomacy_tribute |
| obj_paythemongols | `MissionTutorial_AddHintToPayMongols()` | training_tribute |
| obj_paythemongols | `MissionTutorial_AddHintToUseMarket()` | training_tribute |
| obj_buysettlements | `BuySettlements_StartFindMoreSettlementsObjective()` | obj_buysettlements (self) |
| obj_buysettlements | `MissionTutorial_AddHintToBuySettlements()` | training_tribute |
| obj_buysettlements | `MissionTutorial_AddHintToBuildDefencesAroundSettlement()` | training_tribute |
| obj_buysettlements | `Diplomacy_UpdateUI()` | diplomacy_tribute |
| obj_buysettlements | `Mission_AdjustPlayerMaxPopCap()` | gdm_chp2_tribute |
| obj_buildcabins | (self-contained) | — |
| diplomacy_tribute | `Core_CallDelegateFunctions("OnTributeSent")` | triggers `Mission_OnTributeSent` in core |

### MissionOMatic Integration

- Uses `MissionOMatic/MissionOMatic.scar` framework for recipe, modules, objectives, leader system
- Leader: Prince Dmitry initialized via `Missionomatic_InitializeLeader` with `neutralHolder = player4` for downed state
- Modules: 1 `UnitSpawner` for initial player units (trade carts, villagers, military, leader)
- Locations: Moscow (player1)
- Dynamic modules: `RovingArmy` for bandits (per-zone), `Defend` for bandit camps, `RovingArmy` for punitive Mongol army
- Custom UI: WPF XAML diplomacy panel with integrated Buy Settlements sub-panel, Xbox controller support via `xbox_diplomacy_menus.scar`
- `Diplomacy` registered as a Core module via `Core_RegisterModule("Diplomacy")`
- Trade route completion tracked via `GE_TradeRouteCompleted` global event
- Trade cart health doubled via `Modifier_Create` on `health_maximum_modifier`
