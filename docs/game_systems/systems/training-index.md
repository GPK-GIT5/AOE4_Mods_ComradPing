# Training & Tutorial Index

Cross-reference of the Training_Goal system, goal sequences, medal benchmarks, and campaign tutorial usage.

## Training_Goal API

The training system teaches players mechanics through interactive hints using a **Goal → GoalSequence** architecture.

### Core Data Structures

**`Training_Goal(keyType, data, completionFunc)`**
- `keyType` — UI anchor: `"Squad"`, `"Entity"`, `"PBG"`, `"Cursor"`, `"LooseReticle"`, `"ControlGroupButton1Tag"`, `"PopulationButton"`, `"CommandsCommandCardTab"`, `"EconomicCommandCardTab"`, `"MilitaryCommandCardTab"`, `"DiplomacyButton"`, `"RadialDPadLeft"`, `"XboxLandMarkSelectMenuTag"`, etc.
- `data` — Table with `ID` (debug string), `Message` (localization ID), `DataTemplate` (UI template)
- `completionFunc` — Returns `true` when goal is satisfied
- `.key` — Dynamically set by trigger predicate (entity ID, squad ID, blueprint, position, or UI element)
- `.temp` — Transient state table; `.timerID` — per-goal timing

**`Training_GoalSequence(id, repeatMax, remindMax, triggerPred, ignorePred, remindPred, bypassPred, canRegress, goals)`**
- `id` — String identifier (e.g., `"gather"`, `"build_house"`, `"age_up_abb"`)
- `repeatMax` — Repeat count (1 = once, -1 = infinite)
- `remindMax` — Reminder count after initial display
- `triggerPred` — Activation predicate (also sets goal `.key` fields)
- `ignorePred` — Temporary hide/cancel predicate
- `bypassPred` — Skip entirely predicate (player already demonstrated skill)
- `canRegress` — Whether sequence can step back to earlier goals
- `goals` — Ordered table of `Training_Goal` objects

### Registration Flow

1. `Training_AddGoalSequence(sequence)` — register with engine
2. `Training_EnableGoalSequenceByID(id, bool)` — enable/disable by string ID
3. `Training_EnableGoalSequence(sequence, bool)` — enable/disable by reference
4. `Training_ResetTimers()` — reset all training timers
5. `Training_GetNewTimerID()` — allocate timer for custom delays
6. `Training_InvalidateCurrentTag()` — force UI tag recreation
7. `Training_AddCallbacksToGoal(goal, startCb, completeCb)` — lifecycle callbacks

### Goal Lifecycle

1. Module `_OnInit` creates goals/sequences, calls `Training_AddGoalSequence`
2. Goals initially disabled; `CoreTrainingGoals_Start` enables after intro
3. Engine polls `triggerPred` — when true, activates sequence
4. Engine polls each goal's `completionFunc` — on success, advances `currentGoalIndex`
5. `canRegress = true` allows stepping back when earlier conditions become unmet
6. `ignorePred` returning true suspends display
7. `bypassPred` returning true completes entire sequence
8. After `repeatMax` completions, sequence permanently retires

---

## Goal Sequence Categories

### Core Controls (`training_goals_core_controls`)
| Sequence ID | Mechanic Taught |
|---|---|
| `single_selection` | Select a unit (left-click / press A) |
| `move_unit` | Move selected unit (right-click / press A on ground) |
| `pan_camera` | Pan camera (middle mouse / right stick) |
| `bandbox_selection` | Drag-select multiple military units |
| `setup_siege` | Setup siege weapon (right-click drag) |

### Core Economy (`training_goals_core_econ`)
| Sequence ID | Mechanic Taught |
|---|---|
| `gather` | Right-click villager on food resource |
| `build_villager` | Produce villager from TC |
| `build_house` | Build house when pop-capped (skipped for Mongol) |
| `scout_returns_sheep` | Scout drops off herded sheep at TC |
| `build_drop_off` | Build lumber camp near wood gatherers (skipped for Mongol) |
| `goal_next_idle` | Use idle villager button |
| `goal_build_farm` | Build farm near TC/mill (skipped for Mongol) |

### Age Up (`training_goals_age_up`)
| Sequence ID | Mechanic Taught |
|---|---|
| `build_towards_wonder` | View landmark requirements when can't afford |
| `build_wonder` | Build landmark when affordable (skipped for Abbasid) |

---

## Civ-Specific Goal Sequences

