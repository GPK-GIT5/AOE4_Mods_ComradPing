# Abbasid Mission 7: Acre

## OVERVIEW

Abbasid Mission 7 is a large-scale siege assault where the player (Mamluk Sultanate, player1) must destroy all Frankish Keeps (player2) in the city of Acre while defending their own Siege Camp from counter-attacks. The player controls a unique Siege Camp entity with a map-wide barrage ability, receives allied NPC support (player3), and faces escalating enemy waves including timed Genoese naval landings after a 1291-second countdown. Difficulty extensively scales unit counts, wave timers, counter-attack intensity, and whether naval flanking threats are active (Hard/Expert only). The mission uses the Army system for both defenders and attackers, with amortized spawning to spread initial load across frames.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m7_acre.scar` | core | Main mission script: player/variable setup, restrictions, recipe, mission start/flow, resource drops, debug helpers |
| `abb_m7_acre_data.scar` | data | Difficulty tables (`Util_DifVar`), marker collection, enemy/allied army initialization, attack wave composition, Genoese naval attack setup, player/allied unit spawning |
| `abb_m7_acre_objectives.scar` | objectives | Defines and registers all objectives (OBJ_DefendSiegeCamp, OBJ_DestroyCrusaders, OBJ_Genoese), keep tracking UI, siege camp health monitor |
| `abb_m7_acre_attackcycle.scar` | spawns | Counter-attack logic, barrage ability monitoring, enemy reinforcement loop |
| `abb_m7_acre_training.scar` | training | Tutorial goal sequences for Relic pickup and Siege Camp barrage (Easy/Normal only) |
| `abb_m7_acre_automated.scar` | automated | Automated testing: AI-controlled player, checkpoint registration, roving army test flow |

---

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_SetupPlayers` | acre.scar | Configure 3 players, colours, relationships, shared LOS |
| `Mission_SetupVariables` | acre.scar | Grant tech upgrades per difficulty, init barrage abilities, lighthouse setup |
| `Mission_SetDifficulty` | acre.scar | Calls `Init_Acre_Difficulty()` |
| `Mission_SetRestrictions` | acre.scar | Lock House of Wisdom wings, remove walls/keeps/bombards/trade from player production |
| `Mission_Preset` | acre.scar | Init marker armies, objectives, allied units, animator states, food reserves |
| `Mission_Start` | acre.scar | Start objectives, launch first attack wave, begin reinforcement/counter-attack timers, resource drops, naval rules on Hard+ |
| `GetRecipe` | acre.scar | Return MissionOMatic recipe with intro/outro NIS and title card |
| `_Monitor_Enemy_Replacements` | acre.scar | Respawn destroyed enemy army at nearest surviving keep |
| `_Monitor_Enemy_Naval_Replacements` | acre.scar | Respawn destroyed naval army at nearest surviving dock |
| `_Monitor_Ship_Resource_Drops` | acre.scar | Drop wood pickup on enemy ship death (frequency scaled by difficulty) |
| `_Monitor_Land_Resource_Drops` | acre.scar | Drop stone pickups on enemy building death (count scaled by difficulty) |
| `Get_ValidEnemySpawn` | acre.scar | Return closest surviving Crusader keep as spawn point |
| `Get_ValidEnemySpawn_Naval` | acre.scar | Return closest surviving enemy dock as naval spawn point |
| `Mission_TrickleResources` | acre.scar | Per-second gold/food/wood trickle based on difficulty (disabled in final code) |
| `_Control_AlliedArmy` | acre.scar | Redirect allied army toward banner entity position |
| `Init_Acre_Difficulty` | data.scar | Build `t_difficulty` table with all `Util_DifVar` parameters |
| `Acre_InitTuningValues` | data.scar | Init `Acre_EnemyArmies` category tables, distance-sorted army lists, counter-attack globals |
| `Acre_MarkerData` | data.scar | Collect all marker arrays for infantry, archers, cavalry, ships, patrols, allied, Genoese |
| `Acre_InitMarkerArmies` | data.scar | Amortized spawn of all enemy armies (ships, infantry, archers, anti-siege, holy orders, cavalry patrols) |
| `_Amoritize_EnemySpawns` | data.scar | OneShot callback: init Army/NavalArmy, record distance, insert into sorted tables |
| `Sort_Enemy_Tables_Distances` | data.scar | Sort all army/navy lists by distance to siege camp, start counter-attack timer |
| `Acre_LaunchAttack` | data.scar | Spawn cyclic enemy+allied attack waves from sequenced composition tables |
| `AllyTargetClosestKeep` | data.scar | Redirect completed allied wave army toward nearest surviving keep |
| `Init_GenoeseAttack` | data.scar | Spawn Genoese transport fleets with crossbowmen and escort hulks |
| `_GenoeseAttack_TransitionToLand` | data.scar | Convert Genoese naval army to land attack targeting siege camp |
| `Acre_InitPlayerUnits` | data.scar | Spawn player starting military units and assign villagers to resources |
| `Acre_InitAlliedUnits` | data.scar | Spawn allied defensive spearmen and archers at marker positions |
| `Replace_Allied_Units` | data.scar | Recursive self-scheduling respawn of dead allied defense armies |
| `Init_StoryModeItems` | data.scar | Spawn tutorial relic and imam (Easy only) |
| `_Monitor_WaterRuins` | data.scar | Check player villagers near naval landing, trigger transport spawning |
| `_Monitor_NavyTransports` | data.scar | Rebuild enemy transport ships up to difficulty max |
| `SpawnEnemy_FrankishMarines` | data.scar | Load infantry into transports, launch naval landing attack |
| `_RuinsAttack_TransitionToLand` | data.scar | Convert landed marines to land army targeting siege camp |
| `Flank_Warning` | data.scar | CTA/minimap blip when enemy transports approach naval landing |
| `Difficulty_Split` | data.scar | Return one of two values based on difficulty threshold |
| `Acre_InitObjectives` | objectives.scar | Define and register all 3 objectives |
| `_Monitor_Genoese_Timer` | objectives.scar | Watch countdown; on expiry trigger Genoese intel event and attack |
| `Update_KeepMarkers` | objectives.scar | Add UI markers to keeps (Easy: immediately; others: when ≤3 remain) |
| `Monitor_KeepVisbility` | objectives.scar | Per-keep visibility check to add UI marker on first sight (Hard+) |
| `AddKeepUIMarker` | objectives.scar | Attach objective UI element to a keep entity |
| `_KeepIsDead` | objectives.scar | Remove UI marker when keep is destroyed |
| `_Monitor_SiegeCampHealth` | objectives.scar | Trigger danger VO/ping when siege camp health < 70% |
| `COUNTER_ATTACK` | attackcycle.scar | Select nearest non-empty armies, redirect them to siege camp, escalate amount |
| `_Monitor_Barrage_Used` | attackcycle.scar | Detect barrage ability use, disable visuals, schedule refresh |
| `_Monitor_Barrage_Refreshed` | attackcycle.scar | Re-enable barrage visuals after 60s cooldown |
| `Loop_EnemyReinforcementSpawn` | attackcycle.scar | Call `_Monitor_Enemy_Replacements` multiple times for burst reinforcement |
| `Acre_Tutorials_Init` | training.scar | Start relic and siege camp tutorial sequences |
| `MissionTutorial_Relic` | training.scar | Training goal: teach relic deposit into mosques via Imams |
| `MissionTutorial_SiegeCamp` | training.scar | Training goal: teach siege camp barrage ability |
| `AutoTest_OnInit` | automated.scar | Entry point for campaign auto-test: AI control, checkpoints |
| `AutomatedAcre_Phase1_CheckPlayStart` | automated.scar | Wait for OBJ_DestroyCrusaders, then launch roving army test |
| `Player_RovingArmy` | automated.scar | Create test attack + defense roving armies for auto-test |

