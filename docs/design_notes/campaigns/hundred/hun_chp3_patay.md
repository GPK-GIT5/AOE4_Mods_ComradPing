# Hundred Years War Chapter 3: Patay

## OVERVIEW

The Battle of Patay (1429) is mission 6 of the Hundred Years War campaign. The player controls Jeanne d'Arc's French cavalry force pursuing retreating English troops along a road toward the town of Patay. The mission progresses through distinct phases: an opening ambush, clearing road blockers, fighting through St. Sigmund, breaking an English blockade in a main battle, then chasing down three fleeing English regiments before they reach Patay. A gold-based reinforcement purchase system lets the player buy named allied reserves (archers, infantry, horsemen, knights) via a customized diplomacy/tribute UI panel. The mission ends when all regiments are eliminated and the blockade is defeated, with an optional objective to take control of Patay's town center and economy.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| hun_chp3_patay.scar | core | Main mission script: player/AI setup, phase triggers, battle logic, spawn management |
| hun_chp3_patay_data.scar | data | All variable initialization, SGroup creation, regiment/scatter/reinforcement data tables, MissionOMatic recipe |
| diplomacy_chp3_patay.scar | other | Customized diplomacy & tribute UI system repurposed as the reinforcement purchase panel |
| obj_defeat_english.scar | objectives | Defines and registers all OBJ_/SOBJ_ objective constants with callbacks |
| obj_reinforcements.scar | other | Reinforcement panel UI data binding and gold-for-units purchase logic |
| hun_chp3_patay_training.scar | training | Tutorial goal sequence prompting the player to use the diplomacy/gold-send panel |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | hun_chp3_patay | Configure 4 players, ages, relationships, colours |
| Mission_SetDifficulty | hun_chp3_patay | Set difficulty vars for regiment timers and counts |
| Mission_SetRestrictions | hun_chp3_patay | Remove tower/wall/TC production for player |
| Mission_Preset | hun_chp3_patay | Apply upgrades, init objectives, audio, spawn units |
| Mission_Start | hun_chp3_patay | Start primary objective, deploy palings, set resources |
| Patay_CheckAmbushTrigger | hun_chp3_patay | Trigger ambush when player reaches marker |
| Patay_SpawnAmbush | hun_chp3_patay | Deploy 4 rearguard RovingArmy archer groups |
| Patay_StartRearguardPursuit | hun_chp3_patay | Redirect rearguard armies to pursue player |
| Patay_DisbandRearguard | hun_chp3_patay | Disband rearguard and flee to marker |
| Patay_CheckClearRoadTrigger | hun_chp3_patay | Start clear road objective on proximity |
| Patay_CheckStSigmundTrigger | hun_chp3_patay | Start St. Sigmund objective on proximity |
| Patay_CheckMainBattleTrigger | hun_chp3_patay | Activate blockade battle and road patrol |
| Patay_BeginMainBattle | hun_chp3_patay | Launch 3 battle groups, spawn regiments, track progress |
| Patay_ProcessMainBattle | hun_chp3_patay | Monitor main line and battle group attrition |
| Patay_CheckBattleGroup | hun_chp3_patay | Check individual battle group for rout threshold |
| Patay_SpawnRegiment | hun_chp3_patay | Spawn regiment and scatter group units at markers |
| Patay_SetRegimentUnitData | hun_chp3_patay | Configure unit compositions per regiment by difficulty |
| Patay_BeginChasePhase | hun_chp3_patay | Start regiment elimination phase with timed wakes |
| Patay_CheckRegiments | hun_chp3_patay | Poll all 3 regiments for completion |
| Patay_CheckRegiment | hun_chp3_patay | Check single regiment kill count and progress bar |
| Patay_ActivateRegiment | hun_chp3_patay | Set RovingArmy targets to activate regiment march |
| Patay_MergeRegiment | hun_chp3_patay | Merge scatter groups into parent regiment |
| Patay_WakeRegiment1/2/3 | hun_chp3_patay | Timed activation of each regiment |
| Patay_CheckScatterGroups | hun_chp3_patay | Monitor scatter groups for flee/merge logic |
| Patay_SpawnJoanCav | hun_chp3_patay | Spawn Joan and cavalry reinforcements |
| Patay_SpawnSigmundReserve | hun_chp3_patay | Spawn English archer/spearman clusters at St. Sigmund |
| Patay_InitStartingUnits | hun_chp3_patay | Spawn player army and intro archer groups |
| Patay_MoveStartingUnits1/2 | hun_chp3_patay | Animate intro archer retreat and player advance |
| Patay_StartRoadPatrol | hun_chp3_patay | Deploy and move 5-archer patrol on road |
| Patay_InitPatay | hun_chp3_patay | Spawn allied villagers and assign to resources |
| Patay_TakeControlOfPatay | hun_chp3_patay | Transfer Patay ownership, grant resources by time |
| Patay_CheckAllyFlee | hun_chp3_patay | Flee allied villagers when English approach |
| Patay_CheckMissionFail | hun_chp3_patay | Fail if all units lost or TC destroyed |
| Patay_CheckPatayDefendTrigger | hun_chp3_patay | Start defend objective when English near Patay |
| Patay_CheckSigmundFail | hun_chp3_patay | Fail St. Sigmund if player runs past it |
| Patay_SetGoldValue | hun_chp3_patay | Set gold pickup entities to 400 gold each |
| Patay_OnSquadKilled | hun_chp3_patay | Track road blocker and sigmund kill progress |
| Patay_CheckReinforcePanel | hun_chp3_patay | Enable reinforcement panel on first qualifying event |
| Patay_CheckGoldPickupsLooted | hun_chp3_patay | Track achievement for collecting all gold chests |
| Patay_SetUpOutro | hun_chp3_patay | Deploy Joan and army for outro cinematic |
| Patay_TriggerOutro | hun_chp3_patay | Call Mission_Complete |
| Patay_Data_Init | data | Initialize all mission variables, SGroups, data tables |
| GetRecipe | data | Return MissionOMatic recipe with modules and settings |
| DefeatEnglish_InitObjectives | obj_defeat_english | Define and register all objective constants |
| UI_ReinforcePanel_UpdateData | obj_reinforcements | Refresh reinforcement panel UI data bindings |
| UI_RequestAid_ButtonCallback | obj_reinforcements | Purchase reinforcements with gold, spawn units |
| Start_IntelCooldown | obj_reinforcements | Play reinforcement intel event with 20s cooldown |
| Diplomacy_DiplomacyEnabled | diplomacy | Initialize diplomacy data context and UI state |
| Diplomacy_CreateUI | diplomacy | Build WPF XAML tribute/reinforcement panel |
| Diplomacy_SendTributeNtw | diplomacy | Network callback to transfer resources between players |
| Diplomacy_OverrideSettings | diplomacy | Override tribute enable/visibility flags |
| Diplomacy_OverridePlayerSettings | diplomacy | Override per-player tribute button states |
| TrainingGoal_AddSendGold | training | Register tutorial goal for diplomacy gold usage |
| TrainingGoal_EnableSendGold | training | Enable the send-gold training prompt |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_DefeatEnglish | Primary | Top-level: defeat the English on the road to Patay |
| OBJ_ClearRoad | Battle | Clear the blocked road (archer barricade with palings) |
| OBJ_ClearStSigmund | Battle | Clear English from St. Sigmund village |
| OBJ_DefeatArmy | Battle | Defeat the English blockade (main battle, progress-tracked) |
| OBJ_ClearRegiments | Battle | Eliminate 3 remaining English regiments (parent objective) |
| SOBJ_ClearRegiment1 | Battle (sub) | Eliminate the eastern regiment |
| SOBJ_ClearRegiment2 | Battle (sub) | Eliminate the central regiment |
| SOBJ_ClearRegiment3 | Battle (sub) | Eliminate the western regiment |
| OBJ_TakePatay | Optional | Take control of Patay (transfer buildings/villagers to player) |
| OBJ_DefendPatay | Information | Town Center in Patay must survive |
| OBJ_DebugComplete | Debug | Destroy all English and trigger outro |

