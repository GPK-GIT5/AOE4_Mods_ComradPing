# Angevin Chapter 2: Tinchebray

## OVERVIEW

Tinchebray (1106) is an Angevin campaign RTS mission where the player controls King Henry I's English army against Duke Robert Curthose's forces. The mission has three phases: destroy two enemy villages (Martigny and Frenes) to lure Robert's army out of its defensive position, intercept an enemy relief army before it reinforces Robert, then eliminate Robert's field army and capture the Duke himself. A gold-based reinforcement purchasing system (via a customized diplomacy/tribute UI) lets the player hire named reserves — Alan of Brittany (infantry), Ranulf of Bayeux (archers), Raoul of Tosny (cavalry), and Elias of Maine (knights) — using gold collected from the map. An achievement tracks purchasing 45+ knights. The outro cinematic shows Robert captured as a prisoner.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp2_tinchebray.scar` | core | Main mission script: player setup, game flow, army AI, spawn logic, village tracking, outro staging |
| `ang_chp2_tinchebray_data.scar` | data | Initializes all state variables, SGroups, EGroups, reinforcement data tables, and the MissionOMatic recipe/modules |
| `ang_chp2_tinchebray_training.scar` | training | Training goal sequences for picking up gold and opening the diplomacy/reserve panel |
| `diplomacy_chp2_tinchebray.scar` | other | Customized diplomacy system repurposed as a "Buy Reserves" panel; handles tribute UI, XAML, and network events |
| `obj_defeat.scar` | objectives | Registers all primary and sub-objectives with start/complete/fail callbacks |
| `obj_reinforce.scar` | other | Reinforcement purchase UI logic: builds reserve panel data, handles buy button callbacks, deploys purchased units |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Sets up 4 players, ages, diplomacy, colors |
| `Mission_SetupVariables` | core | Calls data init, castle init, starting units |
| `Mission_SetDifficulty` | core | Defines difficulty-scaled enemy unit counts |
| `Mission_Preset` | core | Upgrades outposts/keep, spawns Robert, sets music |
| `Mission_Start` | core | Starts defeat objective, resets resources, adds fail check |
| `Mission_Start_Delayed` | core | Starts village destruction objective after 2s |
| `Mission_OnTributeSent` | core | Processes gold tribute toward OBJ_PayTribute |
| `Tinchebray_InitCastle` | core | Modifies gates (50% damage, invuln threshold), upgrades towers |
| `Tinchebray_InitStartingUnits` | core | Spawns wall archers, outer guards, palisade vanguards |
| `Tinchebray_Spawn_Henry_Army` | core | Deploys player's 3 infantry groups + King Henry + scout |
| `Tinchebray_InitVillages` | core | Spawns Martigny/Frenes garrison archers and guard modules |
| `Tinchebray_CheckVillages` | core | Monitors village building counts; triggers phase transitions |
| `Tinchebray_SallyOut` | core | Transitions Robert's army from defend to attack mode |
| `Tinchebray_SetArmyToAttack` | core | Sets army targeting to cycle mode after 45s delay |
| `Tinchebray_ProcessArmyTargets` | core | AI targeting: tracks visible player squads, spawns scouts |
| `Tinchebray_ProcessArmyTarget` | core | Per-army target logic: track, arrive, default cycle |
| `Tinchebray_CheckArmyState` | core | Monitors army elimination + Robert capture for win |
| `Tinchebray_SpawnEnemyReinforcements` | core | Spawns relief army, starts CTA and proximity checks |
| `Tinchebray_CheckReliefArmyProx` | core | If relief army reaches castle, merges into Robert's forces |
| `Tinchebray_OnReliefWithdraw` | core | Completes reinforcement objective on withdrawal |
| `Tinchebray_SpawnScout` | core | Spawns a roving scout with random patrol targets |
| `Tinchebray_RobertCallToAction` | core | Reveals Robert with FOW and CTA event cue |
| `Tinchebray_TriggerOutro` | core | Clears all units, deploys outro scene with prisoner Robert |
| `Tinchebray_CheckMissionFail` | core | Fails mission if player has no non-villager squads |
| `Tinchebray_IntroduceDiplomacyUI` | core | Shows tribute/reserve panel and starts gold reminder |
| `Tinchebray_CheckDiplomacyReminder` | core | Auto-opens diplomacy panel when gold >= 500 |
| `Tinchebray_SetPopulationCapVisibility` | core | Toggles pop cap display (hidden this mission) |
| `Tinchebray_SpawnUnitLine` | core | Spawns units across numbered markers in a line |
| `Tinchebray_SpawnIntroGroup` | core | Spawns invulnerable intro cinematic spearmen groups |
| `Tinchebray_SetDefaultArmyTargets` | core | Resets all army modules to cycle targeting |
| `Tinchebray_CheckMartignyProx` | core | Reveals Martigny on player approach, merges archers |
| `Tinchebray_CheckFrenesProx` | core | Reveals Frenes on player approach, merges archers |
| `Tinchebray_CheckReinforcementState` | core | Tracks relief army kill progress bar |
| `Tinchebray_Data_Init` | data | Initializes all state vars, SGroups, reinforcement table |
| `GetRecipe` | data | Returns MissionOMatic recipe with all modules |
| `Defeat_InitObjectives` | obj_defeat | Registers all OBJ/SOBJ objectives with callbacks |
| `UI_ReinforcePanel_UpdateData` | obj_reinforce | Builds reserve purchase UI data from t_reinforcementData |
| `UI_RequestAid_ButtonCallback` | obj_reinforce | Buys reserves: deducts gold, spawns units, tracks knights |
| `Start_IntelCooldown` | obj_reinforce | Plays intel event on first purchase, cooldown 20s |
| `TrainingGoal_AddPickupGold` | training | Adds training sequence for right-clicking gold pickups |
| `TrainingGoal_AddSendGold` | training | Adds training sequence for opening diplomacy button |
| `Diplomacy_DiplomacyEnabled` | diplomacy | Initializes full diplomacy data context |
| `Diplomacy_CreateUI` | diplomacy | Creates XAML-based Buy Reserves panel UI |
| `Diplomacy_SendTributeNtw` | diplomacy | Network handler: transfers resources between players |
| `Diplomacy_OverrideSettings` | diplomacy | Overrides tribute enabled/visible/score/team settings |
| `Diplomacy_OverridePlayerSettings` | diplomacy | Overrides per-player tribute visibility and resource toggles |
| `Diplomacy_UpdateDataContext` | diplomacy | Recalculates all UI enabled/visible states |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DefeatArmy` | Primary | Defeat Robert and his followers (completes on both sub-objectives) |
| `OBJ_DestroyVillages` | Primary | Destroy villages to lure out Robert's army |
| `SOBJ_DestroyMartigny` | Sub (of DestroyVillages) | Destroy all buildings in Martigny (counter-tracked) |
| `SOBJ_DestroyFrenes` | Sub (of DestroyVillages) | Destroy all buildings in Frenes (counter-tracked) |
| `SOBJ_EliminateReinforcements` | Sub (of DefeatArmy) | Destroy the enemy relief army before it reaches the castle |
| `SOBJ_EliminateArmy` | Sub (of DefeatArmy) | Eliminate Robert's field army (progress bar tracked) |
| `SOBJ_CaptureRobert` | Sub (of DefeatArmy) | Capture Duke Robert Curthose |
| `OBJ_DebugComplete` | Debug | Skips to outro cinematic |

