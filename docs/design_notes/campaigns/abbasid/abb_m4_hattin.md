# Abbasid Mission 4: Hattin

## OVERVIEW

Abbasid Mission 4 recreates the Battle of Hattin (1187) where Saladin's forces intercept Crusader columns marching to relieve Tiberias. The mission begins with a two-part tutorial teaching the **Burnable Fields** mechanic — the player attacks grass fields to set them on fire, creating smoke that debuffs Crusader units passing through (speed, damage dealt, damage received). After the tutorial, the player receives a preparation timer before 8 waves of Crusaders spawn from three map edges (north, mid, south) and march along a network of named locations toward Tiberias. The player wins by defeating all waves including the final boss Reynald; the mission fails if Crusaders reach Tiberias. An 8-player setup uses dedicated player slots for allies, defenders, burnable field entities, and neutral structures.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m4_hattin.scar` | core | Main mission script: player/relationship setup, recipe, init flow, spawn modules, map exploration, end conditions |
| `abb_m4_hattin_data.scar` | data | Constants, difficulty table (`t_difficulty`), global variable initialization |
| `abb_m4_hattin_automated.scar` | automated | Automated test harness with checkpoints (PlayStart, TutorialComplete, MissionVictory) |
| `obj_crusaders.scar` | objectives/spawns | Crusader wave objective definitions, full `t_crusaderData` wave table (8 waves), `t_crusaderLocations` pathing network, Crusader spawn/move/wait/phase management |
| `obj_burningfields.scar` | objectives/other | Burnable fields system: init, fire spread, smoke debuffs, field termination, Tiberias road monitoring |
| `obj_tutorial.scar` | objectives | Tutorial objective tree (burn fields tutorial), field-tagging hints, idle-player warnings, failure recovery |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_SetupPlayers` | abb_m4_hattin | Configures 8 players, relationships, colours, upgrades, AI |
| `Mission_SetupVariables` | abb_m4_hattin | Calls `Hattin_InitData`, creates all SGroups/EGroups |
| `Mission_Preset` | abb_m4_hattin | Inits objectives, fields, disables player control, assigns villagers |
| `Mission_Start` | abb_m4_hattin | Starts tutorial, adds end-condition check rule |
| `Mission_CheckEndConditions` | abb_m4_hattin | Checks crusader count or Tiberias breach for win/loss |
| `GetRecipe` | abb_m4_hattin | Returns MissionOMatic recipe (intro NIS, unit spawners, modules) |
| `Hattin_SpawnBarricadeAllies` | abb_m4_hattin | Spawns allied spear/archer armies at barricade markers |
| `Hattin_ReinforceAsNeeded` | abb_m4_hattin | Emergency cavalry reinforcements when troops < 40 (easy only) |
| `Hattin_InitData` | abb_m4_hattin_data | Sets all constants, difficulty table, global variables |
| `Crusaders_InitObjectives` | obj_crusaders | Registers all crusader-phase objectives, builds `t_crusaderData` and `t_crusaderLocations` |
| `Crusaders_Start` | obj_crusaders | Completes prep timer, spawns wave 1, starts manager |
| `Crusaders_SpawnUnits` | obj_crusaders | Spawns a crusader group, assigns path, chains next wave timer |
| `Crusaders_Manager` | obj_crusaders | Per-tick loop: tracks kills, callbacks, phase transitions |
| `Crusaders_ManageEntry` | obj_crusaders | Non-AI path following with pursuit/leash logic |
| `Crusaders_MoveToLocation_Start` | obj_crusaders | Picks next location, issues Army/path move orders |
| `Crusaders_MoveToLocation_Update` | obj_crusaders | Checks arrival, triggers intel events, transitions to wait |
| `Crusaders_WaitAtEncampment_Update` | obj_crusaders | Waits at location based on waitTime, then departs |
| `Crusaders_ChooseNextLocation` | obj_crusaders | Selects next location by priority, avoids burning paths |
| `Crusaders_ChooseNextLocation_ScoreFires` | obj_crusaders | Scores path 0–10 by fire ratio on route fields |
| `Crusaders_ForceMarchNext` | obj_crusaders | Forces first group at a location to depart immediately |
| `Crusaders_UpdateLocationWaitTime` | obj_crusaders | Changes a location's waitTime (used in tutorial) |
| `Crusaders_ChartFullMinimapPath` | obj_crusaders | Draws minimap path from start locations to Tiberias |
| `Crusaders_CatchStragglersOnSpawn` | obj_crusaders | Kicks stuck AI groups after spawn |
| `Crusaders_CatchStragglersOngoing` | obj_crusaders | Recurring stall detection for AI groups |
| `Crusaders_UpdateFullPath` | obj_crusaders | Reassigns a non-AI group's marker path |
| `_Crusaders_IssuePathOrders` | obj_crusaders | Resolves closest path node, issues move/attack-move orders |
| `BurnableFields_Init` | obj_burningfields | Builds `t_burnableFields` table, inits each field, starts manager |
| `BurnableFields_InitField` | obj_burningfields | Creates fire/debuff subgroups, sets targeting, fire thresholds |
| `BurnableFields_Manager` | obj_burningfields | Per-tick: fire spread, invulnerability locking, debuff triggering, burndown timers |
| `BurnableFields_TriggerDebuffs` | obj_burningfields | Applies speed/damage/received-damage modifiers to nearby Crusaders |
| `BurnableFields_ReleaseUnits` | obj_burningfields | Removes debuff state after duration expires |
| `BurnableFields_Terminate` | obj_burningfields | Ends a field's burn, kills entities, removes UI |
| `BurnableFields_Activate` | obj_burningfields | Makes field selectable, adds hintpoint/reticule/minimap icon |
| `BurnableFields_Deactivate` | obj_burningfields | Makes field invulnerable and unselectable |
| `BurnableFields_GetFireStrength` | obj_burningfields | Returns fire ratio relative to largest field |
| `Monitor_TiberiasRoadApproach` | obj_burningfields | Moves allied roadblock when enemies near location 7 |
| `BurnTutorial_InitObjectives` | obj_tutorial | Registers tutorial objective tree (OBJ_Tutorial + sub-objectives) |
| `BurnTutorial_Start` | obj_tutorial | Starts tutorial objective, intel event, Crusader manager |
| `BurnTutorial_SpawnUnits` | obj_tutorial | Spawns tutorial crusader group with path assignment |
| `BurnTutorial_WatchForBurn` | obj_tutorial | Monitors field burn status, shows debuff explainer tag |
| `Scouts1_Killed` | obj_tutorial | Handles first scout group death, pass/fail field check |
| `Scouts2_Killed` | obj_tutorial | Completes second tutorial combat on scout death |
| `Tutorial_StartSecondLocation` | obj_tutorial | Starts SOBJ_SecondTutorialBurn |
| `Tutorial_WarnIdlePlayer` | obj_tutorial | Warns player 3x if field not burning; fails on third |
| `Tutorial_HasPlayerRetreated` | obj_tutorial | Checks if player has left tutorial exclusion zones |
| `Tutorial_CheckForQueueGuidanceStart` | obj_tutorial | Triggers production queue guidance on low difficulty |
| `MissionTutorial_ManageFailure` | obj_tutorial | Recovery logic: spawns buffer units, resumes on burn |
| `MissionTutorial_TagField` | obj_tutorial | Creates right-click attack hint tag on field entity |
| `MissionTutorial_UntagField` | obj_tutorial | Removes field attack hint tag |
| `AutoTest_OnInit` | abb_m4_hattin_automated | Checks CampaignAutoTest arg, starts test flow |
| `AutomatedMission_Start` | abb_m4_hattin_automated | Gives upgrades, reveals FOW, registers checkpoints |
| `AutomatedHattin_PlayerTutorial` | abb_m4_hattin_automated | Simulates player actions through tutorial |
| `AutomatedHattin_PlayerBurnFields` | abb_m4_hattin_automated | Spawns torchers to burn key fields on timers |
| `AutomatedHattin_PlayerDefendRoad` | abb_m4_hattin_automated | Spawns/manages autotest army defending road |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Tutorial` | Primary | Tutorial umbrella: complete the burn-fields tutorial |
| `SOBJ_FirstTutorialCombat` | Primary (child) | Defeat first scout group (optionally after burning field) |
| `SOBJ_SecondTutorialBurn` | Primary (child) | Burn the large tutorial field to ≥25% |
| `SOBJ_SecondTutorialRetreat` | Primary (child) | Retreat all units to the pass marker |
| `SOBJ_SecondTutorialCombat` | Primary (child) | Defeat second scout group using crossbowmen + fire |
| `OBJ_Crusaders` | Primary | Main objective: defeat all Crusader waves, prevent Tiberias breach |
| `SOBJ_WaveCounter` | Primary (child) | Tracks waves killed vs total; completes parent when all dead + Reynald defeated |
| `SOBJ_DefeatReynald` | Primary (child) | Kill Reynald (spawns in wave 8, mid path) |
| `TOBJ_PrepareForCrusaders` | Tip (child) | Countdown timer before first wave (180/120/90/90s by difficulty) |
| `TOBJ_BurnableFields` | Tip (child) | Reminds player about burnable fields |
| `SOBJ_PlacementGuidance` | Bonus (child) | Place ≥15 military units at preparation marker (easy/medium only) |
| `SOBJ_BuildTroops` | Primary (child) | Train 20 additional military units |
| `OBJ_NextWaveTimer` | Information | Countdown to next crusader wave |
| `OBJ_ProductionQueueGuidance` | Information | Warning when production queue < 5 for > 60s |
| `OBJ_FieldScoutingGuidance` | Tip | Pings on all burnable field locations until observed |

