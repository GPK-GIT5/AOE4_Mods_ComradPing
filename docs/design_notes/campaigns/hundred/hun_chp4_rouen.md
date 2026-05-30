# Hundred Years War Chapter 4: Rouen

## OVERVIEW

The Rouen mission ("Retake Normandy", 1449) is a multi-phase campaign scenario where the player (France, Castle Age) must capture a university town, research cannon technology via the Bureau Brothers' Workshop, then breach Rouen's walls and destroy England's landmarks. The mission features four players: France (player1), England (player2, enemy), University (player3, neutral), and The Bureau Brothers (player4, ally). A customized diplomacy panel is repurposed as the Bureau Brothers' Workshop UI, tracking optional location captures (trade route, river port, mine) that provide cannon production bonuses. England sends attack waves along three lanes (north, center, south) with escalating compositions scaled by difficulty and game time, while the player must balance economy, optional objectives, and siege production.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| hun_chp4_rouen.scar | core | Main mission script: player setup, variables, restrictions, difficulty, MissionOMatic recipe, attack wave system, and game flow |
| diplomacy_rouen.scar | other | Customized diplomacy/tribute UI repurposed as Bureau Brothers' Workshop panel showing location capture bonuses |
| obj_destroy_rouen.scar | objectives | Primary objective chain: Retake Normandy → Build Cannons → Breach Walls → Destroy Landmarks |
| obj_bbsurvive.scar | objectives | Information objective requiring the Bureau Brothers' Workshop building to survive |
| obj_research.scar | objectives | Research Chemistry objective with university age-up gate and cannon research completion flow |
| obj_optionals.scar | objectives | Optional parent objective (Assist Bureau Brothers) with trade route, river port, and mine sub-objectives |
| obj_uni_capture.scar | objectives | Primary capture objective for the University town, triggers transition to base-building phase |
| sobj_capture_mine.scar | objectives | Optional sub-objective for capturing the Rouen Mine location via Location system |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| Mission_SetupPlayers | hun_chp4_rouen | Configure 4 players, ages, relationships, colours |
| Mission_SetupVariables | hun_chp4_rouen | Define SGroups, EGroups, patrol routes, global flags |
| Mission_SetRestrictions | hun_chp4_rouen | Lock siege upgrades, auto-upgrade English buildings, remove abilities |
| Mission_SetDifficulty | hun_chp4_rouen | Define difficulty-scaled resources, lane timers, defender values |
| Mission_Preset | hun_chp4_rouen | Initialize all objectives, assign villagers, init attack waves |
| Mission_Start | hun_chp4_rouen | Start primary objectives, enable proximity monitors, begin game |
| GetRecipe | hun_chp4_rouen | Build MissionOMatic recipe with locations, defenders, patrols, modules |
| Init_AttackWaves | hun_chp4_rouen | Create Wave objects for north/center/south lanes and Rouen defense |
| ConstructWave | hun_chp4_rouen | Dynamically compose wave units based on game time and type |
| Send_NorthWave | hun_chp4_rouen | Deploy cavalry wave via north lane from forward or base spawn |
| Send_CentralWave | hun_chp4_rouen | Deploy infantry wave via center lane |
| Send_SouthWave | hun_chp4_rouen | Deploy mixed wave via south lane with fallback logic |
| Manage_AttackWaves | hun_chp4_rouen | Randomly select lane, construct wave, schedule next attack |
| ChooseWhereToSendUnitsToPlayer | hun_chp4_rouen | Legacy wave dispatch with phased unit escalation |
| PrepareWaves | hun_chp4_rouen | Build wave compositions per phase and village state |
| Anti_Ram | hun_chp4_rouen | Counter player rams with springald waves on all lanes |
| CounterMonks | hun_chp4_rouen | Spawn monk+army to recapture holy sites taken by player |
| ApplyPressure_Wave1/2/3 | hun_chp4_rouen | Redirect pre-placed pressure modules toward player base |
| MonitorFirstAttackers | hun_chp4_rouen | Trigger intel event when first enemy reaches player base |
| Monitor_TC | hun_chp4_rouen | Detect TC or workshop under attack and fire intel |
| Monitor_landmarks | hun_chp4_rouen | Fail mission if player has no landmarks |
| Monitor_BBWorkshop | hun_chp4_rouen | Fail mission if Bureau Brothers Workshop destroyed |
| GameOver_EarlyDeath | hun_chp4_rouen | Fail mission if all player squads die before capture phase |
| MonitorTown02–06 | hun_chp4_rouen | Track destruction of English village clusters, cascade defenders |
| SendTown02–06UnitsOff | hun_chp4_rouen | Dissolve defeated village defenders into other modules |
| AddUnitsToDefendRouen | hun_chp4_rouen | Periodically reinforce Rouen garrison if player not nearby |
| RetakeNormandy_MoveStartingUnits | hun_chp4_rouen | Deploy intro army and march toward destination |
| DestroyFieldWall_EntityKill | hun_chp4_rouen | Celebrate and play SFX when field walls breached |
| Achievement_ProduceUpgradedCannon | hun_chp4_rouen | Track achievement for producing siege with all 3 bonuses |
| FrenchMovesOnTown | hun_chp4_rouen | Outro cinematic: parade, cheering villagers, fleeing English |
| CelebrateOnPosition | hun_chp4_rouen | Play celebration SFX on nearby friendly squads |
| Diplomacy_DiplomacyEnabled | diplomacy_rouen | Initialize custom diplomacy data context with workshop text |
| Diplomacy_CreateUI | diplomacy_rouen | Build XAML UI for Bureau Brothers settlement panel |
| Diplomacy_ShowUI | diplomacy_rouen | Show/hide the workshop panel |
| Diplomacy_UpdateDataContext | diplomacy_rouen | Refresh all UI state: enabled, visibility, tribute buttons |
| Diplomacy_OverridePlayerSettings | diplomacy_rouen | Override tribute visibility per player |
| Diplomacy_SendTributeNtw | diplomacy_rouen | Network callback to transfer resources between players |
| Init_RouenWorkshopUI | diplomacy_rouen | Populate settlement data for 3 locations with bonuses |
| UI_ReinforcePanel_UpdateData | diplomacy_rouen | Refresh workshop panel settlements data each second |
| UI_CameraSnap_ButtonCallback | diplomacy_rouen | Snap camera to settlement marker on button click |
| RetakeNormandy_InitObjectives | obj_destroy_rouen | Register OBJ_RetakeNormandy and sub-objectives |
| GetCannons_Start | obj_destroy_rouen | Begin monitoring cannon count |
| GetCannons_Monitor | obj_destroy_rouen | Track cannon production, complete at 4 cannons |
| GetCannons_Complete | obj_destroy_rouen | Start wall breach objective, transition to sunset |
| GetNearRouen_Monitor | obj_destroy_rouen | Detect player approach to Rouen, start wall events |
| DestroyWallRouen_EntityKill | obj_destroy_rouen | Track wall/gate destruction for breach objective |
| DestroyWalls_OnComplete | obj_destroy_rouen | Trigger landmark destruction phase, reinforce Rouen |
| DestroyLandmarks_UI | obj_destroy_rouen | Setup UI counter for 3 enemy landmarks |
| DestroyRouenLandmark_EntityKill | obj_destroy_rouen | Increment landmark counter on each kill |
| RetakeNormandy_OnComplete | obj_destroy_rouen | Trigger victory intel and celebration |
| BBSurvive_InitObjectives | obj_bbsurvive | Register workshop survival information objective |
| RetakeNormandy_Init_ResearchObjectives | obj_research | Register OBJ_ResearchCannons and sub-objectives |
| CannonResearch_Start | obj_research | Begin chemistry research tracking |
| CannonResearch_IsComplete | obj_research | Check if player has chemistry upgrade |
| CannonResearch_OnComplete | obj_research | Enable cannon production, start optional objectives |
| BuildLandmark_IsComplete | obj_research | Monitor age-up to Imperial, trigger chemistry availability |
| DelayDiplomacyPanel | obj_research | Show workshop UI after call-to-action clears |
| CaptureLocations_InitUniTown | obj_uni_capture | Register university capture objective with Location system |
| OBJ_CaptureUniTown.PreComplete | obj_uni_capture | Grant resources, place workshop, start monitors, spawn villagers |
| OBJ_CaptureUniTown.OnComplete | obj_uni_capture | Start survival/research objectives, enable attack waves |
| ConditionalInit_OptionalObjectives | obj_optionals | Register Assist Brothers and 3 sub-objectives |
| AssistBrothers_IsComplete | obj_optionals | Check all 3 optional locations completed |
| TradeRoute_Step1–3 | obj_optionals | Proximity → clear defenders → assign 3 traders sequence |
| RiverPort_Step1–2 | obj_optionals | Proximity → raze all port buildings sequence |
| MineCapture_PlayerProx | obj_optionals | Start mine capture on player proximity |
| StartOptionals_IfNotStarted | obj_optionals | Force-start all optional objectives at once |
| CaptureLocations_InitRouenMine_Optional | sobj_capture_mine | Register mine capture with Location system, grant iron upgrade |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_RetakeNormandy | Primary/Battle | Top-level: retake Normandy from England |
| OBJ_CaptureUniTown | Primary/Capture | Phase 1: capture the university area |
| OBJ_ResearchCannons | Primary | Phase 2: research Chemistry upgrade |
| OBJ_BBSurvive | Information | Fail condition: Bureau Brothers' Workshop must survive |
| OBJ_AssistTheBrothers | Optional | Parent for 3 optional location captures |
| SOBJ_GetCannons | Sub/Build | Build 4 cannons (culverin/ribauldequin/cannon types) |
| SOBJ_DestroyRouenWalls | Sub/Battle | Breach Rouen's walls with siege |
| SOBJ_DestroyLandmarks | Sub/Battle | Destroy 3 English landmarks to win |
| SOBJ_DefeatUniDefenders | Sub/Capture | Clear English defenders from university |
| SOBJ_LocationUniTown | Sub/Capture | Capture university location marker |
| SOBJ_EstablishTradeRoute_Optional | Optional | Capture trade route → assign 3 traders |
| SOBJ_RaidTheRiverPort_Optional | Optional | Raze all river port buildings |
| SOBJ_CaptureRouenMine_Optional | Optional/Capture | Capture the mine via Location system |
| SOBJ_BuildLandmark | Sub/Primary | Advance to Imperial Age before chemistry |
| SOBJ_HoldTheUniversity | Sub/Primary | Hold the university location |
| SOBJ_EstablishTradeRoute | Sub/Primary | Primary version of trade route capture |
| SOBJ_RaidTheRiverPort | Sub/Battle | Primary version of river port raze |