### Difficulty

| Parameter | Values (Easy/Normal/Hard/Hardest) | Effect |
|-----------|-----------------------------------|--------|
| `regimentWakeTimer` | 60 / 40 / 30 / 30 seconds | Time before each regiment activates (multiplied by 1x/3x/5x per regiment) |
| `regimentBaseCount` | 9 / 10 / 10 / 10 | Base multiplier for regiment unit squads |
| `regimentSiegeCount` | 1 / 2 / 2 / 2 | Number of siege units (springalds/mangonels) per regiment |

Additional static thresholds: `road_blocker_threshold = 5`, `sigmund_threshold = 5`, `main_line_threshold = 10` (reduced to 3 if player skips St. Sigmund), `battle_group_threshold = 6` (reduced to 1 if skipped).

### Spawns

**Player starting army**: 2 scouts, 6 horsemen, 15 knights across 9 sub-groups at staggered markers.

**Intro archers**: 5 groups of English archers (2–3 each) that retreat during the opening cinematic.

**Rearguard ambush**: 4 RovingArmy groups (archers + scouts, ~17 squads total) spawned when player reaches ambush trigger. Pursue the player then flee and despawn.

**Road blockers**: 20 archers with palings deployed across 5 line markers (UnitSpawner, holdPosition).

**Main line**: 24 archers with palings across 8 markers (UnitSpawner, holdPosition).

