# Angevin Chapter 3: Wallingford

## OVERVIEW

Wallingford (1153) is a defensive siege mission where the player controls Matilda (player1, English, Castle Age) against Stephen (player2, English, Castle Age). The player must defend the town of Wallingford from escalating multi-lane assault waves arriving from three directions (NE, N, NW), survive until Henry's reinforcements arrive after a 600-second countdown, then counterattack to destroy 4 enemy outpost camps, and finally defeat a converging final attack wave. The mission features a MissionOMatic-driven wave system with progressive unit compositions that scale across 4 difficulty tiers, enemy reinforcement mechanics that backfill depleted defenders, and multiple training hint sequences teaching repair, wall garrison, tower building, and keep upgrades.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp3_wallingford.scar` | core | Main mission script: player setup, imports, preset spawns, game logic, wave scheduling, reinforcement flow |
| `ang_chp3_wallingford_data.scar` | data | All constants, timing values, wave unit tables, spawn paths, MissionOMatic module references, recipe definition |
| `ang_chp3_wallingford_objectives.scar` | objectives | Defines OBJ_Defend, OBJ_Survive, OBJ_DestroyOutposts, OBJ_Eliminate_Units with completion/fail logic |
| `obj_defend.scar` | objectives (template) | Earlier/alternate defend objective definition (landmark-based fail condition) |
| `obj_eliminate.scar` | objectives (template) | Earlier/alternate camp-destruction objective with sub-objectives and debug complete |
| `obj_eliminate_waves.scar` | objectives (template) | Earlier/alternate final unit-elimination objective with unit count tracking |
| `obj_survive.scar` | objectives (template) | Earlier/alternate survive-timer objective deploying bulk reinforcements |
| `training_wallingford.scar` | training | Training hint goal sequences: repair buildings, garrison walls, build towers, keep upgrades, incendiary arrows |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Wallingford_InitData1()` | data | Init globals, timing constants, spawn_info, path targets, EGroups/SGroups |
| `Wallingford_InitData2()` | data | Cache MissionOMatic module refs, defender/camp data, reinforcement sources |
| `Wallingford_LoadUnitTables()` | data | Define all difficulty-scaled unit compositions for defenders, patrols, waves |
| `GetRecipe()` | data | Return MissionOMatic recipe with all modules, audio, title card |
| `SetupWaves()` | data | Create Wave objects for NE/N/NW lanes with assault data and build-time overrides |
| `Wallingford_InitObjectives()` | objectives | Register OBJ_Defend, OBJ_DestroyOutposts, OBJ_Eliminate_Units, OBJ_Survive |
| `SpawnReinforcements()` | objectives | Deploy Henry's player reinforcements (knights, MAA, archers) across 7 markers |
| `GetSpawnCount()` | objectives | Return min(remaining pop to 200, 9) for reinforcement batch sizing |
| `UpdateCampsRemaining()` | objectives | Track destroyed camps, update counter, trigger intel events |
| `UpdateUnitsRemaining()` | objectives | Sum all enemy module squad counts for final-wave progress tracking |
| `HenryReminder()` | objectives | Repeat CTA event every 90s until player interacts with reinforcements |
| `MonitorHenry()` | objectives | Check if player has seen/selected reinforcement squads |
| `Mission_SetupPlayers()` | core | Set player names (Matilda/Stephen), Castle Age, colours |
| `Mission_Preset()` | core | Deploy starting army, assign villagers, set resources, remove upgrades, launch wave 1 |
| `Mission_Start()` | core | Set resources by difficulty, schedule all wave timers, start mainloop |
| `Wallingford_LaunchIntroWave()` | core | Manually launch intro assault wave for a given wave_number/lane |
| `Wallingford_TryPrepare()` | core | Choose a valid lane and prepare the next wave if outposts not yet destroyed |
| `Wallingford_PrepareWave()` | core | Set units on a Wave, call Wave_Prepare, start monitoring the assault module |
| `ChooseLane()` | core | Select lane with most spawnable categories, avoiding recent repeats |
| `Wallingford_GetWaveUnits()` | core | Cycle through wave_units table, wrapping back 5 from end |
| `Wallingford_OnLaunch()` | core | Callback when a wave auto-launches from staging area |
| `Wallingford_OnComplete()` | core | Callback when assault module reaches staging position |
| `Wallingford_MonitorWave()` | core | Per-second tracking: arrival detection, retreat logic, walla/threat arrows |
| `Wallingford_MonitorEnemyReinforcements()` | core | Check if field defenders reduced to half, trigger reinforcement rounds |
| `ReinforceFirst()` | core | Dissolve first reinforcement modules into depleted defender modules |
| `ReinforceSecond()` | core | Dissolve second reinforcement modules into depleted defenders |
| `WallsBreached()` | core | Fire WALL_BREACHED intel event on first wall segment death |
| `Wallingford_Mainloop()` | core | Increment mission timer (wallingford_seconds) every second |
| `Wallingford_ReinforcementsArrive()` | core | Complete OBJ_Survive, trigger autosave |
| `Wallingford_ReinforcementsAlmostHere()` | core | Play HENRY_ONEMINUTE intel, shift music to tense |
| `Wallingford_StartOutpostObjective()` | core | Start OBJ_DestroyOutposts 30s after mission start |
| `Wallingford_AddHintToRepair()` | training | Training sequence: right-click damaged building to repair |
| `Wallingford_AddHintToBuildTower()` | training | Training sequence: build stone towers on walls |
| `Wallingford_AddHintToGarrisonWall()` | training | Training sequence: garrison infantry on walls |
| `Wallingford_AddHintToKeep()` | training | Training sequence: research upgrades at the keep |
| `Wallingford_AddHintIncendiaryArrows()` | training | Training sequence: research incendiary arrows at arsenal (disabled) |
| `Wallingford_FindEntityOnScreen()` | training | Find closest on-screen entity of a given scar_type |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Defend` | Primary/Battle | Fail if all player landmarks destroyed → `Mission_Fail()` |
| `OBJ_Survive` | Information | Countdown timer (600s) until Henry's reinforcements arrive |
| `OBJ_DestroyOutposts` | Primary/Battle | Destroy 4 enemy camps; counter tracks progress (0/4); on complete pauses waves, starts final objective |
| `OBJ_Eliminate_Units` | Primary/Battle | Defeat all remaining enemy units (progress bar); awards wall-protection achievement on complete |
| `OBJ_DebugComplete` | Debug | Cheat to instantly complete mission |