### Difficulty

| Parameter | Easy | Normal | Hard | Expert | What it scales |
|-----------|------|--------|------|--------|----------------|
| given_resources_gold | 3000 | 2500 | 2200 | 2000 | Starting gold after university capture |
| given_resources_wood | 2400 | 1200 | 700 | 500 | Starting wood after university capture |
| given_resources_food | 3000 | 2500 | 2000 | 1200 | Starting food after university capture |
| given_resources_stone | 1000 | 1000 | 500 | 0 | Starting stone after university capture |
| initial_lane_timer_top/mid/below | 150 | 150 | 120 | 110 | Seconds between attack waves per lane |
| i_request_upperThreshold | 0.6 | 0.6 | 0.7 | 0.75 | AI request strength upper bound |
| i_request_lowerThreshold | 0.2 | 0.2 | 0.2 | 0.1 | AI request strength lower bound |
| i_request_desiredStrength | 0.7 | 0.7 | 0.8 | 1.0 | AI desired army strength |
| defenderValue | 0.66 | 0.75 | 1.0 | 1.20 | Multiplier on all defender squad counts |
| timerMod | 0 | 0 | 45 | 90 | Seconds subtracted from wave timers (faster waves) |

- Attack waves disabled entirely on Easy (Story) difficulty
- Pressure waves only on Hard+ with varying delays: Hard {300,900,1200}s, Expert {120,300,600}s
- Anti-Ram counter spawns only on Hard+ (every 360s)
- Counter-monk armies spawn every 680s on Normal+
- Siege defenders at `mkr_siege_defender_medium` only on Hard+, `mkr_siege_defender_hard` only on Expert
- Village reinforcement unit counts scale per difficulty via inline `Util_DifVar`