### Difficulty

All values are arrays `{Easy, Medium, Normal, Hard}` via `Util_DifVar`:

| Parameter | Easy | Medium | Normal | Hard | Scales |
|-----------|------|--------|--------|------|--------|
| `extraGuidance` | true | true | false | false | Enables placement/build troop guidance objectives |
| `emergencyReinforcements` | true | false | false | false | Auto-spawns cavalry when troops < 40 |
| `playerStartFood` | 1400 | 1200 | 1000 | 800 | Starting resources |
| `playerStartWood` | 1000 | 800 | 700 | 600 | Starting resources |
| `playerStartGold` | 1000 | 800 | 700 | 600 | Starting resources |
| `playerStartStone` | 800 | 800 | 500 | 500 | Starting resources |
| `productionSpeedBonus` | 2.0 | 1.8 | 1.25 | 1.0 | Military build time multiplier |
| `playerFarmerStart` | 8 | 6 | 5 | 3 | Starting farmer villagers per farm group |
| `crusadePrepTime` | 180 | 120 | 90 | 90 | Seconds before first wave |
| `crusaderHasSiege` | 0 | 1 | 1 | 1 | Whether crusaders bring siege (multiplier) |
| `crusaderWaveInterval` | 120 | 90 | 90 | 90 | Seconds between waves |
| `crusaderDifficultyTopUp` | 0 | 0 | 5 | 10 | Extra squads per group |
| `crusaderDifficultyTopUpHolyOrders` | 0 | 0 | 2 | 6 | Extra holy order squads |
| `smokeDebuffDuration` | 90 | 75 | 60 | 45 | Seconds debuff lasts |
| `smokeDebuffSpeed` | 0.5 | 0.5 | 0.5 | 0.5 | Speed multiplier on debuffed |
| `smokeDebuffDmgDealt` | 0.1 | 0.2 | 0.5 | 0.6 | Damage dealt multiplier |
| `smokeDebuffDmgReceived` | 4.0 | 3.0 | 3.0 | 3.0 | Damage received multiplier |
| `fieldBurndownTime` | 120 | 90 | 60 | 60 | Seconds until field expires |
| `hornsOfHattinBurnTime` | 180 | 120 | 90 | 75 | Final field burn duration |

