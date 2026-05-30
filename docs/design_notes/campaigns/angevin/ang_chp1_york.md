# Angevin Chapter 1: York

## OVERVIEW

"York 1069" is the second mission of the Norman/Angevin campaign. The player controls King William's Normans (player1) starting in the Dark Age, tasked with reclaiming the city of York from rebel factions and Danish raiders. The mission flows through sequential phases: capture two rebel villages (Middlethorpe, Fulford), develop an economy, deal with a Danish raiding threat (repel or pay tribute or destroy their camp), build up military support (stable + landmark to Feudal Age), breach the city gates, and destroy the rebel keep. Three enemy factions operate simultaneously — Village Rebels, City Rebels, and Danes — each with distinct RovingArmy/Defend modules managed through MissionOMatic. Difficulty scaling affects enemy counts, raid timings, spawn delays, patrol sizes, unit build times, and outpost upgrades across four tiers.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp1_york_data.scar` | data | Initializes all globals, SGroups, EGroups, unit tables, wave data, patrol targets, and the MissionOMatic recipe (locations, modules, audio, NIS). |
| `ang_chp1_york.scar` | core | Main mission script — player setup, difficulty config, restrictions, init/start flow, event handlers, patrol/reinforcement logic, spawn systems, Dane raid mechanics, tribute UI bridge, outro staging. |
| `diplomacy_chp1_york.scar` | other (UI system) | Full diplomacy/tribute UI framework — data context creation, XAML panel, tribute send/clear/increment logic, network sync, player relationship display. |
| `training_york.scar` | training | Tutorial goal sequences — gather food, build barracks, build palisade, build landmark/wonder, send gold tribute, stop attacking buildings. |
| `obj_capture_locations.scar` | objectives | Defines and registers OBJ_CaptureMiddlethorpe and OBJ_CaptureFulford with sub-objectives for defeating rebels and capturing locations. |
| `obj_defeat_danes.scar` | objectives | Defines OBJ_RepelAttack, OBJ_StopDaneRaids (with SOBJ_PayTribute / SOBJ_DestroyCamp alternatives), and OBJ_DestroyCampAlt. Tracks Dane building destruction and tribute progress. |
| `obj_develop.scar` | objectives | Defines OBJ_DevelopEconomy with sub-objectives: build farms (4), assign wood gatherers (5), build houses (2). |
| `obj_reclaim.scar` | objectives | Defines the primary OBJ_ReclaimYork with sub-objectives SOBJ_BreachGates and SOBJ_DestroyKeep. Monitors gate destruction and keep health. |
| `obj_strengthen.scar` | objectives | Defines OBJ_BuildSupport with sub-objectives: gather resources for landmark, build landmark (Feudal Age), build stable. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `York_Data_Init` | data | Initialize all mission globals, unit tables, wave data |
| `GetRecipe` | data | Return MissionOMatic recipe with modules and locations |
| `Mission_SetupPlayers` | core | Configure 5 players, relationships, ages, colors, pop caps |
| `Mission_SetDifficulty` | core | Define `t_difficulty` table via Util_DifVar for all tiers |
| `Mission_SetRestrictions` | core | Lock construction/upgrades, remove abilities for enemies |
| `Mission_Preset` | core | Init objectives, deploy units, set wave build times |
| `Mission_Start` | core | Start primary objectives, add interval rules, set gold |
| `York_InitPlayerUnits` | core | Spawn player cavalry, scouts, spears, archers at markers |
| `York_InitEnemyUnits` | core | Deploy Dane lines, defenders, outer guards, city gate units |
| `York_MoveStartingUnits` | core | Formation-move all starting units to destination markers |
| `York_CheckMissionFail` | core | Fail mission if no TC or no military units remain |
| `York_OnConstructionComplete` | core | Track farm/house/palisade/stable/landmark construction |
| `York_AddPatrolTargets` | core | Activate rebel patrol routes and start reinforcement timer |
| `York_UpdatePatrolTargets` | core | Set patrol targets based on difficulty attack group count |
| `York_DefendTheKeep` | core | Redirect all rebel patrols to defend keep area |
| `York_AddFinalRebelTargets` | core | Extend patrol routes to include village targets |
| `York_SpawnEarlyRaiders` | core | Periodically spawn escalating early raider waves |
| `York_StopEarlyRaiders` | core | Disband early raider module, remove spawn rule |
| `York_SpawnDaneRaiders` | core | Spawn repeating Dane raider waves from camp |
| `York_TriggerDaneTravel` | core | Set Dane attackers to travel state with road targets |
| `York_StartInitialDaneRaid` | core | Launch first 3-group Dane attack toward Fulford |
| `York_CheckDaneArrival` | core | Monitor Dane proximity to Fulford, switch to raiding |
| `York_TriggerDaneWithdraw` | core | Force Dane retreat by setting withdraw threshold to 2 |
| `York_CheckDaneWithdraw` | core | Auto-withdraw Danes when below 50% strength |
| `York_SpawnDaneGold` | core | Create gold resource pickups at Dane camp markers |
| `York_CheckDaneCampReveal` | core | Detect when player sees Dane camp, trigger intel |
| `York_CheckBridgeTriggers` | core | Start breach gates objective when player nears bridges |
| `York_CheckMiddlethorpeTrigger` | core | Reveal Middlethorpe FOW, merge outer guards on approach |
| `York_CheckFulfordTrigger` | core | Reveal Fulford FOW, start capture objective on approach |
| `York_CheckKeepTrigger` | core | Reveal keep area, boost defender compositions |
| `York_CheckKeepDefendTrigger` | core | Toggle rebel defend-the-keep mode on player proximity |
| `York_ShowTributeMenu` | core | Configure diplomacy UI to show only Danes for gold tribute |
| `York_HideTributeMenu` | core | Disable and hide diplomacy UI |
| `York_SpawnReinforcements` | core | Spawn friendly reinforcements with pop cap clamping |
| `York_ReinforceRebels` | core | Periodically replenish rebel waves up to pop cap |
| `York_CheckWave` | core | Scale wave unit counts by villager ratio and escalation |
| `York_CheckKeepRepair` | core | Spawn rebel villagers to repair keep on Hard+ difficulty |
| `York_SetUpOutro` | core | Stage outro — burn keep, destroy all squads, spawn parade |
| `Mission_OnTributeSent` | core | Track gold tribute progress toward Dane payment goal |
| `Diplomacy_DiplomacyEnabled` | diplomacy | Initialize diplomacy state and data context |
| `Diplomacy_CreateUI` | diplomacy | Build XAML tribute panel UI or Xbox variant |
| `Diplomacy_SendTributeNtw` | diplomacy | Network-synced tribute transfer between players |
| `Diplomacy_UpdateDataContext` | diplomacy | Refresh tribute button states, visibility, age checks |
| `Diplomacy_OverridePlayerSettings` | diplomacy | Override per-player tribute visibility/enabled state |
| `CaptureLocations_InitMiddlethorpe` | obj_capture | Register Middlethorpe capture objective and sub-objectives |
| `CaptureLocations_InitFulford` | obj_capture | Register Fulford capture objective and sub-objectives |
| `DefeatDanes_InitObjectives` | obj_danes | Register all Dane-related objectives (repel/pay/destroy) |
| `DefeatDanes_OnSquadKilled` | obj_danes | Update repel progress bar on Dane squad kills |
| `DefeatDanes_CheckBuildings` | obj_danes | Track Dane building destruction for camp destroy objectives |
| `PayTribute_Start` | obj_danes | Set tribute counter, show tribute UI, enable training |
| `PayTribute_Complete` | obj_danes | Complete Dane objectives, withdraw Danes, spawn gold |
| `Develop_InitObjectives` | obj_develop | Register economy objectives (farms, wood, houses) |
| `Develop_CheckGathering` | obj_develop | Monitor wood gatherer count for SOBJ_AssignToWood |
| `Reclaim_InitObjectives` | obj_reclaim | Register OBJ_ReclaimYork, SOBJ_BreachGates, SOBJ_DestroyKeep |
| `Reclaim_OnEntityKilled` | obj_reclaim | Trigger gate breach complete on gate/wall destruction |
| `Reclaim_CheckKeep` | obj_reclaim | Monitor keep health, complete mission below 0.5% HP |
| `Reclaim_Complete` | obj_reclaim | Stop rebels, celebrate, complete mission |
| `Strengthen_InitObjectives` | obj_strengthen | Register OBJ_BuildSupport and sub-objectives |
| `TrainingGoal_AddGatherFood` | training | Create food gathering tutorial goal sequence |
| `TrainingGoal_AddBuildBarracks` | training | Create barracks building tutorial (PC variant) |
| `TrainingGoal_AddBuildBarracks_Xbox` | training | Create barracks building tutorial (Xbox variant) |
| `TrainingGoal_AddBuildWonder` | training | Create landmark/wonder building tutorial (PC variant) |
| `TrainingGoal_AddBuildWonder_Xbox` | training | Create landmark/wonder building tutorial (Xbox variant) |
| `TrainingGoal_AddBuildPalisade` | training | Create palisade wall building tutorial |
| `TrainingGoal_AddStopAttacking` | training | Create stop-attacking-buildings tutorial |
| `TrainingGoal_AddSendGold` | training | Create send-gold-tribute tutorial |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_ReclaimYork` | Primary | Top-level mission objective — reclaim the city of York |
| `SOBJ_BreachGates` | Primary (sub) | Destroy a city gate or wall section to enter York |
| `SOBJ_DestroyKeep` | Primary (sub) | Reduce the rebel keep to below 0.5% health |
| `OBJ_CaptureMiddlethorpe` | Capture | Capture the village of Middlethorpe (first objective) |
| `SOBJ_DefeatMiddlethorpeRebels` | Capture (sub) | Defeat Middlethorpe's rebel defenders |
| `SOBJ_LocationMiddlethorpe` | Capture (sub) | Middlethorpe location marker |
| `OBJ_CaptureFulford` | Capture | Capture the village of Fulford (second village) |
| `SOBJ_DefeatFulfordRebels` | Capture (sub) | Defeat Fulford's rebel defenders |
| `SOBJ_LocationFulford` | Capture (sub) | Fulford location marker |
| `OBJ_DevelopEconomy` | Build | Build up economy after capturing Middlethorpe |
| `SOBJ_BuildFarms` | Build (sub) | Build 4 additional farms |
| `SOBJ_AssignToWood` | Build (sub) | Assign 5 villagers to chop wood |
| `SOBJ_BuildHouses` | Build (sub) | Build 2 additional houses |
| `OBJ_BuildSupport` | Build | Build up support for your army (after Fulford) |
| `SOBJ_GatherResourcesForLandmark` | Build (sub) | Gather 400 Food and 200 Gold for landmark |
| `SOBJ_BuildLandmark` | Build (sub) | Construct a landmark to advance to Feudal Age |
| `SOBJ_BuildStable` | Build (sub) | Build a stable to produce horsemen |
| `OBJ_RepelAttack` | Battle | Repel the initial Danish raid (timed — countdown) |
| `OBJ_StopDaneRaids` | Optional | Stop the Danish raids (parent for two alternatives) |
| `SOBJ_PayTribute` | Optional (sub) | Send gold tribute to Danes (amount = difficulty-scaled) |
| `SOBJ_DestroyCamp` | Optional (sub) | OR destroy the Dane camp (7 buildings) |
| `OBJ_DestroyCampAlt` | Optional | Standalone Dane camp destroy (if discovered before raid) |
| `OBJ_DebugComplete` | Primary | Debug cheat objective — instantly completes mission |

### Difficulty

All values use `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| `danes_goldAmount` | 500 | 500 | 800 | 1200 | Gold tribute required / gold pickups spawned |
| `danes_spawnDelay` | 240 | 200 | 160 | 120 | Interval (sec) between repeating Dane raid spawns |
| `danes_initRaid_Countdown` | 150 | 150 | 120 | 90 | Timer (sec) for initial raid repel objective |
| `danes_raiderCount1` | 2 | 3 | 5 | 7 | Initial Dane attack group 1 & 3 squad count |
| `danes_raiderCount2` | 4 | 4 | 5 | 6 | Initial Dane attack group 2 squad count |
| `danes_raiderCountCap` | 16 | 20 | 30 | 40 | Max Dane raider squads during repeating raids |
| `danes_defenderCount` | 8 | 10 | 15 | 20 | Dane camp defender squad count |
| `rebels_earlyRaiderCount` | 0 | 1 | 2 | 3 | Base early raider spawn count (0 = disabled on Easy) |
| `rebels_earlyRaidInterval` | 200 | 200 | 160 | 120 | Interval (sec) between early raider spawns |
| `rebels_defenderCount` | 3 | 4 | 5 | 5 | City rebel defender squad count per module |
| `rebels_patrolCount` | 3 | 6 | 8 | 12 | Rebel patrol unit count per patrol module |
| `rebels_attackStartDelay` | 240 | 240 | 120 | 60 | Delay (sec) before rebel patrols become aggressive |
| `rebels_attackGroupCount` | 0 | 1 | 2 | 3 | Number of rebel patrol groups that go on offense |
| `rebels_initNumSquads` | 3 | 4 | 5 | 6 | Initial rebel wave escalation counter |
| `rebels_reinforceDelay` | 300 | 240 | 200 | 160 | Interval (sec) between rebel reinforcement waves |
| `rebels_maxModuleSize` | 10 | 15 | 25 | 35 | Max squads per rebel wave module |
| `enemy_unitBuildTime` | 30 | 25 | 20 | 12 | Wave unit build time override (sec) |
| `upgradeLevel` | 0 | 0 | 1 | 2 | Outpost arrowslit upgrade level (0=removed, 1=city, 2=all) |
| `extraVillagerCount` (locations) | 12 | 9 | 6 | 6 | Extra villagers granted on village capture |