### Difficulty

All values are `Util_DifVar({easy, normal, hard, hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| `upgradeLevel` | 0 | 0 | 1 | 2 | Enemy upgrade tier |
| `enemy_reinforcements_horseman` | 20 | 30 | 15 | 5 | Relief army horsemen count |
| `enemy_reinforcements_knight` | 0 | 0 | 15 | 25 | Relief army knights (none on easy/normal) |
| `enemy_reinforcements_infantry` | 12 | 15 | 20 | 25 | Relief army spearmen AND archers each |
| `enemy_mainarmy_maa` | 10 | 15 | 15 | 15 | Robert's main army men-at-arms |
| `enemy_mainarmy_knight` | 0 | 0 | 10 | 18 | Robert's main army knights (none on easy/normal) |
| `enemy_scout_limit` | 3 | 4 | 5 | 6 | Max concurrent enemy scouts |

### Spawns

**Player starting forces (x3 groups):** 5 Foot Knights, 5 Archers, 10 Spearmen per group (t_henry_infantry) plus King Henry and 1 Scout.

**Enemy static defenses:**
- 20 wall archers (10 markers x 2 each)
- 3 outer guard groups (6/3/6 archers)
- 3 palisade vanguard groups (4 spearmen, 4+4 archers)
- Keep vanguard: 5 archers + 5 spearmen
- Bailey vanguard: 3 archers + 7 spearmen

**Village garrisons (Martigny):** 3 guard modules — 5 spearmen + 5 archers, 15 spearmen, 5 spearmen + 5 archers; plus 2+3 archers at outposts.

**Village garrisons (Frenes):** 2 guard modules — 15 spearmen + 8 archers, 5 spearmen + 5 archers + 5 horsemen; plus 3+2 archers at outposts.

**Robert's main army (3 Defend modules):** 20 spearmen + 10 archers each; DukeRobert RovingArmy gets difficulty-scaled MaA + knights.

**Relief army:** Difficulty-scaled horsemen, knights, spearmen, archers — spawned at mkr_relief_army1, patrols through 8 waypoints toward castle.

**Enemy scouts:** Spawned 1 at a time up to `enemy_scout_limit`, roving randomly across 11 patrol markers.

**Player purchasable reserves (gold cost):**
- Alan of Brittany (100g): 5 Spearmen + 5 Archers
- Ranulf of Bayeux (200g): 20 Archers
- Raoul of Tosny (300g): 5 Knights + 15 Horsemen
- Elias of Maine (500g): 10 Knights + 10 Dismounted Knights

### AI

- `AI_Enable(playerNeutral, false)` — neutral player has no AI
- `PlayerUpgrades_Auto(playerHuman, false)` — player auto-upgrades disabled
- `PlayerUpgrades_Auto(playerRobert, true)` — Robert gets auto-upgrades
- **Robert army state machine:** Starts in `"defend"` mode (3 Defend modules). On village destruction, `Tinchebray_SallyOut()` dissolves Defend modules into RovingArmy modules (A2/B2/C2), sets `robert_army_state = "out"`. After 45s delay, `Tinchebray_SetArmyToAttack()` switches to `"attack"` with `ARMY_TARGETING_CYCLE`.
- **Army targeting AI (`Tinchebray_ProcessArmyTargets`, every 5s):** Checks if Robert can see player squads. If visible, each army sub-group attack-moves toward closest visible player unit (`"track"` state). On losing sight, continues to last known position (`"arrive"`), then reverts to default cycle targets.
- **Relief army:** RovingArmy module with 0.2 withdraw threshold and 8 sequential waypoints. On reaching final destination, disbands and merges units into Robert's army modules. On withdrawal, completes SOBJ_EliminateReinforcements.
- **Scouts:** RovingArmy modules with `ARMY_TARGETING_RANDOM`, patrol 11 markers. On army elimination, withdraw threshold set to 1 to force retreat.

### Timers

| Rule | Type | Timing | Purpose |
|------|------|--------|---------|
| `Tinchebray_CheckMissionFail` | Interval | 1s | Check if player has zero combat units |
| `Mission_Start_Delayed` | OneShot | 2s | Start village destruction objective |
| `Tinchebray_Spawn_Henry_Army` | OneShot | 1s | Deploy player starting forces |
| `Tinchebray_MoveMainArmy` | OneShot | 11s | Move intro armies to positions (if not skipped) |
| `Tinchebray_SetArmyToAttack` | OneShot | 45s (after sally) | Switch Robert's army to attack targeting |
| `Tinchebray_ProcessArmyTargets` | Interval | 5s | AI army targeting and scout spawning |
| `Tinchebray_CheckArmyState` | Interval | 1s | Monitor army/Robert elimination progress |
| `Tinchebray_CheckVillages` | Interval | 1s | Track village building destruction counters |
| `Tinchebray_CheckMartignyProx` | Interval | 1s | Reveal Martigny on player proximity |
| `Tinchebray_CheckFrenesProx` | Interval | 1s | Reveal Frenes on player proximity |
| `Tinchebray_CheckReinforceTrigger` | Interval | 1s | Spawn relief army when player nears trigger markers |
| `Tinchebray_CheckReinforcementState` | Interval | 1s | Track relief army kill progress |
| `Tinchebray_CheckReliefArmyProx` | Interval | 1s | Check if relief army reached castle |
| `Tinchebray_CheckReliefRemove` | Interval | 5s | Clean up fleeing relief army squads |
| `Tinchebray_IntroduceDiplomacyUI` | OneShot | 21s (after first village) | Show the Buy Reserves panel |
| `Tinchebray_AddSendGoldDelayed` | OneShot | 10s | Enable send-gold training goal |
| `TrainingGoal_EnableSendGold` | OneShot | 3s (after add) | Activate send-gold goal sequence |
| `TrainingGoal_EnablePickupGold` | OneShot | 2s | Activate pickup-gold goal sequence |
| `Tinchebray_CheckDiplomacyReminder` | Interval | 1s | Auto-open reserve panel when gold >= 500 |
| `UI_ReinforcePanel_UpdateData` | Interval | 1s | Refresh reserve purchase button states |
| `ReinforceIntel_Cooldown` | OneShot | 20s | Re-enable reinforcement intel after purchase |
| `Rule_Diplomacy_UpdateUI` | OneShot | 0.125s | Debounced diplomacy UI data context update |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (includes Cardinal scripts)
- `obj_defeat.scar` — objective definitions (mission-local)
- `obj_reinforce.scar` — reinforcement UI (mission-local)
- `ang_chp2_tinchebray_data.scar` — data initialization (mission-local)
- `ang_chp2_tinchebray_training.scar` — training goals (mission-local)
- `diplomacy_chp2_tinchebray.scar` — customized diplomacy system (mission-local)
- `training/campaigntraininggoals.scar` — shared campaign training infrastructure
- `gameplay/xbox_diplomacy_menus.scar` — Xbox-specific diplomacy UI (conditional)

### Shared Globals & Systems
- `Core_RegisterModule("Diplomacy")` — registers as a Core module with standard lifecycle callbacks
- `Core_CallDelegateFunctions("OnTributeSent", ...)` — delegate pattern for tribute events
- `Core_CallDelegateFunctions("DiplomacyEnabled", ...)` — initializes diplomacy from mission scripts
- `Missionomatic_InitializeLeader` — shared leader hero system (King Henry)
- `MissionOMatic_FindModule` / `Prefab_DoAction` / `DissolveModuleIntoModule` — MissionOMatic module management
- `RovingArmy_*` / `SpawnUnitsToModule` — shared army module API
- `EventCues_CallToAction` — shared CTA system
- `Util_DifVar` — shared difficulty scaling utility
- `EVENTS.*` — Intel event constants (Tinchebray_Intro, Tinchebray_Outro, SallyOut, StartLureArmy, Near_FirstVillage, Destroy_Martigny, Destroy_Frenes, TributePanel, ReliefArmyArrives, ReliefArmy_Damaged, ReliefArmy_Failed, GetReinforcementsA-D)
- `CampaignTraining_TimeoutIgnorePredicate` — shared training timeout logic

### Inter-file Function Calls
- Core → Data: `Tinchebray_Data_Init()`, `GetRecipe()`
- Core → Training: `TrainingGoal_AddPickupGold()`, `TrainingGoal_AddSendGold()`, `TrainingGoal_EnableSendGold()`
- Core → Diplomacy: `Diplomacy_ShowUI()`, `Diplomacy_IsExpanded()`, `Diplomacy_ShowDiplomacyUI()`, `Diplomacy_UpdateUI()`, `Core_CallDelegateFunctions("DiplomacyEnabled")`
- Core → Objectives: `Defeat_InitObjectives()`
- Core → Reinforce: `UI_ReinforcePanel_UpdateData()`
- Objectives → Core: `Tinchebray_CheckVillages()`, `Tinchebray_CheckMartignyProx()`, `Tinchebray_CheckFrenesProx()`
- Reinforce → Core: reads `t_reinforcementData`, `player_reinforcement_counter`, `reinforcements_called` globals
- Training → Diplomacy: reads `_diplomacy.data_context.is_ui_expanded/is_ui_visible`
- Diplomacy → Core: `Core_CallDelegateFunctions("OnTributeSent")` → `Mission_OnTributeSent()`
- Core → Diplomacy: `Tribute_Intel()` called from `Tinchebray_IntroduceDiplomacyUI` and `Diplomacy_ToggleDiplomacyUI`

### Achievement
- `CE_ACHIEVPURCHASEKNIGHTSTINCHEBRAY` — triggered when cumulative knight purchases reach 45+