### Spawns

**Tutorial phase:** 2 scout groups spawn at `mkr_tutorial_crusader_spawn`:
- scouts1: 8 horsemen
- scouts2: 18 horsemen + 12 knights (leash range 100)

**Main phase:** 8 waves, each with rank 1–3 sub-groups (rank 3 only on Normal+). Three spawn lanes:
- **North** (`mkr_crusader_spawn_north`): Waves 1, 4, 8 — militia, archers, spearmen, springalds
- **South** (`mkr_crusader_spawn_south`): Waves 2 (Templars), 5 (Hospitallers), 7, 8 — holy order units + horsemen/knights
- **Mid** (`mkr_crusader_spawn_mid`): Waves 3, 6, 8 — Templar/Hospitaller Grand Masters, mixed infantry, siege

**Wave 8 (Finale):** Simultaneous 3-lane attack from all directions. Rank 2 mid group includes **Reynald** (leader unit). Rank 3 groups add mangonels + trebuchets. All groups track `g_finalCrusadersKilled` on death.

**Player starting forces** (via recipe UnitSpawner modules):
- Tutorial: 6 spearmen
- Main army: Saladin (leader) + 20 horsemen + 10 knights + 20 camel riders + 30 horse archers
- Allies (player4): 8 archers + 12 men-at-arms + 12 spearmen at roadblock; 14×3 archer groups defending Tiberias