### Spawns

**Static Defenders (MissionOMatic modules):**
- Trade Route: 15×spearman + 5×men-at-arms (×defenderValue)
- Mine: 10×spearman + 6×archer + 2×men-at-arms (×defenderValue)
- University: 40×spearman + 15×horseman (×defenderValue)
- Patrol Routes 1/3: 15×horseman + 5×knight; Route 2: 20×spearman + 10×archer + 1×men-at-arms
- Pressure Waves 1/3: 15×horseman + 2×knight; Wave 2: 20×spearman + 5×men-at-arms
- Dynamic archery/infantry/elite/cavalry/siege defenders generated from map markers

**Attack Wave System (`Manage_AttackWaves`):**
- After university capture, randomly selects north (35%), center (31%), or south (34%) lane
- `ConstructWave` scales power exponentially: `wavePower = gameTime/4 + gameTime^6/10^9` (capped at 66 at 60 min)
- Wave types: Mixed, Infantry, Cavalry, Melee, Ranged — each with different unit pools
- Unit cost weights: siege=4, knight/crossbow=2, ram=3, others=1
- Forward spawn if enemy buildings exist and player absent; otherwise base spawn with auto-launch delay
- Rouen defense wave: 10×knight + 20×horseman + 40×spearman + 30×men-at-arms when player threatens