| Civ | Sequence ID | Mechanic Taught | Status |
|-----|------------|-----------------|--------|
| Abbasid | `build_house_of_wisdom` | Build the House of Wisdom landmark | Active |
| Abbasid | `age_up_abb` | Age up via Wing upgrades on HoW | Active |
| Abbasid | `golden_age_abb` | View Golden Age tier requirements | Active |
| Chinese | `tax_gold_chi` | Build Imperial Official when tax accumulates | Active |
| Chinese | `goal_floating_tax_chi` | Select building with excess tax (>70) | Active |
| Chinese | `create_dynasty_chi` | Build 2nd landmark to create dynasty | Active |
| Mongol | `build_ovoo` | Build Ovoo on stone deposit | Active |
| Mongol | `ovoo_depleted` | Notification when Ovoo stone exhausted | Active |
| Sultanate | `scholar_low_count_upgrade_sul` | Train more scholars when researching (level 1) | Active |
| Sultanate | `scholar_no_count_upgrade_sul` | Train scholars urgently (level 0, research halted) | Active |
| Sultanate | `scholar_idle_sul` | Garrison idle scholar in mosque | Active |
| English | *(palings, setup_camp, enclosures)* | — | Disabled/commented out |
| French | *(pavise, toggle_resource)* | — | Stub only |
| Rus | *(hunting_bounty, hunting_cabin)* | — | Disabled/commented out |

---

## Campaign Usage

### Salisbury (Tutorial Campaign)

#### sal_chp1_rebellion
Pure camera/movement tutorial. No combat.
**Goal sequences:** `Goals_PanCameraLumber` (pan to lumber camp), `Goals_PanCameraRock` (pan to rocks), `Goals_RotateCamera` (rotate), `Goals_ZoomCamera` (zoom in/out), `Goals_ResetCamera` (RS press), `Goals_SelectWilliam` (pan to Guillaume, press A), `Goals_MoveWilliam` (select → move to marker), `Goals_FOW` (fog-of-war explanation).
**Teaching flow:** Camera → Selection → Movement → FOW

#### sal_chp1_valesdun
Extensive combat tutorial with 7+ sequential objective phases.
**Goal sequences:** `Goals_SelectAllSpearmen`, `Goals_MoveSpearmen`, `Goals_CreateRegiment` (control groups), `Goals_UseMarquee` (hold LT), `Goals_SnapTo` (press LS), `Goals_AttackStructure` (palisade), `Goals_AttackMove` (press X), `Goals_CavalryVSArchers` (counter matchup), `Goals_ExploreSelection` (LT+A/B add/subtract), `Goals_TerrainAdvantage` (height advantage), `Goals_DPadUse` / `Goals_DPadUseReminder`, `Goals_BattleHelp` (counter reminder), `Goals_HeroAbility` (D-pad right → Y).
**Teaching flow:** Selection → Grouping → Attack → Counters → Terrain → Hero Abilities
**Special:** Player4 grey-out holds units during focused objectives. Reinforcement safety nets.

#### sal_chp2_dinan
Base-building and military tutorial.
**Goal sequences:** `Goals_VillagerPriorities`, `Goals_Build2Houses`, `Goals_BuildBarracks`, `Goals_RallyPoint`, `Goals_Make10Spearmen`, `Goals_BuildStables`, `Goals_HorsemenRaid`, `Goals_ProduceMultipleSources`, `Goals_BuildArchery`, `Goals_ArchersRaid`, `Goals_Make10Archers`, `Goals_SelectDPad`, `Goals_HeroAbility`, `Goals_UpgradeUnits`, `Goals_BuildBlacksmiths`, `Goals_Research`.
**Teaching flow:** Housing → Barracks → Rally → Stables → Archery → Upgrades → Siege
**Special:** Production rate ×3, construction time ×0.5. Two scripted raids teach counter-unit matchups.

#### sal_chp2_township
Age advancement and research tutorial.
**Goal sequences:** `Goals_BuildLandmark` (select villager → landmark menu), `Goals_FasterLandmark` (multi-step with auto-advance after 5s), `Goals_Research` (select Mill → Horticulture).
**Teaching flow:** Landmark → Faster Construction → Research

#### sal_chp2_womanswork
Pure economy tutorial (15 goal sequences).
**Goal sequences:** `Goals_SelectVillager`, `Goals_GatherFood`, `Goals_BuildMill`, `Goals_BuildLumber`, `Goals_VillagerCommand` (TC queue), `Goals_Make5Villagers` (LT modifier), `Goals_BuildHouses`, `Goals_Scouting`, `Goals_ScoutingHerd`, `Goals_ScoutingSecond`, `Goals_BuildMine`, `Goals_BuildFarms`, `Goals_SetBalanced` (VPS preset), `Goals_Research` (Wheelbarrow), `Goals_BuildLandmark`.
**Teaching flow:** Selection → Gathering → Building → Villagers → Housing → Scouting → Mining → Farms → VPS → Research → Landmark
**Special:** Build time ×0.25–0.75, production ×2, food gather ×2. SMS flows for Mine/Farms.