### AI

- `AI_Enable(player7, false)` — Burnable fields player (no AI)
- `AI_Enable(player8, false)` — Neutral houses/towers (no AI)
- `CRUSADERS_USE_AI = false` — Crusaders use a custom path-following system (`Crusaders_ManageEntry`) instead of the Army AI module
- Non-AI pursuit system: groups follow marker paths, deviate to attack within `CRUSADER_PURSUIT_LEASH` (15²=225 distance²), leash back after `CRUSADER_PURSUIT_FOCUS` (90s) cooldown or exceeding leash distance
- Location network: Crusaders pathfind through named locations (Saffuriyah → Meskana → Lubiya → Horns → Tiberias) choosing open (non-burning) paths via `Crusaders_ChooseNextLocation`
- Straggler detection: `Crusaders_CatchStragglersOnSpawn` (1s) and `Crusaders_CatchStragglersOngoing` (5s recurring) kick stuck groups

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Mission_CheckEndConditions` | Interval 1s | Checks crusader count < 15 or Tiberias breach |
| `Crusaders_Manager` | Interval 3s | Global crusader phase management loop |
| `Crusaders_ManageEntry` | Every tick (Rule_Add) | Per-group non-AI path following |
| `BurnableFields_Manager` | Every tick (Rule_Add) | Fire spread, debuff checks, burndown timers |
| `Monitor_TiberiasRoadApproach` | Interval 2s | Allied roadblock repositioning |
| `TOBJ_PrepareForCrusaders` | Countdown 180/120/90/90s | Pre-wave preparation timer |
| `OBJ_NextWaveTimer` | Countdown per wave interval | Next wave arrival countdown |
| `Crusaders_SpawnUnits` | OneShot per wave delay | Chains wave spawns based on `spawnDelay` values |
| `_Crusaters_PreSpawn` | OneShot (delay - 10s) | Pre-spawn callbacks (minimap arrows) |
| `Tutorial_WarnIdlePlayer` | Interval 30s | Warns player if tutorial field not burning |
| `Tutorial_CheckForQueueGuidanceStart` | Delay 30s, Interval 5s | Starts production guidance objective |
| `Hattin_ReinforceAsNeeded` | Interval 1s | Emergency reinforcement spawns (easy only) |
| `BurnableFields_ReleaseUnits` | OneShot after debuff duration | Removes smoke debuff modifiers |
| `Mission_ExploreMap_PartB` | OneShot 0.25s | UnReveals FOW after initial reveal |
| `Crusaders_CatchStragglersOnSpawn` | OneShot 1s | Kicks stalled groups after spawn |
| `Crusaders_CatchStragglersOngoing` | OneShot 5s (recurring) | Detects and fixes stuck AI groups |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `abb_m4_hattin.scar` | `MissionOMatic/MissionOMatic.scar`, `abb_m4_hattin_automated.scar`, `abb_m4_hattin_data.scar`, `obj_crusaders.scar`, `obj_burningfields.scar`, `obj_tutorial.scar` |
| `abb_m4_hattin_data.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar` |
| `abb_m4_hattin_automated.scar` | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/modules/module_rovingarmy.scar`; conditionally: `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |
| `obj_crusaders.scar` | `abb_m4_hattin.scar`, `abb_m4_hattin_data.scar` |
| `obj_burningfields.scar` | `abb_m4_hattin.scar`, `abb_m4_hattin_data.scar` |
| `obj_tutorial.scar` | `abb_m4_hattin.scar` |

### Shared Globals

- **Player handles:** `player1`–`player8` (defined in `Mission_SetupPlayers`, used everywhere)
- **Difficulty table:** `t_difficulty` (defined in `abb_m4_hattin_data.scar`, read by all objective files)
- **Crusader data:** `t_crusaderData`, `t_crusaderLocations` (built in `obj_crusaders.scar`, used by tutorial/automated)
- **Field data:** `t_burnableFields`, `i_highestNumBurnableFields` (built in `obj_burningfields.scar`, read by crusader pathing)
- **SGroups:** `sg_crusaders`, `sg_tutorial_infantry`, `sg_tutorial_ranged`, `sg_saladin_forces`, `sg_playerUnitsDisabled`, `sg_scuttle_removed`, `sg_allies_roadblock`, `sg_crusaders_reynald`, `sg_extra_spearmen`
- **EGroups:** `eg_playerBuildingsDisabled`, `eg_burnableFieldsTut1/2`, `eg_burnableFields_*`, `eg_houseofwisdom`, `eg_tiberias_walls`
- **Wave tracking:** `g_crusaderWaveTotal`, `g_crusaderWavesKilled`, `g_crusaderCurrentWave`, `t_waveSGroups`, `g_currentCrusaderIdx`, `b_allCrusadersSpawned`
- **Constants:** `CRUSADERS_USE_AI`, `CRUSADER_PURSUIT_TIME/LEASH/FOCUS`, `CRUSADER_STOP_WAIT_TIME`, `CRUSADER_INCOMING_ANIMATION_TIME`, `WAVE_BUFFER`, `NONCOMBAT_WALK_SPEED`, `TROOP_TRAINING_TARGET`, `PRODUCTION_QUEUE_TARGET/WARNING_TIME`

### Inter-File Calls

- `abb_m4_hattin.scar` → `Hattin_InitData()`, `BurnTutorial_InitObjectives()`, `Crusaders_InitObjectives()`, `BurnableFields_Init()`, `AutoTest_OnInit()`, `BurnTutorial_Start()`
- `obj_crusaders.scar` → `BurnableFields_GetField()`, `BurnableFields_HasBeenBurned()`, `BurnableFields_CountFieldsOnFire()`, `BurnableFields_UpdateHint()`, `Hattin_SpawnBarricadeAllies()`, `Hattin_ReinforceAsNeeded()`, `Tutorial_CheckForQueueGuidanceStart()`
- `obj_tutorial.scar` → `Crusaders_SpawnUnits()`, `Crusaders_ForceMarchNext()`, `Crusaders_StartManager()`, `Crusaders_UpdateLocationWaitTime()`, `Crusaders_GetGroup()`, `Crusaders_UpdateFullPath()`, `BurnableFields_GetField()`, `BurnableFields_HasBeenBurned()`, `BurnableFields_Activate()`, `BurnableFields_GetOnFirePercentage()`, `BurnableFields_Terminate()`, `BurnableFields_UpdateHint()`, `Hattin_SpawnBarricadeAllies()`
- `obj_burningfields.scar` → reads `sg_crusaders`, `t_burnableFields`, `t_difficulty` smoke/debuff values; references `TOBJ_BurnableFields`, `SOBJ_FirstTutorialCombat` from objectives
- `abb_m4_hattin_automated.scar` → references `OBJ_Tutorial`, `OBJ_Crusaders`, `OBJ_FieldScoutingGuidance`, `BurnableFields_GetField()`, `BurnableFields_HasBeenBurned()`, `BurnableFields_GetOnFirePercentage()`