Additional: On Easy difficulty, player starts with bonus gold equal to `danes_goldAmount`.

### Spawns

**Player Starting Forces:**
- 5× horseman groups (2 squads each), 2× scouts, 5× spearman groups (3 each), 4× archer groups (3 each)
- King William leader unit at `mkr_william_start_n`

**Player Reinforcements:**
- After economy complete: 10 men-at-arms, 10 spearmen, 10 archers, 5 horsemen (at Middlethorpe)
- After stable built: 10 spearmen, 10 men-at-arms, 10 horsemen (at Fulford)

**Dane Initial Raid:** 3 attack groups, each with `danes_raiderCount1/2` units of UNIT_RAIDER_DANE + shield_villager, traveling via road markers to Fulford. Withdraws when below 50% strength.

**Dane Repeating Raids:** Spawned every `danes_spawnDelay` seconds. Count escalates by 5 per raid up to `danes_raiderCountCap`. Split 33/33/33 across 3 RovingArmy modules. Cycle between traveling → raiding → retreating states.

**Dane Camp Defenders:** `danes_defenderCount` each of UNIT_RAIDER_DANE + shield_villager. Three static defense lines (dane_line1/2/3) merge into DaneDefenders on player approach.

**Rebel Waves (3 concurrent):**
- Wave 1 (West): spearmen, staging from west city, auto-launch
- Wave 2 (Crossroads): shield villagers + archers, staging from crossroads
- Wave 3 (North Gate): horsemen, staging from north gate
- All waves use `Wave_New` with `auto_launch = true`, scaled by escalation counter and rebel villager ratio