**Objective Flow:** `OBJ_Defend` + `OBJ_Survive` active from start → after 30s `OBJ_DestroyOutposts` starts → on 4 camps destroyed → `OBJ_Eliminate_Units` starts (all enemies converge on player base) → on all killed → Outro NIS.

### Difficulty

All values are `Util_DifVar({story, easy, normal, hard})`:

| Parameter | Story | Easy | Normal | Hard |
|-----------|-------|------|--------|------|
| Defender units (spearman) | 5 | 7 | 10 | 14 |
| Defender units (crossbow/archer) | 4–5 | 5–7 | 7–10 | 10–14 |
| Fort defenders (MAA) | 5 | 7 | 10 | 14 |
| Fort defenders (archer) | 7 | 10 | 14 | 20 |
| Fort defenders (mangonel) | 0 | 0 | 1 | 2 |
| Siege patrol (MAA) | 4 | 5 | 7 | 10 |
| Cavalry patrol (knight) | 4 | 5 | 7 | 10 |
| Enemy reinforcements (springald) | 0 | 0 | 1 | 2 |
| Final wave (per unit type) | 9 | 12 | 17 | 24 |
| Knight patrols | 4–5 | 5–7 | 7–10 | 10–14 |
| Player starting villagers (wood) | 6 | 4 | 4 | 4 |
| Player starting villagers (gold) | 4 | 3 | 3 | 3 |
| Player starting villagers (stone) | 2 | 1 | 1 | 1 |
| Player starting resources | 800 each | 800 each | 600 each | 400 each (200 expert) |

Wave unit tables are entirely separate per difficulty: `wave_units_story` (smaller squads, fewer siege), `wave_units_easy`, `wave_units_normal`, `wave_units_hard` (larger squads, more rams/mangonels/springalds).

### Spawns

**Intro Waves (3 scripted):**
- Wave 1 (NE): Launched at mission preset (time 0). Units from `wave_units[1]`.
- Wave 2 (N): Launched at t=100s (`LAUNCH_ATTACK_2`). Units from `wave_units[2]`.
- Wave 3 (NW): Launched at t=225s (`LAUNCH_ATTACK_3`). Units from `wave_units[3]`.

**Ongoing Waves (prepared via `Wallingford_TryPrepare`):**
- Wave 4: ~t=350s, lanes NW/N/NE
- Wave 5: ~t=475s, lanes NW/N/NE
- Wave 6: ~t=675s, lanes NW/N
- Wave 7: ~t=800s, lanes NW/N
- After wave 7: repeating every 125s (`ATTACK_INTERVAL`), all 3 lanes