**St. Sigmund garrison**: 20 spearman Defend module + 20 reserve archers/spearmen spawned in clusters. Survivors retreat to join blockade if defeated.

**Battle groups**: 3 RovingArmy modules, each with 10 archers + 4 men-at-arms. Activated sequentially during main battle.

**Regiments** (chase phase, difficulty-scaled):
- Regiment 1: 3×base archers + 1×base horsemen (east road, init ~40)
- Regiment 2: 2×base archers + 4×base spearmen + siege springalds (mid road, init ~62)
- Regiment 3: 3×base archers + 4×base men-at-arms + siege mangonels (west road, init ~72)

**Scatter groups**: 3 mixed groups (archers/spearmen/men-at-arms, 7 squads each) that flee toward and merge into Regiment 1.

**Joan cavalry**: 1 Joan hero + 4 groups of scouts and horsemen (5 each), spawned on blockade defeat.

**Purchasable reinforcements** (gold cost):
- 10 Archers — 400 gold
- 6 Men-at-arms + 4 Crossbowmen — 600 gold
- 10 Horsemen — 800 gold
- 8 Royal Knights — 1000 gold

**Patay villagers**: 8 farmers, 6 woodcutters, 3 gold miners, 1 stone miner, 2 shepherds (allied, transferred on capture).

**Patay defenders**: 2 Defend modules (5 spearmen + 5 crossbowmen each) for playerAllies.

### AI

- `AI_Enable(playerNeutrals, false)` — neutrals holder for Joan leader entity disabled.
- `PlayerUpgrades_Auto(player1, false)` — player auto-upgrades disabled.
- `PlayerUpgrades_Auto(playerEnglish, false, {...})` — English get specific archer upgrades only (Silk String, Incendiary, Ranged Damage II).
- **RovingArmy modules**: Rearguard1–4 (withdrawThreshold 0.5, attackEverything), BattleGroup1–3, Regiment1–3, SigmundAttackers, LureArchers.
- **Defend modules**: SigmundDefenders, PatayDefenders1–2, BlockadeMangonel1–2.
- Regiments start stationary, activate on timed wake or proximity (60 range), speed up when player within 35 range. Scatter groups flee when locally outnumbered and merge into parent regiment.
- `DissolveModuleIntoModule("SigmundDefenders", "SigmundAttackers")` if player skips St. Sigmund.

### Timers