---

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DefendSiegeCamp` | `OT_Information` | Protect the Siege Camp; failure = mission loss (`Mission_Fail`) |
| `OBJ_DestroyCrusaders` | `ObjectiveType_Primary` | Destroy all Frankish Keeps; completion = mission win (`Mission_Complete`); counter tracks destroyed/total |
| `OBJ_Genoese` | `ObjectiveType_Battle` | 1291-second countdown timer; on expiry spawns Genoese crossbowmen fleet; tracks remaining Genoese count |

### Difficulty

All values use `Util_DifVar({Easy, Normal, Hard, Expert})`:

**Player Mods (`t_difficulty.playerMods`)**

| Parameter | Easy | Normal | Hard | Expert | What it scales |
|-----------|------|--------|------|--------|----------------|
| `STARTING_SPEARMEN` | 20 | 20 | 20 | 20 | Initial spearman count |
| `STARTING_ARCHERS` | 20 | 20 | 20 | 30 | Initial archer count |
| `STARTING_HORSEMEN` | 12 | 12 | 12 | 12 | Initial horseman count |
| `STARTING_MANATARMS` | 20 | 20 | 10 | 10 | Initial men-at-arms count |
| `STARTING_KNIGHTS` | 20 | 20 | 16 | 10 | Initial knight count |
| `STARTING_MANGONELS` | 4 | 3 | 3 | 2 | Initial mangonel count |
| `STARTING_TREBUCHETS` | 3 | 2 | 2 | 1 | Initial trebuchet count |
| `STARTING_VILLAGERS` | 11 | 9 | 7 | 4 | Wood-gathering villagers |
| `BERRY_VILLAGERS` | 5 | 3 | 0 | 0 | Berry-gathering villagers (Easy/Normal only; mill removed on Hard+) |
| `RES_TRICKLE_AMOUNT` | 800 | 500 | 500 | 300 | Gold/food/wood trickle per minute (disabled in shipped code) |
| `ALLY_RESPAWN_DELAY` | 2 | 5 | 6 | 10 | Seconds before allied defense respawn check |
| `RES_PICKUP_SPAWN_CHANCE_NAVAL` | 1 | 1 | 2 | 4 | Ship kills per wood pickup (lower = more frequent) |
| `RES_PICKUP_SPAWN_AMOUNT_LAND` | 3 | 3 | 2 | 1 | Stone pickups per building kill |

**Enemy Mods (`t_difficulty.enemyMods`)**

| Parameter | Easy | Normal | Hard | Expert | What it scales |
|-----------|------|--------|------|--------|----------------|
| `ACRE_COMMON_INFANTRY_SIZE` | 4 | 4 | 4 | 6 | Spearmen per defender group |
| `ACRE_COMMON_INFANTRY_SGT` | 0 | 1 | 2 | 3 | Men-at-arms sergeants per infantry group |
| `ACRE_ELITE_INFANTRY_SIZE` | 4 | 4 | 4 | 6 | Elite infantry per defender group |
| `ACRE_ELITE_INFANTRY_SGT` | 0 | 1 | 2 | 3 | Teutonic elite per elite group |
| `ACRE_ARCHER_SIZE` | 4 | 5 | 6 | 8 | Archers per wall garrison |
| `ACRE_ANTISIEGE_ENGINE_SIZE` | 0 | 1 | 1 | 2 | Springalds per anti-siege point |
| `ACRE_ANTISIEGE_GUARD_SIZE` | 0 | 2 | 4 | 8 | Guards per anti-siege point |
| `ACRE_CAVALRY_PATROL_SIZE` | 4 | 4 | 4 | 6 | Horsemen per patrol |
| `ACRE_CAVALRY_PATROL_SGT` | 0 | 1 | 2 | 3 | Knights per patrol |
| `ACRE_SHIP_SIZE` | 3 | 2 | 3 | 4 | Galleys per ship group |
| `ACRE_ELITE_SHIP_SIZE` | 0 | 1 | 1 | 2 | Hulks per ship group |
| `ACRE_GENOESE_CROSSBOWS_PERBOAT` | 10 | 9 | 6 | 5 | Genoese crossbowmen per transport |
| `ACRE_GENOESE_SGT_PERBOAT` | 0 | 1 | 1 | 2 | Men-at-arms per Genoese transport |
| `ACRE_GENOESE_TRANSPORTS_PERSPAWN` | 1 | 1 | 2 | 4 | Transport ships per spawn point |
| `ACRE_ENEMY_REINFORCEMENT_TIMER` | 120 | 60 | 40 | 35 | Seconds between enemy army respawns |
| `ACRE_ENEMY_NAVAL_REINFORCEMENT_TIMER` | 0 | 0 | 240 | 180 | Seconds between naval reinforcements (Hard+ only) |
| `ACRE_ATTACK_WAVE_TIMER` | 120 | 120 | 90 | 90 | Seconds between attack waves |
| `ACRE_ATTACK_WAVE_DELAY` | 180 | 180 | 120 | 120 | Initial delay before first wave (unused in final code) |
| `COUNTER_ATTACK_TIMER` | 600 | 400 | 300 | 300 | Seconds between counter-attacks on siege camp |
| `COUNTER_ATTACK_INITIAL_AMOUNT` | 4 | 4 | 6 | 6 | Number of armies redirected per counter-attack |
| `COUNTER_ATTACK_RAMP_AMOUNT` | 0 | 0.5 | 1 | 1.5 | Additional armies per subsequent counter-attack |
| `NAVAL_ATTACK_TIMER` | 0 | 0 | 120 | 120 | Seconds between Frankish marine landings (Hard+ only) |
| `NAVAL_TRANSPORT_REBUILD` | 0 | 0 | 360 | 240 | Seconds between transport ship rebuilds (Hard+ only) |
| `NAVAL_MAX_TRANSPORTS` | 0 | 0 | 4 | 5 | Maximum simultaneous transports |

### Spawns

- **Initial enemy armies**: Spawned via amortized `Rule_AddOneShot` calls at 0.005s intervals to spread load. Categories: common infantry, elite infantry, archers, anti-siege (militia on Easy, springalds on Hard+), Templars, Hospitallers, Teutons, cavalry patrols, ship defenders, ship patrols.
- **Attack waves**: Cyclic sequence of MELEE/RANGED/CAVALRY/SIEGE/MILITIA compositions. Enemy waves target siege camp via `WARPATH_ENEMY_LEFT/RIGHT`; allied counter-waves mirror with reversed difficulty compositions. Wave army targets chosen based on player unit density near siege camp.
- **Counter-attacks**: Periodic redirection of nearest non-empty existing armies toward siege camp; amount escalates by `COUNTER_ATTACK_RAMP_AMOUNT` each cycle. Triggers burst reinforcement spawns proportional to counter-attack size.
- **Genoese naval assault**: After 1291s countdown, transport fleets spawn at `mkr_geneose_spawn` markers carrying crossbowmen. On Easy, only odd-numbered spawn points used. Transports land at closest `mkr_genoese_landing`, then transition to land army targeting siege camp.
- **Frankish marines (Hard+ only)**: Periodic transport rebuild + marine loading. Infantry loaded into transports near `mkr_naval_spawn`, land at `mkr_naval_landing`, then attack resources/siege camp.
- **Enemy reinforcements**: Dead defender armies respawn at nearest surviving keep on a timer.
- **Player starting units**: Military at siege camp, villagers assigned to gold/wood/berries per difficulty.
- **Allied defense**: Spearman and archer groups at defensive markers; self-healing respawn system via recursive `Rule_AddOneShot`.

### AI

- **AI_Enable**: Only in automated test (`AutoTest_OnInit`) — player1 given AI control via `Game_AIControlLocalPlayer()` + `AI_Enable(player1, true)`.
- **No general AI_Enable for player2/player3**: Enemy and ally behavior driven entirely by Army system (patrol, attack-move, target waypoints) rather than strategic AI.
- **Patrol logic**: Cavalry patrols use 3 waypoint sets (`mkr_cavalry_patrol_1/2/3`) with `TARGET_ORDER_PATROL`. Ship patrols use 2 waypoint sets (`mkr_ship_patrol_1/2`).
- **Army targeting**: Armies use `Army_Init` with `targets` (marker chains), `TARGET_ORDER_LINEAR` for attack waves, `TARGET_ORDER_PATROL` for patrols. `Army_SetTarget` used for counter-attack redirection.
- **Allied waves**: Capped at 50 spawned units (`sg_allied_wave_pop_count`). On completion, redirected to closest surviving keep via `AllyTargetClosestKeep`.

### Timers

| Timer | Type | Interval/Delay | Purpose |
|-------|------|-----------------|---------|
| `Acre_LaunchAttack` | `Rule_AddInterval` | `ACRE_ATTACK_WAVE_TIMER` (90–120s) | Spawn cyclic enemy + allied attack waves |
| `_Monitor_Enemy_Replacements` | `Rule_AddInterval` | `ACRE_ENEMY_REINFORCEMENT_TIMER` (35–120s) | Respawn destroyed defender armies |
| `COUNTER_ATTACK` | `Rule_AddInterval` | `COUNTER_ATTACK_TIMER` (300–600s) | Redirect armies to siege camp |
| `_Monitor_Enemy_Naval_Replacements` | `Rule_AddInterval` | `ACRE_ENEMY_NAVAL_REINFORCEMENT_TIMER` (180–240s) | Respawn destroyed naval armies (Hard+) |
| `SpawnEnemy_FrankishMarines` | `Rule_AddInterval` | `NAVAL_ATTACK_TIMER` (120s) | Load/launch marine transports (Hard+) |
| `_Monitor_WaterRuins` | `Rule_AddInterval` | `NAVAL_TRANSPORT_REBUILD` (240–360s) | Rebuild enemy transport ships (Hard+) |
| `Flank_Warning` | `Rule_AddInterval` | 1s | Check transport proximity for CTA warning (Hard+) |
| `Flank_Warning_Cooldown` | `Rule_AddOneShot` | 45s | Re-enable flank warning after cooldown |
| `_Monitor_Barrage_Refreshed` | `Rule_AddOneShot` | 60s | Re-enable barrage visual indicators after use |
| `Replace_Allied_Units` | `Rule_AddOneShot` | `ALLY_RESPAWN_DELAY` (2–10s) | Recursive allied defense respawn |
| `Acre_AutoSaveInterval` | `Rule_AddInterval` | 600s | Trigger autosave every 10 minutes |
| `VOCue_MissionStart_Acre` | `Rule_AddOneShot` | 15s | Delay mission start VO after intro camera |
| `Acre_Tutorials_Init` | `Rule_AddOneShot` | 5s | Start tutorials (Easy/Normal) |
| `_Monitor_SiegeCampHealth` | `Rule_AddInterval` | 2s | Watch siege camp health for danger warning |
| `_Monitor_Genoese_Timer` | `Rule_AddInterval` | 1s | Watch Genoese countdown timer |
| `Update_KeepMarkers` | `Rule_AddInterval` | 1s | Track keep visibility/count for UI markers |
| `Barrage_Activate` (autotest) | `Rule_AddInterval` | 30s | Auto-fire barrage in automated testing |

---

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `abb_m7_acre.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`, `MissionOMatic/missionomatic_upgrades.scar`, `abb_m7_acre_data.scar`, `abb_m7_acre_attackcycle.scar`, `abb_m7_acre_objectives.scar`, `abb_m7_acre.events`, `abb_m7_acre_automated.scar`, `abb_m7_acre_training.scar` |
| `abb_m7_acre_data.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar` |
| `abb_m7_acre_attackcycle.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`, `gameplay/event_cues.scar` |
| `abb_m7_acre_objectives.scar` | `MissionOMatic/MissionOMatic.scar` |
| `abb_m7_acre_training.scar` | `training/campaigntraininggoals.scar` |
| `abb_m7_acre_automated.scar` | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/modules/module_rovingarmy.scar`, `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals

| Global | Set In | Used In |
|--------|--------|---------|
| `player1`, `player2`, `player3` | acre.scar (`Mission_SetupPlayers`) | All files |
| `t_difficulty` | data.scar (`Init_Acre_Difficulty`) | data.scar, attackcycle.scar, acre.scar, objectives.scar |
| `All_Army_Distance_Sorted` | data.scar (`Acre_InitTuningValues`) | data.scar, attackcycle.scar, acre.scar |
| `All_Navy_Distance_Sorted` | data.scar (`Acre_InitTuningValues`) | data.scar, acre.scar |
| `counterAttackAmount` | data.scar (`Acre_InitTuningValues`) | attackcycle.scar (`COUNTER_ATTACK`) |
| `lastCounterAttackTime` | data.scar (`Acre_InitTuningValues`) | attackcycle.scar (`COUNTER_ATTACK`) |
| `eg_siegecamp` | prefab (world) | attackcycle.scar, objectives.scar, training.scar, acre.scar |
| `eg_crusaderkeeps` | prefab (world) | objectives.scar, data.scar, acre.scar, automated.scar |
| `bBarrageUsed` | acre.scar (init `false`) | attackcycle.scar (`_Monitor_Barrage_Used`, `COUNTER_ATTACK`), training.scar |
| `sg_all_enemy_ships` | acre.scar (init) | data.scar, acre.scar |
| `OBJ_DefendSiegeCamp` | objectives.scar | acre.scar (`Mission_Start`) |
| `OBJ_DestroyCrusaders` | objectives.scar | acre.scar, automated.scar |
| `OBJ_Genoese` | objectives.scar | acre.scar (`Mission_Start`) |
| `Acre_EnemyArmies` | data.scar | data.scar (sub-tables populated by `_Amoritize_EnemySpawns`) |
| `Allied_Defense_Armies` | data.scar (`Acre_InitAlliedUnits`) | data.scar (`Replace_Allied_Units`) |
| `EVENTS` | acre.events (event file) | objectives.scar, attackcycle.scar, acre.scar |
| `debug_bGenoeseSkip` | acre.scar | objectives.scar (`_Monitor_Genoese_Timer`) |
| `sg_genoese` / `sg_genoese_ships` | data.scar (`Init_GenoeseAttack`) | objectives.scar (`OBJ_Genoese.IsComplete`) |
| `ABILITY_BARRAGE` / `ABILITY_SMALL_BARRAGE` | acre.scar | attackcycle.scar (`_Monitor_Barrage_Used`) |
| `VOPlayed_FirstBarrage_CTA` | (init assumed) | attackcycle.scar (`COUNTER_ATTACK`) |
| `VOPlayed_FirstKeepSpotted` | (init assumed) | objectives.scar (`AddKeepUIMarker`) |
| `bFirstFlank` | acre.scar | data.scar (`Flank_Warning`) |
| `acre_global_spawn_delay` | (external/optional) | data.scar (`Acre_InitMarkerArmies`) |

### Inter-File Function Calls

| Caller File | Calls | Defined In |
|-------------|-------|------------|
| acre.scar | `Init_Acre_Difficulty()` | data.scar |
| acre.scar | `Acre_InitMarkerArmies()` | data.scar |
| acre.scar | `Acre_InitObjectives()` | objectives.scar |
| acre.scar | `Acre_InitAlliedUnits()` | data.scar |
| acre.scar | `AutoTest_OnInit()` | automated.scar |
| acre.scar | `Acre_LaunchAttack()` | data.scar |
| acre.scar | `_Monitor_Enemy_Replacements()` | acre.scar (also called from attackcycle.scar via `Loop_EnemyReinforcementSpawn`) |
| acre.scar | `_Monitor_WaterRuins()` | data.scar |
| acre.scar | `SpawnEnemy_FrankishMarines()` | data.scar |
| acre.scar | `Flank_Warning()` | data.scar |
| acre.scar | `Monitor_KeepVisbility()` | objectives.scar |
| acre.scar | `Init_StoryModeItems()` | data.scar |
| attackcycle.scar | `_Monitor_Enemy_Replacements()` | acre.scar |
| objectives.scar | `Init_GenoeseAttack()` | data.scar |
| objectives.scar | `Mission_Fail()` / `Mission_Complete()` | MissionOMatic |
| automated.scar | `Army_Init()` / `Army_AddSGroup()` | MissionOMatic/module_rovingarmy |
| data.scar | `Army_Init()` / `NavalArmy_Init()` | MissionOMatic |
| data.scar | `EventCues_CallToAction()` | gameplay/event_cues.scar |
| training.scar | `Training_Goal()` / `Training_GoalSequence()` / `Training_AddGoalSequence()` | training/campaigntraininggoals.scar |
