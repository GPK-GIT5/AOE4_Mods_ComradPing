# Challenge Mission: Malian

## OVERVIEW

Challenge Mission: Malian is an "Art of War" economy-and-defense scenario where the player controls a Malian (Imperial Age) force defending three gold pit mines against endless waves of Sultanate enemies approaching via three paths (west, south, east). The player earns gold passively from pit mines and spends it to purchase reinforcements (Musofadi Warriors, Donso, Archers, Javelin Throwers, Handcannoneers) through a customized diplomacy/tribute UI panel. Medal benchmarks are based on total gold collected before all mines are destroyed (PC: Bronze ≥4500, Silver ≥7000, Gold ≥7000; Xbox: Bronze ≥4000, Silver ≥6500, Gold ≥6500). Before waves begin, the player must capture two path positions; Gbeto scouts with torches line the attack paths to signal incoming enemies. Enemy monks carrying relics can convert player units, adding a conversion-defense mechanic on top of the core tower-defense loop.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_malian.scar` | core | Main mission logic: wave spawning, waypoint guidance, objectives, gold tracking, victory/defeat, pit mine defense |
| `challenge_mission_malian_diplomacy.scar` | other (UI) | Customized diplomacy/tribute system repurposed as the reinforcement purchase panel UI |
| `challenge_mission_malian_preintro.scar` | other (cinematic) | Four pre-intro cinematic shots with scripted Malian vs Sultanate battles showcasing unit types |
| `challenge_mission_malian_reinforce.scar` | other (UI) | Reinforcement purchase data context, button callbacks, gold cost deduction, unit spawning |
| `challenge_mission_malian_training.scar` | training | Tutorial hint sequences teaching Musofadi stealth activation (PC and Xbox variants) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | malian | Set Xbox-adjusted medal benchmark thresholds |
| `Mission_SetupVariables` | malian | Initialize wave paths, unit compositions, reinforcement data |
| `Mission_SetupPlayers` | malian | Init 6 players with Imperial Age and colours |
| `Mission_PreInit` | malian | Hide tribute menu before mission starts |
| `Mission_Preset` | malian | Setup game, upgrades, player units, diplomacy |
| `Mission_Start` | malian | Start objectives, waves, scouts, FOW, torches, UI |
| `GetRecipe` | malian | Define MissionOMatic recipe with locations and modules |
| `ChallengeMission_OnGameSetup` | malian | Create player/enemy/ally/neutral/scout player references |
| `ChallengeMission_SetupDiplomacy` | malian | Set all inter-player relationships and shared LOS |
| `ChallengeMission_SpawnPlayerUnits` | malian | Spawn 8 Musofadi, 10 Javelin, 10 Donso; place ally mines |
| `ChallengeMission_SetPlayerUpgrades` | malian | Grant poison arrow, stealth healing, precision training upgrades |
| `ChallengeMission_SetupGbetoScouts` | malian | Deploy invulnerable torch-bearing Gbeto along all 3 paths |
| `ChallengeMission_SetupGbetoScouts2` | malian | Issue hold-position orders to all Gbeto scouts |
| `ChallengeMission_InitializeObjectives` | malian | Register primary, battle, and medal objectives |
| `ChallengeMission_PathSetupObjectives` | malian | Create capture objectives and reticules for path setup |
| `ChallengeMission_CheckPathSetupObjectives` | malian | Monitor path capture progress; start waves on completion |
| `ChallengeMission_CapturePath1` | malian | Animate capture reticule for path 1 position |
| `ChallengeMission_CapturePath2` | malian | Animate capture reticule for path 2 position |
| `ChallengeMission_AddNewWave` | malian | Spawn next wave from endless pattern; adjust cost/timing |
| `ChallengeMission_GetWaveUnitCount` | malian | Calculate unit count fitting wave cost budget |
| `ChallengeMission_SendWave` | malian | Deploy wave units at spawn marker; reveal path |
| `ChallengeMission_GuideWaves` | malian | Advance waves along waypoints; handle monk conversion |
| `ChallengeMission_GuideWaveAttack` | malian | Redirect attacked wave toward next waypoint |
| `ChallengeMission_SwitchTarget` | malian | Redirect finished waves to nearest surviving pit mine |
| `ChallengeMission_TargetMines` | malian | Order enemy units near mines to attack pit mines |
| `ChallengeMission_Update` | malian | Main tick: spawn waves, track gold, update medals |
| `ChallengeMission_UpdateMedals` | malian | Promote medal tier when gold threshold reached |
| `ChallengeMission_CheckVictory` | malian | Evaluate win/loss when all mines destroyed |
| `ChallengeMission_EndChallenge` | malian | Play end narration; send custom event for gold medal |
| `ChallengeMission_OnSquadKilled` | malian | Handle wave defeat; unreveal path; despawn relics |
| `ChallengeMission_OnDestruction` | malian | Handle pit mine destruction; trigger victory check |
| `ChallengeMission_CheckLaneActive` | malian | Unreveal inactive lane and reset scouts to neutral |
| `ChallengeMission_CheckNodeInUse` | malian | Check if waypoint node is used by another active wave |
| `ChallengeMission_SetupMinimapPath` | malian | Create minimap blips and light torches along a path |
| `ChallengeMission_UpdateTorches` | malian | Re-light torches when scouts come on-screen |
| `ChallengeMission_ScoutHoldPos` | malian | Warp scout to marker; apply hold-ground modifiers |
| `ChallengeMission_ScoutHoldGround` | malian | Apply damage boost and block rates to stationary scout |
| `ChallengeMission_PulseThreatBlip` | malian | Pulse minimap blip at active wave positions |
| `ChallengeMission_GrantExtraGoldIncome` | malian | Add supplemental gold income every 10 seconds |
| `ChallengeMission_DespawnRelic` | malian | Destroy dropped relics near a position |
| `ChallengeMission_OrderConverts` | malian | Order converted Malian units to attack nearest mine |
| `ChallengeMission_PickUpRelic` | malian | Order monks to pick up nearby relics |
| `ChallengeMission_CheckForIdleWaves` | malian | Detect waves at mines; mark path as completed |
| `ChallengeMission_IntroduceDiplomacyUI` | malian | Show tribute/reinforce menu after 5 seconds |
| `ChallengeMission_CheckDiplomacyReminder` | malian | Auto-open diplomacy panel when gold reaches 500 |
| `ChallengeMission_ShowTributeMenu` | malian | Show UI and start update interval |
| `ChallengeMission_HideTributeMenu` | malian | Disable and hide diplomacy UI |
| `ArcFormation` | malian | Position SGroup units in curved line formation |
| `Malian_PreIntro_Shot01_Units` | preintro | Deploy Malian army vs Sultanate elephants/archers/MAA |
| `Malian_PreIntro_Shot01_Javelin_Attack` | preintro | Order javelins to attack tower elephant (3s interval) |
| `Malian_PreIntro_Shot01_Gunner_Attack` | preintro | Order handcannoneers to attack trebuchet (16s delay) |
| `Malian_PreIntro_Shot01_Turn_Elephant` | preintro | Guide elephant along waypoints (0.2s interval) |
| `Malian_PreIntro_Shot01_Musofadi_Hold` | preintro | Hold Musofadi warriors at current destination |
| `Malian_PreIntro_Shot01_Musofadi_Attack` | preintro | Release held Musofadi to attack-move |
| `Malian_PreIntro_Shot02_Units` | preintro | Deploy Musofadi/gunners vs elephants/MAA with arcs |
| `Malian_PreIntro_Shot02_Hold` | preintro | Hold all shot 2 units at destinations |
| `Malian_PreIntro_Shot02_Attack` | preintro | Order all Malian units to attack-move |
| `Malian_PreIntro_Shot02_EnemyAttack` | preintro | Order elephants to attack in facing direction |
| `Malian_PreIntro_AttackInDirection` | preintro | Find closest enemy in facing direction via dot product |
| `Malian_PreIntro_Shot03_Units` | preintro | Deploy Donso vs horsemen/knights with formation |
| `Malian_PreIntro_Shot03_DonsoAttack` | preintro | Pair Donso and knights for melee engagement |
| `Malian_PreIntro_Shot04_Units` | preintro | Deploy javelins/archers vs elephants/archers/MAA |
| `Malian_PreIntro_Shot04_Archer_Attack` | preintro | Pair Malian archers to enemy archers for poison |
| `Malian_PreIntro_Shot04_Archer_Retreat` | preintro | Retreat player archers after poison applied |
| `Malian_PreIntro_Clean_Scenes` | preintro | Master cleanup for all 4 cinematic shots |
| `Diplomacy_DiplomacyEnabled` | diplomacy | Initialize _diplomacy table with UI config/resources |
| `Diplomacy_OnInit` | diplomacy | Register global events for upgrades/construction/names |
| `Diplomacy_Start` | diplomacy | Set initial age; create UI; register network events |
| `Diplomacy_CreateUI` | diplomacy | Build XAML reinforcement purchase panel |
| `Diplomacy_UpdateDataContext` | diplomacy | Refresh tribute-enabled state and button visibility |
| `Diplomacy_OverrideSettings` | diplomacy | Override tribute/score/team visibility globally |
| `Diplomacy_OverridePlayerSettings` | diplomacy | Override per-player tribute visibility and resources |
| `Diplomacy_SendTributeNtw` | diplomacy | Network callback: transfer resources between players |
| `Diplomacy_AddTribute` | diplomacy | Increment/decrement tribute allotment with tax rate |
| `UI_ReinforcePanel_UpdateData` | reinforce | Build reinforcement panel data context with costs |
| `UI_RequestAid_ButtonCallback` | reinforce | Handle purchase: deduct gold, spawn units, play cue |
| `UI_RequestAid_EventCue` | reinforce | Show high-priority event cue for reinforcement arrival |
| `Start_IntelCooldown` | reinforce | Prevent rapid intel spam with 0.5s cooldown |
| `MalianTrainingGoals_OnInit` | training | Initialize stealth training; disable core training goals |
| `MalianTrainingGoals_InitMusofadiHint` | training | Create PC stealth goal sequence (select → activate) |
| `MalianTrainingGoals_InitMusofadiHint_Xbox` | training | Create Xbox stealth sequence (select → radial → activate) |
| `CanActivateStealthPredicate` | training | Check for idle on-screen Musofadi unit (PC) |
| `CanActivateStealthPredicate_Xbox` | training | Check for idle on-screen Musofadi unit (Xbox) |
| `UserHasSelectedMusofadiUnit` | training | Detect player selecting a Musofadi stealth unit |
| `UserActivatedStealth` | training | Detect stealth ability activated on selected unit |
| `UserHasCompletedStealth` | training | Confirm stealth activation completed after short delay |
| `MalianTrainingGoals_AddDiplomacyPanelHint` | training | Add training hint to open reinforcement panel |
| `UserHasOpenedTheDiplomacyMenu` | training | Check if diplomacy panel has been expanded |

## KEY SYSTEMS

### Objectives

| Constant/Key | Type | Purpose |
|--------------|------|---------|
| `OBJ_Victory` | Primary | Collect gold — ends when all mines destroyed |
| `OBJ_AmbushWaves` | Battle | Ambush incoming enemy waves |
| `OBJ_DefendMines` | Battle | Defend the three gold pit mines |
| `OBJ_PrepareForAmbush` | Capture | Pre-mission: capture 2 path positions to start waves |
| `SOBJ_Path1` | Capture | Position units at path 1 capture point |
| `SOBJ_Path2` | Capture | Position units at path 2 capture point |
| `OBJ_Recruit` | Optional | Use the reinforcement panel to purchase units |
| `SOBJ_RecruitPanel` | Optional | Open the diplomacy/reinforcement panel |
| `benchmarks.unplaced.objective` | Bonus | No medal — collect 3000 gold (2500 Xbox) |
| `benchmarks.bronze.objective` | Bonus | Bronze medal — collect 4500 gold (4000 Xbox) |
| `benchmarks.silver.objective` | Bonus | Silver medal — collect 7000 gold (6500 Xbox) |
| `benchmarks.gold.objective` | Bonus | Gold medal — collect 7000 gold (6500 Xbox); sends `CE_MALIANSARTGOLD` |

### Difficulty

No `Util_DifVar` scaling is used. Difficulty is effectively fixed:
- **Player**: Malian, Imperial Age, starts with 1000 gold (500 pre-setup + 1000 at Mission_Start, offset = -1000 spent)
- **Enemy**: Sultanate, Imperial Age, wave-based with escalating cost
- **Xbox adjustments**: Medal thresholds reduced by ~500 gold per tier
- **Income adjustment**: After 2 intervals, if gold income rate is below 411/min, supplemental gold is added every 10 seconds to compensate
- **Wave cost scaling**: Starts at 800, increases by 50–75 per wave depending on elapsed time
- **Wave interval scaling**: Starts at ~50s between waves, decreases over time; big waves (4, 7) get +30s before and +20s after

### Spawns

**Player starting army** (spawned at `Mission_Preset`):
- 8× Musofadi Warriors (Gbeto, tier 4 Malian)
- 10× Javelin Throwers (tier 4 Malian)
- 10× Donso/Spearmen (tier 4 Malian)

**Purchasable reinforcements** (via gold):
- Musofadi Warriors: 5 units, 360 gold
- Donso: 5 units, 400 gold
- Archers: 4 units, 430 gold
- Javelin Throwers: 4 units, 430 gold
- Handcannoneers: 2 units, 430 gold

**Enemy wave compositions** (Sultanate tier 4, 2-phase cycle of 7 wave types):

*Phase 1 (Waves 1–4):*
- Wave 1: Tower elephants + archers (path 1); MAA + monks (path 2)
- Wave 2: Crossbowmen + archers (path 1); war elephants (path 3)
- Wave 3: Tower elephants + crossbowmen + monks (path 1); knights + monks (path 3)
- Wave 4 (big): Five groups on path 2 — horsemen, tower elephants, spearmen, MAA, mangonels (5 spawn points)

*Phase 2 (Waves 5–7):*
- Wave 5: Tower elephants + spearmen (path 1); knights + MAA + monks (path 2)
- Wave 6: Crossbowmen + archers (path 1); MAA + monks (path 2); horsemen + monks (path 3)
- Wave 7 (big): Five groups on path 2 — knights, tower elephants + monks, spearmen + archers, war elephants + monks, mangonels

After wave 7, the pattern repeats from wave 1 with increased cost. Relics spawn with monks starting at wave group 15+ for conversion mechanics.

**Pre-intro cinematic units** (temporary, cleaned up):
- Shot 1: 7+4 Musofadi, 10+10 javelins, 7 archers, 8 Donso, 8 gunners vs 5 horsemen, 1 tower elephant, 1 trebuchet, 15 archers, 8 MAA
- Shot 2: 16 Musofadi, 8 gunners vs 8 MAA, 2 war elephants (weakened)
- Shot 3: 12 Donso vs 5 horsemen, 5 knights
- Shot 4: 12 javelins, 8 archers vs 10 archers, 1 tower elephant, 4 MAA

### AI

- **No `AI_Enable` calls** — all enemy behavior is scripted via wave spawning and waypoint guidance
- **Wave pathing**: Each wave follows a predefined marker path (west: 13 nodes, south: 18 nodes, east: 16 nodes) with `Cmd_FormationAttackMove` at each waypoint
- **Target switching**: `ChallengeMission_SwitchTarget` (5s) redirects waves that reach path end toward the nearest surviving pit mine
- **Mine targeting**: `ChallengeMission_TargetMines` (6s) orders enemies near mines to prioritize pit mine buildings after 2+ houses destroyed
- **Monk conversion**: Enemy monks with relics attempt `monk_conversion` on nearby player units; converted units are ordered to attack nearest pit mine
- **Relic lifecycle**: Relics spawn with later waves, are picked up by monks, dropped on conversion, then despawned

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `ChallengeMission_Update` | 0.125s | Main tick: wave spawning, gold tracking, medal updates |
| `ChallengeMission_GuideWaves` | 0.15s | Advance waves along waypoints; handle conversion logic |
| `ChallengeMission_UpdateTorches` | 0.25s | Re-light Gbeto scout torches when on-screen |
| `ChallengeMission_CheckPathSetupObjectives` | 0.5s | Monitor capture zone completion |
| `UI_ReinforcePanel_UpdateData` | 1s | Refresh reinforcement panel enabled/cost state |
| `ChallengeMission_CheckDiplomacyReminder` | 1s | Auto-open panel when gold ≥500 |
| `ChallengeMission_CapturePath1/2` | 0.025s | Animate capture reticule progress (2s duration) |
| `ChallengeMission_SwitchTarget` | 5s | Redirect finished waves to nearest pit mine |
| `ChallengeMission_TargetMines` | 6s | Order enemies to attack mines when houses lost |
| `ChallengeMission_PulseThreatBlip` | 5s | Pulse minimap blip at active wave positions |
| `ChallengeMission_GrantExtraGoldIncome` | 10s | Add supplemental gold if income below 411/min |
| `ChallengeMission_IntroduceDiplomacyUI` | OneShot 5s | Show reinforcement panel after mission start |
| `ChallengeMission_ScoutHoldPos` | OneShot 3s | Position scouts after path setup |
| `ReinforceIntel_Cooldown` | OneShot 0.5s | Reset reinforcement intel cooldown flag |
| Pre-intro `Shot01_Javelin_Attack` | 3s | Javelins attack tower elephant |
| Pre-intro `Shot01_Turn_Elephant` | 0.2s | Guide elephant along waypoints |
| Pre-intro `Shot01_Gunner_Attack` | 16s | Gunners attack trebuchet |
| Pre-intro `Shot01_Musofadi_Hold` | OneShot 5s | Hold Musofadi in arc formation |
| Pre-intro `Shot01_Musofadi_Attack` | OneShot 17s | Release Musofadi to attack |
| Pre-intro `Shot02_Hold` | OneShot 8s | Hold all shot 2 units |
| Pre-intro `Shot02_Attack` | OneShot 10.5s | Attack-move all player units |
| Pre-intro `Shot03_DonsoAttack` | OneShot 7s | Engage Donso vs knights |
| Pre-intro `Shot04_Archer_Attack` | OneShot 10s | Pair archers for poison application |
| Pre-intro `Shot04_Archer_Retreat` | OneShot 14s | Retreat archers after poison |

## CROSS-REFERENCES

### Imports
- `Cardinal.scar` — core game framework (via MissionOMatic)
- `MissionOMatic/MissionOMatic.scar` — modular mission system
- `MissionOMatic/MissionOMatic_utility.scar` — MissionOMatic utility functions
- `missionomatic/missionomatic_artofwar.scar` — Art of War challenge framework
- `training/coretraininggoals.scar` — base training system (`TrainingGoal_DisableCoreControlGoals`, `TrainingGoal_DisableCoreEconGoals`)
- `training/coretrainingconditions.scar` — training condition helpers
- `challenge_mission_malian_preintro.scar` — imported by core for cinematic
- `challenge_mission_malian_diplomacy.scar` — imported by core for tribute/reinforcement UI
- `challenge_mission_malian_reinforce.scar` — imported by core for purchase callbacks
- `challenge_mission_malian_training.scar` — imported by core (via `coretraininggoals`)
- `challenge_mission_malian.events` — narration event definitions
- `gameplay/xbox_diplomacy_menus.scar` — Xbox-specific diplomacy UI (conditionally imported)

### Shared Globals
- `localPlayer` / `enemyPlayer` / `allyPlayer` / `enemyPlayer2` / `neutralPlayer` / `scoutPlayer` — 6 player slots shared across all files
- `_challenge` — master config table (startingResources, benchmarks, icons, currentBenchmark)
- `_diplomacy` — diplomacy system state table (UI config, tribute settings, data context)
- `challengeGoldSpent` — tracks gold spent on reinforcements for net gold calculation
- `challengeGoldCollected` — computed gold total (current + spent)
- `t_reinforcementData` — reinforcement unit definitions (5 entries with costs, units, display strings)
- `player_reinforcement_counter` — increments per purchase for unique SGroup naming
- `b_reinforceCooldown` — prevents rapid intel event spam
- `waveObjectList` — active wave tracking table
- `endlessWavePattern` — 21-entry wave composition pattern (2 phases × 7 wave types)
- `waveWaypointPathsList` — 3 waypoint paths with marker arrays
- `gbetoScoutPath` — 3 paths of Gbeto scout data (sGroup, marker, torch state, road side)
- `minimapBlips` — tracked minimap blip entries for the 3 mines
- `sg_single` / `eg_single` — reusable single-element groups
- `EVENTS` — narration events (PreIntro, NarrIntro, NarrMissionStart, Narr2ndWave, NarrBigWave, NarrBronze/Silver/GoldThreshold, NarrWest/South/EastMineDestroyed, NarrMissionEndBronze/Silver/Gold, GetReinforcementsA–E)
- `_userHasOpenedDiplomacyMenu` — training hint flag for diplomacy panel
- `selectMusofadiUnitsStealthActivated` — training completion flag
- `wavesStarted` — flag set when capture objectives complete
- `eg_gold_mines` — EGroup of player pit mine buildings

### Inter-File Function Calls
- Core → diplomacy: `Diplomacy_ShowUI()`, `Diplomacy_ShowDiplomacyUI()`, `Diplomacy_IsExpanded()`, `Diplomacy_UpdateUI()`, `Core_CallDelegateFunctions("DiplomacyEnabled")`
- Core → reinforce: `UI_ReinforcePanel_UpdateData()`
- Core → preintro: `Malian_PreIntro_Clean_Scenes()`
- Core → training: `MalianTrainingGoals_AddDiplomacyPanelHint()`
- Reinforce → diplomacy: writes to `_diplomacy.data_context.buyReserves`, calls `Diplomacy_UpdateUI()`
- Reinforce → core: reads `localPlayer`, `t_reinforcementData`, `challengeGoldSpent`, `OBJ_Recruit`, `SOBJ_RecruitPanel`
- Training → diplomacy: reads `_diplomacy.data_context.is_ui_expanded`
- Training → core training: `Training_AddGoalSequence()`, `Training_GoalSequence()`, `Training_Goal()`, `Training_EnableGoalSequenceByID()`
- Diplomacy → core: `Core_RegisterModule("Diplomacy")`, `Core_GetPlayersTableEntry()`, `Core_CallDelegateFunctions("OnTributeSent")`

### Blueprint References
- **Player (Malian)**: `unit_gbeto_4_mal`, `unit_javelin_4_mal`, `unit_spearman_4_mal`, `unit_archer_4_mal`, `unit_handcannon_4_mal`, `unit_gbeto_4_only_torch_mal`, `building_open_pit_mine_mal`, `building_house_mal`
- **Enemy (Sultanate)**: `unit_spearman_4_sul`, `unit_horseman_4_sul`, `unit_knight_4_sul`, `unit_archer_4_sul`, `unit_crossbowman_4_sul`, `unit_manatarms_4_sul`, `unit_war_elephant_3_sul`, `unit_war_elephant_tower_4_sul`, `unit_monk_2_sul`, `unit_mangonel_3_sul`, `unit_trebuchet_4_cw_sul`, `building_house_control_sul`
- **Upgrades**: `upgrade_siege_engineers`, `upgrade_archer_poison_arrow_mal`, `upgrade_stealth_healing_mal`, `upgrade_donso_precision_training_mal`, `upgrade_unit_archer/spearman/javelin/gbeto_4_mal`
- **Abilities**: `activate_stealth_mal`, `core_formation_wedge`, `core_formation_spread`, `core_formation_line`, `core_building_scuttle`, `core_unit_death`, `pickup_relic`, `monk_conversion`, `monk_statetree_drop_relic`