| Call | Timing | Purpose |
|------|--------|---------|
| `Rule_AddInterval(Patay_CheckAmbushTrigger, 1)` | 1s | Poll for ambush proximity trigger |
| `Rule_AddInterval(Patay_CheckMissionFail, 1)` | 1s | Check mission fail conditions |
| `Rule_AddInterval(Patay_CheckGoldPickupsLooted, 1)` | 1s | Track gold chest achievement |
| `Rule_AddInterval(Patay_CheckClearRoadTrigger, 1)` | 1s | Start clear road on proximity |
| `Rule_AddInterval(Patay_CheckStSigmundTrigger, 1)` | 1s | Start St. Sigmund on proximity |
| `Rule_AddInterval(Patay_CheckMainBattleTrigger, 1)` | 1s | Start main battle on proximity |
| `Rule_AddInterval(Patay_CheckMainBattleStartTrigger, 1)` | 1s | Begin main battle engagement |
| `Rule_AddInterval(Patay_ProcessMainBattle, 1)` | 1s | Track main battle attrition and progress |
| `Rule_AddInterval(Patay_CheckDepartTrigger, 1)` | 1s | Begin chase phase on proximity |
| `Rule_AddInterval(Patay_CheckRegiments, 1)` | 1s | Poll all 3 regiments for elimination |
| `Rule_AddInterval(Patay_CheckPatayDefendTrigger, 1)` | 1s | Detect English approaching Patay |
| `Rule_AddInterval(Patay_CheckAllyFlee, 3)` | 3s | Flee allied villagers from English |
| `Rule_AddInterval(Patay_CheckScatterGroups, 3)` | 3s | Monitor scatter group flee/merge |
| `Rule_AddInterval(UI_ReinforcePanel_UpdateData, 1)` | 1s | Refresh reinforcement panel data |
| `Rule_AddOneShot(Patay_ReverseSpeedMod, 7)` | 7s | Restore player starting unit speed |
| `Rule_AddOneShot(Patay_EnableSendGoldHint, 20)` | 20s | Enable training goal for gold spending |
| `Rule_AddOneShot(Patay_SpawnRegiment, 2/3/4)` | 2s/3s/4s | Staggered regiment spawning in main battle |
| `Rule_AddOneShot(Patay_WakeRegiment1, regimentWakeTimer)` | 30–60s | Activate Regiment 1 |
| `Rule_AddOneShot(Patay_WakeRegiment2, regimentWakeTimer × 3)` | 90–180s | Activate Regiment 2 |
| `Rule_AddOneShot(Patay_WakeRegiment3, regimentWakeTimer × 5)` | 150–300s | Activate Regiment 3 |
| `Rule_AddOneShot(Patay_MergeRetreatIntoRegiment1, 35)` | 35s | Merge retreating units into Regiment 1 |
| `Rule_AddOneShot(Patay_MergeIntoSigmund, 15)` | 15s | Merge road blockers into Sigmund defense |
| `Rule_AddOneShot(ReinforceIntel_Cooldown, 20)` | 20s | Reset reinforcement intel cooldown |
| `Rule_AddOneShot(Patay_RestartMusic, 30)` | 30s | Restart music after objective |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (includes Cardinal scripts)
- `hun_chp3_patay_data.scar` — mission data
- `diplomacy_chp3_patay.scar` — customized tribute UI (itself imports `gameplay/xbox_diplomacy_menus.scar` on Xbox)
- `obj_defeat_english.scar` — objective definitions
- `obj_reinforcements.scar` — reinforcement purchase system
- `hun_chp3_patay_training.scar` — tutorial goals
- `training/campaigntraininggoals.scar` — shared campaign training framework

### Shared Globals
- `_diplomacy` — diplomacy data context (shared between diplomacy script and reinforcement/training scripts)
- `player1`, `playerEnglish`, `playerAllies`, `playerNeutrals` — player handles used across all files
- `g_leaderJoan` — leader data table initialized via `Missionomatic_InitializeLeader()`
- `t_reinforcementData` — reinforcement purchase definitions (data → obj_reinforcements)
- `t_regiments`, `t_scatter_groups` — regiment/scatter data tables (data → core)
- `t_difficulty` — difficulty parameters (core → used in regiment spawning)
- `mkr_reinforce_main`, `mkr_reinforce_main_dest` — dynamic reinforcement spawn points updated as mission progresses
- `EVENTS` — intel event table (referenced across objectives and core for NIS/VO triggers)
- `reinforce_panel_enabled`, `b_reinforceCooldown`, `b_tributeIntelPlayed` — UI state flags shared between core and reinforcement scripts

### Inter-File Function Calls
- Core calls `Patay_Data_Init()`, `DefeatEnglish_InitObjectives()`, `TrainingGoal_AddSendGold()`, `TrainingGoal_EnableSendGold()` from respective files
- Core calls `Diplomacy_ShowUI()`, `Diplomacy_ShowDiplomacyUI()`, `Diplomacy_IsExpanded()`, `Diplomacy_OverrideSettings()` from diplomacy script
- Core calls `UI_ReinforcePanel_UpdateData()` from reinforcement script
- Reinforcement script calls `Diplomacy_UpdateUI()` to refresh the repurposed tribute panel
- Diplomacy script calls `Core_CallDelegateFunctions("OnTributeSent", ...)` for tribute network events
- Achievement event: `Game_SendCustomChallengeEvent(player1, CE_ACHIEVALLGOLDCHESTSPATAY, 1)` — "Fill The Coffers" achievement (Achievement #14)

### MissionOMatic Modules Referenced
- UnitSpawner: `PlayerStartLeader`, road blockers, main line
- RovingArmy: `Rearguard1–4`, `BattleGroup1–3`, `Regiment1–3`, `SigmundAttackers`, `LureArchers`
- Defend: `SigmundDefenders`, `PatayDefenders1–2`, `BlockadeMangonel1–2`