#### sal_chp3_brokenpromise
Naval and invasion tutorial.
**Goal sequences:** `Goals_Docks` (build dock), `Goals_TransportShips` (produce), `Goals_LoadTroops` (board ships), `Goals_Minimap` (navigate via minimap), `Goals_UnloadTroops` (unload at beach), `Goals_SurviveAmbush` (panic select), `Goals_MarchHastings` (scout into fog).
**Teaching flow:** Dock → Transport Ships → Loading → Minimap Navigation → Unloading → Combat → March
**Special:** Production rate ×2, build time ×0.5.

---

### Art of War Challenges

#### challenge_basiccombat
**Training file:** `challenge_mission_basiccombat_training.scar`
**Goal sequences:** `meat_shield` (place spearmen in front of archers), `hold_ground`
**Hint triggers:** Stealth forest (wave 2, 10s), meat-shield (wave 4, 10s), ridge/elevation (wave 5, 10s)
**Medal system:** Gold: <16 lost (19 Xbox), Silver: <21 (26 Xbox), Bronze: <36 (41 Xbox)

#### challenge_advancedcombat
**Training file:** None (uses hint points + CTA cues)
**Hint triggers:** Stealth forest (wave 4, 10s), cliffs (wave 5, 10s), army selection reminder (30s)
**Medal system:** Gold: <15 lost (18 Xbox), Silver: <30 (35 Xbox), Bronze: <40 (45 Xbox)

#### challenge_earlyeconomy
**Training file:** `challenge_mission_earlyeconomy_training.scar`
**Goal sequences:** `train_villager` (idle TC, 15s/5s), `idle_villager` (5s idle), `idle_scout` (20s idle, max 5 repeats)
**Hint triggers:** Sheep gathering (20s), scout usage (60s), deer (55s), mill reminder (40s), stone warning
**Medal system:** Gold: ≤5m10s (5m20s Xbox), Silver: ≤6m00s (6m30s Xbox), Bronze: ≤7m30s (8m00s Xbox)

#### challenge_lateeconomy
**Training file:** `challenge_mission_lateeconomy_training.scar`
**Goal sequences:** `train_villager` (idle TC), `train_trader` (idle Market), `idle_villager` (5s), `idle_trader` (10s), `idle_scout` (20s)
**Hint triggers:** Second TC, markets, houses (pop ≥85%), farms, technologies, premature aging
**Medal system:** Gold: ≤10m30s (10m45s Xbox), Silver: ≤15m30s (16m00s Xbox), Bronze: ≤19m30s (20m00s Xbox)

#### challenge_earlysiege
**Training file:** `challenge_mission_earlysiege_training.scar`
**Goal sequences:** Ram building (select → place → build → garrison), Springald built, Mangonel built, Siege tower built (with dismissible warning)
**Medal system:** Gold: ≤6 min (7 Xbox), Silver: ≤10 (12 Xbox), Bronze: ≤20. Forfeited on reinforcement.

#### challenge_latesiege
**Training file:** `challenge_mission_latesiege_training.scar`
**Goal sequences:** Siege tower lifecycle (build → garrison → approach wall → unload), Ram built, Springald built, Mangonel built, Trebuchet built, Bombard built (9 sequences total)
**Medal system:** Gold: ≤6 min (7 Xbox), Silver: ≤9 (10 Xbox), Bronze: ≤15 (16 Xbox). Forfeited on reinforcement.

#### challenge_malian
**Training file:** `challenge_mission_malian_training.scar`
**Goal sequences:** `musofadi_stealth` (select Musofadi → activate stealth), `diplomacy_panel` (open reinforcement panel)
**Medal system:** Bronze: ≥4500 gold (4000 Xbox), Silver: ≥7000 (6500 Xbox), Gold: ≥7000 (6500 Xbox)

#### challenge_montgisard
**Training file:** None (tip objectives only)
**Tip objectives:** Sacred Sites mechanics (SOBJ_SacredSitesTip, SOBJ_SacredSitesTip_Build)
**Medal system:** Gold: <17 min, Silver: <25 min, Bronze: <60 min, Conqueror: <25 min in Conqueror Mode

#### challenge_ottoman
**Training file:** `training_ottoman.scar` (placeholder, content commented out)
**Medal system:** Bronze: survive ≥10 min (8 Xbox), Silver: ≥15 (12 Xbox), Gold: ≥21 (16 Xbox)

#### challenge_safed
**Training file:** `challenge_safed_training.scar`
**Goal sequences:** Villager protection/selection (single sequence)
**Medal system:** Based on fortress health %. Conqueror: all villagers alive + 2 mines before 5:00

#### challenge_towton
**Training file:** None (hint objectives only)
**Hint objectives:** `OBJ_AgeUpHint` (7 min), `OBJ_ProductionHint` (8 min)
**Medal system:** Gold: save 35+ buildings, Silver: 20+, Bronze: survive all waves