**Early Raiders:** Spawn every `rebels_earlyRaidInterval` at `mkr_early_raiders`. Unit types cycle through scout → shield_villager → archer → horseman → men-at-arms. Escalates per cycle, max count doubles after economy objective.

**Village Defenders:**
- Middlethorpe: 2 groups (6+5 shield_villager, 4+5 archers) + outer guards
- Fulford: 10 archers, 8+5+3+5 mixed shield_villager/archer at multiple spawn points

**City Defenders:** Multiple Defend modules — CityRebelsCrossroads, KeepDefenders, BaileyRebels, BridgeGuards, SouthBridgeGuards, WestBridgeGuards, OutpostGuards, WestRebels. Unit counts scale with `rebels_defenderCount`.

### AI

- `AI_Enable(playerNeutrals, false)` — Neutrals have no AI
- All enemy factions use **MissionOMatic modules** instead of standard AI:
  - **RovingArmy** modules: WestPatrol, BaileyPatrol, KeepPatrol, CavalryRaiders, DaneAttackers1/2/3, EarlyRaiders, RiverRebels, BridgeGuards, SouthBridgeGuards, WestBridgeGuards
  - **Defend** modules: MiddlethorpeRebels1/2, FulfordRebels, DaneDefenders, NorthGateRebels, CityRebelsCenter, CityRebelsCrossroads, KeepDefenders, BaileyRebels, OutpostGuards, WestRebels
  - **UnitSpawner**: PlayerStartLeader (King William)