**Wave Preparation:** `PREPARE_TIME` = 210s for units to build at production buildings. Waves auto-launch 20s after preparation completes. Lane selection avoids repeating the previous lane and prioritizes lanes with the most spawnable building categories.

**Unit Index Cycling:** `wave_unit_index` increments through the wave_units table (10 entries). After exhausting all entries, wraps back to index `#wave_units - 5` for continued variation.

**Wave Compositions (per difficulty, 10 waves each):**
- Waves 1–5: Infantry-heavy (spearmen, MAA, archers, crossbowmen) with rams and siege towers
- Waves 6–10 (post-reinforcement): Add horsemen, knights, mangonels, springalds; larger squad sizes

**Final Wave:** Spawned at `mkr_enemy_spawn_final_wave` when all camps destroyed. Composition: MAA + spearmen + horsemen (9/12/17/24 each by difficulty).

**Player Starting Forces:**
- 9 MAA, 9 archers (garrison), 9 horsemen, 12 wall archers, 2 idle villagers
- 8 food villagers, 4–6 wood, 3–4 gold, 1–2 stone (by difficulty)

**Player Reinforcements (Henry, t=600s):**
- Up to 63 squads: 27 knights (3×9), 18 MAA (2×9), 18 archers (2×9)
- Capped by remaining pop space (batches of min(remaining, 9))
- Max pop increased by 50 on arrival

### AI

**No AI_Enable calls.** All enemy behavior is module-driven via MissionOMatic:

**Defend Modules (static):**
- 3 fort defenders (NE, N, NW) with front-line defenders (2 per direction) using `enemy_defend_fort` / `enemy_defend_front_1` / `enemy_defend_front_2` compositions
- 4 RovingArmy defenders (`enemy_defend_1–4`) at fixed positions with `enemy_defend_units_a/b`

**Patrol Modules:**
- `siege_patrol_1–4`: MAA patrols with random targeting between 3 waypoints, 10–12s idle time
- `siege_patrol_5`: Knight cavalry patrol with reverse targeting across 10 waypoints, 3s idle
- `patrol_1–7`: Additional RovingArmy patrols (knights, horsemen, spearmen+archers, MAA+springalds) with reverse/random targeting

**Enemy Reinforcement System:**
- Monitors 4 defender modules; when any drops below 50% strength → `ReinforceFirst()` (3 sources)
- When a second drops below 50% → `ReinforceSecond()` (2 sources), then monitoring stops
- Reinforcement modules physically move closer before dissolving into defenders

**Assault Modules:**
- Intro assaults (3): attack-move everything, targeting player base via waypoint paths
- Ongoing assaults: staged approach (targets_a → staging area → targets_b after PREPARE_TIME)
- On outposts destroyed: incoming waves retreat to origin; arrived waves redirect to player base

### Timers

| Timer/Rule | Delay | Type | Purpose |
|------------|-------|------|---------|
| `Wallingford_LaunchIntroWave` (wave 1) | 0 (preset) | OneShot | Launch first NE assault wave |
| `Wallingford_LaunchIntroWave` (wave 2) | 100s | OneShot | Launch second N assault wave |
| `Wallingford_LaunchIntroWave` (wave 3) | 225s | OneShot | Launch third NW assault wave |
| `Wallingford_TryPrepare` (wave 4) | 140s (350-210) | OneShot | Prepare wave 4, all lanes |
| `Wallingford_TryPrepare` (wave 5) | 265s (475-210) | OneShot | Prepare wave 5, all lanes |
| `Wallingford_TryPrepare` (wave 6) | 465s (675-210) | OneShot | Prepare wave 6, NW/N only |
| `Wallingford_TryPrepare` (wave 7) | 590s (800-210) | OneShot | Prepare wave 7, NW/N only |
| `Wallingford_TryPrepare` (recurring) | start=590s, every 125s | Interval | Ongoing wave preparation, all lanes |
| `Wallingford_StartOutpostObjective` | 30s | OneShot | Start OBJ_DestroyOutposts |
| `Wallingford_ReinforcementsAlmostHere` | 540s (600-60) | OneShot | "One minute" warning intel + music shift |
| `Wallingford_ReinforcementsArrive` | 600s | OneShot | Complete OBJ_Survive, spawn Henry's army |
| `Wallingford_Mainloop` | every 1s | Interval | Increment mission clock |
| `Wallingford_MonitorEnemyReinforcements` | every 1s | Interval | Check defender health for reinforcement triggers |
| `Wallingford_MonitorWave` | every 1s | Interval | Track each wave module position, arrival, combat state |
| `HenryReminder` | every 90s | Interval | Repeat CTA if player hasn't interacted with reinforcements |
| `Util_AutoSave` | every 600s | Interval | Periodic autosave after reinforcements arrive |
| `WallsBreached` | event-driven | EGroupEvent | Fire wall-breach intel on first wall death |