#### challenge_walldefense
**Training file:** None (tip objectives only)
**Tip objectives:** `SOBJ_SpendResources`, `SOBJ_QuickBuild`. VO warnings for rams/siege towers/mangonels/trebuchets (30s cooldown).
**Medal system:** Bronze: survive 300s, Silver: 600s, Gold: 900s

#### challenge_agincourt
**Training file:** None
**Medal system:** Gold: ≤16 min, Silver: ≤20 min, Bronze: complete challenge, Conqueror: defeat strengthened French

---

## Data Templates

| Template | Usage |
|----------|-------|
| `GenericTrainingDataTemplate` | Default hint display |
| `LeftClickTrainingDataTemplate` | PC left-click instruction |
| `RightClickTrainingDataTemplate` | PC right-click instruction |
| `PanCameraTrainingDataTemplate` | Camera pan instruction |
| `RadialTrainingDataTemplate` | Controller radial menu instruction |

---

## Input Mode Adaptation

Each `*TrainingGoals_OnInit` function branches on three input modes:

| Mode | Detection | Key Type | Data Templates | Extra Goals |
|------|-----------|----------|---------------|-------------|
| **PC (default)** | Neither Xbox check | `"Cursor"` | LeftClick / RightClick | Fewest per sequence |
| **Xbox Controller** | `UI_IsXboxControllerUI()` | `"LooseReticle"`, `"Squad"` | Generic / Radial | Radial menu steps added |
| **Xbox KBM** | `UI_IsXboxKBMUI()` | Various | Generic | Command card tab navigation added |

Xbox medal thresholds are generally relaxed (e.g., 7→8 min, 16→19 units lost).

---

## Timer Constants

| Constant | Value | Purpose |
|----------|-------|---------|
| `__t_trainingBriefInterval` | 1s | Minimal delay |
| `__t_trainingShortInterval` | 15s (core), 10s (Mongol) | Short delay |
| `__t_trainingModerateInterval` | 30s | Standard delay |
| `__t_trainingLongInterval` | 60s | Extended delay |
| `__t_trainingWonderInterval` | 15s | Landmark hint delay |
| `__t_trainingHoverInterval` | 3s | Required hover time |
| `__t_trainingRadialInterval` | 5s | Controller radial view time |
| `__t_trainingLongDistance` | 50 | Distance invalidation threshold |

---

## Campaign-Specific Features

| Feature | Function | Usage |
|---------|----------|-------|
| Leader Recovery | `TrainingGoal_AddLeaderRecovery()` | Detects downed leader via ownership change, prompts rescue within 12m |
| Timeout Ignore | `CampaignTraining_TimeoutIgnorePredicate` | Auto-disables sequences after 60–120s |
| Diplomacy Panel | `CampaignTraining_AddDiplomacyPanelHint` | Console-only hint for tribute/diplomacy panel |

---

## Module Registration

All training modules use `Core_RegisterModule()`:

| Module | Purpose |
|--------|---------|
| `CoreTrainingGoals` | Universal controls + economy |
| `CampaignTrainingGoals` | Campaign overlays (defers to Core if registered) |
| `AbbasidTrainingGoals` | House of Wisdom, Wings, Golden Age |
| `ChineseTrainingGoals` | Tax gold, floating tax, dynasty |
| `MongolTrainingGoals` | Ovoo, depleted notification |
| `SultanateTrainingGoals` | Scholar availability |
| `EnglishTrainingGoals` | *(disabled)* |
| `FrenchTrainingGoals` | *(stub)* |
| `RusTrainingGoals` | *(disabled)* |

Civ modules gate on `Player_GetRaceName(Game_GetLocalPlayer())` matching their civilization.

### Challenge-Specific Training Modules

| Module | Challenge |
|--------|-----------|
| `BasicCombatTrainingGoals` | challenge_basiccombat |
| `EarlyEconomyTrainingGoals` | challenge_earlyeconomy |
| `LateEconomyTrainingGoals` | challenge_lateeconomy |
| `EarlySiegeTrainingGoals` | challenge_earlysiege |
| `LateSiegeTrainingGoals` | challenge_latesiege |
| `MalianTrainingGoals` | challenge_malian |
| `SafedTrainingGoals` | challenge_safed |

### Construction Phase Tracking

The system hooks into the construction modal via `UI_SetModalConstructionPhaseCallback`:
- **TP_Position / TP_Facing** → `training_currentConstructionBlueprint` set
- **TP_Issued** → `training_previousConstructionBlueprint` set, current cleared
- **TP_Cancelled** → both cleared

Similarly: `UI_SetModalAbilityPhaseCallback` and `UI_SetModalHoverCallback` track ability targeting and blueprint hovering.