- RovingArmy targeting: `ARMY_TARGETING_CYCLE` for patrols, `ARMY_TARGETING_DISCARD` for RiverRebels
- `attackMoveStyle_attackEverything` with configurable `scanRangeEnRoute`, `combatRange`, `leashRange` (typically 30)
- Withdraw thresholds: 0.2–0.6 depending on module role
- Patrol targets dynamically updated based on `rebels_attackGroupCount` (difficulty-driven)
- Keep defend mode: when player enters keep proximity (25 range), all patrols redirect to keep; reverts after `rebels_defend_phase_length` (20 ticks) without player presence
- On Hard+, rebel villagers spawn to repair the keep when player is not nearby

### Timers

| Rule | Type | Timing | Purpose |
|------|------|--------|---------|
| `York_CheckDaneCampReveal` | Interval | 1s | Detect when player can see Dane camp buildings |
| `York_CheckDaneCampLooted` | Interval | 1s | Check if all Dane gold pickups collected (achievement) |
| `York_CheckBridgeTriggers` | Interval | 1s | Start breach gates obj when player nears bridge |
| `York_CheckMiddlethorpeTrigger` | Interval | 1s | Reveal FOW and merge defenders on approach |
| `York_CheckFulfordTrigger` | Interval | 1s | Reveal FOW and start Fulford obj on approach |
| `York_CheckKeepTrigger` | Interval | 1s | Reveal keep, boost compositions, start defend checks |
| `York_CheckReactionScout` | Interval | 1s | Play scout retreat when player sees Middlethorpe scout |
| `York_CheckMissionFail` | Interval | 1s | Monitor for mission fail (no TC or no military) |
| `York_MoveStartingUnits` | OneShot | 0.25s | Move all starting units to formation positions |
| `York_SpawnEarlyRaiders` | Interval | `rebels_earlyRaidInterval` | Spawn escalating early raiders |
| `York_SpawnDaneRaiders` | Interval | `danes_spawnDelay` | Spawn repeating Dane raid waves |
| `York_CheckDaneArrival` | Interval | 2s | Monitor Dane approach to Fulford |
| `York_CheckDaneWithdraw` | Interval | 1s | Auto-withdraw Danes when weakened |
| `York_CheckInitDaneRaid` | Interval | 5s | Check if player left Dane camp area to start raid |
| `York_StartCheckInitDaneRaid` | OneShot | 90s | Delayed start of initial Dane raid check |
| `RepelAttack_TimerComplete` | OneShot | `danes_initRaid_Countdown` | Fail repel objective when timer expires |
| `York_ReinforceRebels` | Interval | `rebels_reinforceDelay` | Periodically reinforce rebel wave modules |
| `York_AddPatrolTargets` | OneShot | `rebels_attackStartDelay` | Activate rebel offensive patrol routes |
| `York_CheckFulfordTC` | Interval | 5s | Monitor Fulford TC health for Dane raid interaction |
| `York_CheckKeepDefendTrigger` | Interval | 3s | Toggle keep defend mode based on player proximity |
| `York_CheckKeepRepair` | Interval | 5s | Spawn repair villagers for keep (Hard+ only) |
| `Reclaim_CheckKeep` | Interval | 0.5s | Monitor keep health for final objective completion |
| `DefeatDanes_CheckBuildings` | Interval | 1s | Track Dane building count for camp destruction progress |
| `Develop_CheckGathering` | Interval | 1s | Monitor wood gatherer count for economy objective |
| `Game_TransitionToState("default")` | — | 450s | Lighting transition after mission start |
| `York_TransitionOutroLight` | OneShot | 450s | Transition to outro lighting state over 1200s |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core campaign framework (imported by both data and core files)
- `obj_capture_locations.scar` — Middlethorpe/Fulford capture objectives
- `obj_develop.scar` — Economy development objectives
- `obj_strengthen.scar` — Army support building objectives
- `obj_reclaim.scar` — Primary reclaim York objectives
- `obj_defeat_danes.scar` — Dane raid/tribute objectives
- `diplomacy_chp1_york.scar` — Custom tribute UI system
- `training_york.scar` — Tutorial goal sequences
- `training/campaigntraininggoals.scar` — Shared campaign training functions
- `gameplay/xbox_diplomacy_menus.scar` — Xbox-specific diplomacy menu (conditional)