### Achievement

- `CE_ACHIEVPROTECTWALLSWALLINGFORD`: Awarded if `startingWallDestroyed == false` when OBJ_Eliminate_Units completes (no wall segments killed).

## CROSS-REFERENCES

### Imports
| Import | Source File |
|--------|-------------|
| `MissionOMatic/MissionOMatic.scar` | core |
| `missionomatic/missionomatic_wave.scar` | core |
| `ang_chp3_wallingford_objectives.scar` | core |
| `ang_chp3_wallingford_data.scar` | core |
| `training_wallingford.scar` | core |
| `training.scar` | training_wallingford |
| `training/campaigntraininggoals.scar` | training_wallingford |

### Shared Systems
- **MissionOMatic**: `MissionOMatic_FindModule()`, `RovingArmy_SetTargets()`, `RovingArmy_SetTarget()`, `RovingArmy_AddTargets()`, `Defend_UpdateTargetLocation()`
- **Wave System**: `Wave_New()`, `Wave_FindWave()`, `Wave_Prepare()`, `Wave_Pause()`, `Wave_SetUnits()`, `Wave_OverrideUnitBuildTime()`, `Wave_ValidateSpawns()`, `Wave_GetSpawnableCategories()`
- **UnitEntry**: `UnitEntry_DeploySquads()` for spawning player/enemy units at markers
- **Training**: `Training_Goal()`, `Training_GoalSequence()`, `Training_AddGoalSequence()`, `Training_EnableGoalSequenceByID()`
- **Campaign Training**: `CampaignTraining_TimeoutIgnorePredicate` from `campaigntraininggoals.scar`
- **Objectives**: `Objective_Register()`, `Objective_Start()`, `Objective_Complete()`, `Objective_StartTimer()`, `Objective_SetCounter()`, `Obj_SetProgress()`
- **Music**: `Music_LockIntensity()`, `Music_PlayStinger()`, `Music_PostCombat_End()`, `Sound_SetMinimumMusicCombatIntensity()`
- **Upgrades**: `UPG.COMMON.UPGRADE_RANGED_INCENDIARY`, `UPG.COMMON.UPGRADE_RANGED_ARCHER_SILKSTRING`, `UPG.COMMON.UPGRADE_SIEGE_WEAPON_SPEED`, `UPG.COMMON.UPGRADE_TOWER_SPRINGALD`, `UPG.COMMON.UPGRADE_OUTPOST_STONE`
- **Events**: `EVENTS.AFTER_INTRO`, `EVENTS.SECOND_ATTACK`, `EVENTS.THIRD_ATTACK`, `EVENTS.SECOND_ATTACK_DEFEATED`, `EVENTS.THIRD_ATTACK_DEFEATED`, `EVENTS.WALL_BREACHED`, `EVENTS.HENRY_ONEMINUTE`, `EVENTS.HENRYARRIVES`, `EVENTS.SIEGE_DEFENDERS1`, `EVENTS.SIEGE_DEFENDERS2`, `EVENTS.SIEGE_DEFENDERS3_ASSAULT`, `EVENTS.ANG_ECAM1153WALLINGFORD_Intro`, `EVENTS.ANG_ECAM1153WALLINGFORD_Outro`

### Inter-File Dependencies
- `ang_chp3_wallingford.scar` calls `Wallingford_InitData1()`, `Wallingford_InitData2()`, `SetupWaves()`, `Wallingford_InitObjectives()`, and all training `AddHint` functions
- Objectives file references globals from data file: `camp_data`, `REINFORCEMENTS_DELAY`, `arrived_assault_modules`, `siege_patrol_*`, `enemy_defend_*`, `reinforcements_*`, `final_wave`, `startingWallDestroyed`
- Core file references objectives: `OBJ_Survive`, `OBJ_DestroyOutposts`
- Template files (`obj_defend/eliminate/eliminate_waves/survive.scar`) are earlier iterations; the final mission inlines their logic into `ang_chp3_wallingford_objectives.scar`

### Recipe Configuration
- Campaign: `english`, Chapter: `chapter3`, Phase: `mission_wallingford`
- Audio: campaign `ang`, mission `rts1153wallingford`
- Title Card: Loc 11160640 ("Wallingford"), Date 11160641 ("1153")
- Shroud: enabled