**Legacy Wave System (`ChooseWhereToSendUnitsToPlayer`):**
- Phase-based escalation (phases 1-2, 3-6, 7-9, 10+) per lane
- Compositions adapt based on which villages are destroyed
- Lane timers shorten as villages fall (150→180→220s depending on lane)

### AI

- `PlayerUpgrades_Auto(player2, false)` — English auto-upgrades disabled except Murder Holes
- English keeps get springald emplacement; outposts get arrowslits and stone upgrades
- No AI_Enable calls — enemy behavior driven by MissionOMatic RovingArmy modules and Wave system
- Three patrol routes with `ARMY_TARGETING_REVERSE` and `attackMoveStyle_attackEverything`
- Village defender modules dissolve into adjacent/base modules when their village is destroyed
- `CounterMonks` spawns a monk+infantry army to retake holy sites every 680s
- `AddUnitsToDefendRouen` periodically reinforces Rouen garrison (runs every 360s by scheduling)
- `wave_defend_rouen` activated if >12 player squads near Rouen and <150×defenderValue defenders present

### Timers

| Rule/Function | Interval | Purpose |
|---------------|----------|---------|
| Manage_AttackWaves | Random 120-360s (−timerMod) | Schedule next lane attack wave |
| CounterMonks | 680s interval | Spawn monk army to recapture holy sites |
| Anti_Ram | 360s interval | Check for player rams, counter with springalds |
| ApplyPressure_Wave1 | OneShot: Hard 300s / Expert 120s | Redirect PressureWave1 module to player base |
| ApplyPressure_Wave2 | OneShot: Hard 900s / Expert 300s | Redirect PressureWave2 module to player base |
| ApplyPressure_Wave3 | OneShot: Hard 1200s / Expert 600s | Redirect PressureWave3 module to player base |
| Monitor_TC | 1s interval | Check if TC/workshop under attack |
| Monitor_landmarks | 3s interval | Fail if player has 0 landmarks |
| Monitor_BBWorkshop | 3s interval | Fail if workshop destroyed |
| MonitorFirstAttackers | 2s interval | Detect first enemy near player base |
| BuildLandmark_IsComplete | 2s interval | Check if player reached Imperial Age |
| GetCannons_Monitor | 1s interval | Track cannon count toward goal of 4 |
| TradeRoute/RiverPort/Mine proximity | 1s interval | Start optional objectives on player approach |
| GameOver_EarlyDeath | 1s interval | Fail if all player squads die (pre-capture phase) |
| UI_ReinforcePanel_UpdateData | 1s interval | Refresh Bureau Brothers panel data |
| Intel_AllBonusResearchComplete | 2s interval | Check if all 3 optional bonuses done |
| Rule_Diplomacy_UpdateUI | OneShot 0.125s | Debounced UI refresh for diplomacy panel |
| Game_TransitionToState("day") | 300s | Day/night transition at mission start |
| Game_TransitionToState("sunset") | 600s | Sunset transition when cannons built |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core framework for locations, modules, waves, playbill
- `gameplay/xbox_diplomacy_menus.scar` — Xbox UI variant (conditional import)
- `training/campaigntraininggoals.scar` — Tutorial hint system
- `obj_destroy_rouen.scar` — Primary objective chain (imported by core)
- `obj_research.scar` — Research objectives (imported by core and obj_optionals)
- `diplomacy_rouen.scar` — Custom diplomacy system (imported by core)
- `obj_optionals.scar` — Optional objectives (imported by core)
- `obj_uni_capture.scar` — University capture (imported by core)
- `obj_bbsurvive.scar` — Workshop survival (imported by core)
- `sobj_capture_mine.scar` — Mine capture (imported by obj_research)