### Shared Globals
- `g_leaderKingWilliam` — Leader unit initialized via `Missionomatic_InitializeLeader`
- `t_difficulty` — Difficulty parameter table, created in core, consumed everywhere
- `player1`/`playerNormans`, `playerVillageRebels`, `playerCityRebels`, `playerDanes`, `playerNeutrals` — Player references used across all files
- `entity_keep` — Keep entity reference used in core, obj_reclaim, and data
- `eg_keep`, `eg_danehouses`, `eg_daneoutposts`, `eg_dane_gold` — Key EGroups shared across files
- `rebel_wave_1/2/3` and `rebel_wave_data_1/2/3` — Wave objects created in data, managed in core
- `_diplomacy` — Diplomacy system state table (diplomacy file, accessed by training)
- `t_allCaptureLocationPrefabs` — Location prefab table used by training stop-attacking logic
- `g_palisadeWallBuilt`, `g_stableBuilt`, `g_landmarkBuilt` — Construction tracking flags (data → core → objectives)
- `initial_dane_raid_complete`, `dane_camp_destroyed`, `danes_discovered`, `danes_have_raided` — Dane state flags shared between core and objectives

### Inter-File Function Calls
- Core → Data: `York_Data_Init()`, `GetRecipe()`
- Core → Objectives: `Reclaim_InitObjectives()`, `CaptureLocations_InitMiddlethorpe/Fulford()`, `Develop_InitObjectives()`, `Strengthen_InitObjectives()`, `DefeatDanes_InitObjectives()`
- Core → Diplomacy: `York_ShowTributeMenu()`, `York_HideTributeMenu()`, `Diplomacy_OverrideSettings()`, `Diplomacy_OverridePlayerSettings()`, `Diplomacy_SetTaxRate()`, `Diplomacy_ShowUI()`
- Core → Training: `TrainingGoal_AddLeaderRecovery()`, `TrainingGoal_AddSendGold()`, `TrainingGoal_AddBuildPalisade()`, `TrainingGoal_AddBuildBarracks()/_Xbox()`, `TrainingGoal_AddBuildWonder()/_Xbox()`, `TrainingGoal_EnableCampaignEconGoals()`, `TrainingGoal_EnableBuildPalisade()`, `TrainingGoal_EnableSendGold()`, `TrainingGoal_DisableSendGold()`
- Objectives → Core: `York_SpawnReinforcements()`, `York_StopEarlyRaiders()`, `York_FindPalisadeBastion()`, `York_AddPatrolTargets()`, `York_AddFinalRebelTargets()`, `York_StartCheckInitDaneRaid()`, `York_TriggerDaneWithdraw()`, `York_SpawnDaneGold()`
- Diplomacy → Core: `Core_CallDelegateFunctions("OnTributeSent")` → `Mission_OnTributeSent()`
- Training → Diplomacy: reads `_diplomacy.data_context.is_ui_expanded` and `is_ui_visible`