### Shared Globals
- `player1`–`player4` — Player references used across all files
- `t_difficulty` — Difficulty table referenced by all objective/spawn files
- `t_reinforcementData` — Settlement data shared between diplomacy_rouen and obj_optionals
- `OptionalObjective_Data` — Completion tracking for 3 optional locations (trade/river/mine)
- `b_universityBoonsOn` — Flag shared between research and optional systems
- `eg_bbworkshop` — Bureau Brothers Workshop EGroup monitored across multiple files
- `t_allRouenRecipeModNames` / `t_allRouenModules` — Dynamic module registry
- `numberOfCannonsObj` (=4) — Cannon build target used by obj_destroy_rouen

### Inter-file Function Calls
- Core calls `BBSurvive_InitObjectives`, `RetakeNormandy_InitObjectives`, `RetakeNormandy_Init_ResearchObjectives`, `CaptureLocations_InitUniTown`, `ConditionalInit_OptionalObjectives` during Preset
- `obj_uni_capture.OnComplete` starts `OBJ_BBSurvive` and `OBJ_ResearchCannons`
- `CannonResearch_OnComplete` calls `StartOptionals_IfNotStarted` from obj_optionals
- `obj_optionals` calls `StartMain_IfNotStarted`, `StartTradeRoute_IfNotStarted`, `StartRiverPort_IfNotStarted`, `StartMineCap_IfNotStarted`
- `obj_optionals` sets `t_reinforcementData[n].activated` and calls `Player_CompleteUpgrade` for cannon bonuses
- `CaptureLocations_InitRouenMine_Optional` (from sobj_capture_mine) registered by obj_optionals
- Core calls `Core_CallDelegateFunctions("DiplomacyEnabled")` to initialize diplomacy_rouen
- `Init_RouenWorkshopUI` called from `AssistBrothers_OnStart` (obj_optionals) populates diplomacy panel
- `AssistBrothers_IsComplete` called by `Achievement_ProduceUpgradedCannon` in core
- `Wave_New`, `Wave_Prepare`, `Wave_Launch`, `Wave_SetUnits` from MissionOMatic Wave system used throughout core
- `RovingArmy_Init`, `RovingArmy_SetTarget`, `DissolveModuleIntoModule` from MissionOMatic used in core
- `LOCATION()`, `Location_SetCapturable` from MissionOMatic location system used in obj_uni_capture and sobj_capture_mine

### Upgrade Bonuses from Optional Objectives
- Trade Route → `upgrade_reliable_supplies_fre` (reduce cannon build time 50%)
- River Port → `upgrade_shipworthy_timber_fre` (increase cannon health 50%)
- Mine → `upgrade_surplus_iron_fre` (reduce cannon gold cost 85%)

### Achievement
- `CE_ACHIEVUPGRADECANNONSNORMANDY` — Triggered when player produces a siege unit with all 3 bonuses active