### Key MissionOMatic Framework Usage
- `MissionOMatic_FindModule(descriptor)` — Retrieve module by name for dynamic target/composition changes
- `RovingArmy_SetTargets()`, `RovingArmy_AddTargets()`, `RovingArmy_SetWithdrawThreshold()`, `RovingArmy_Disband()` — Runtime patrol control
- `SpawnUnitsToModule()`, `TransferModuleIntoModule()`, `DissolveModuleIntoModule()` — Dynamic force management
- `Reinforcement_SetIdealComposition()` — Update module target unit mix at runtime
- `Wave_New()`, `Wave_SetUnits()`, `Wave_Prepare()`, `Wave_Pause()`, `Wave_OverrideUnitBuildTime()` — Wave system for rebel reinforcements
- `LOCATION()`, `Location_SetCapturable()` — Capture point system for villages
- `Objective_Register()`, `Objective_Start()`, `Objective_Complete()`, `Objective_Fail()`, `Objective_SetCounter()`, `Objective_SetProgressBar()`, `Objective_AddUIElements()` — Full objective lifecycle
- `UnitEntry_DeploySquads()`, `SpawnUnitGroups()` — Unit spawning utilities
- `EventCues_CallToAction()` — Contextual call-to-action notifications
- `Util_StartIntel()` — Trigger narrative intel/NIS events
