# Historical Challenge: Towton

## OVERVIEW

Historical Challenge: Towton is a Lancastrian wave-defense mission where the player must defend Castle Lancaster and four allied towns (NW, SW, SE, NE) from escalating Yorkist attacks over ~22.5 minutes. The mission flows through five timed phases: an intro scouting period, then four sequential attack phases each targeting a different allied town, culminating in a massive final boss wave led by the Duke of York. A "Conqueror Mode" unlocks if the player kills two enemy scouts and preserves all outer houses before 5:30, adding extra conqueror-only waves and scaling up unit counts by 1.3x. Beacon towers at each town can be lit (automatically at phase end, or manually by the player attacking them) to call in naval/cavalry reinforcements whose strength scales with how long the town was defended. Medal scoring is based on allied buildings remaining: Gold (35+), Silver (20+), Bronze (survive all), with a separate Conqueror Medal for surviving all strengthened waves.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_towton.scar` | core | Main mission script: player setup, diplomacy, global events, phase transitions, conqueror mode logic, trebuchet attack, destruction/damage handlers, intro/outro, starting units |
| `challenge_towton_obj.scar` | objectives | Defines and registers all OBJ_/SOBJ_ objectives, phase UI with timers/reticules/minimap blips, reinforcement arrival notifications |
| `challenge_towton_waves.scar` | spawns | Defines all enemy wave compositions, paths, spawn timing, wave spawning/tracking, raider split-off logic, siege redirection |
| `challenge_towton_towns.scar` | data | Initializes 4 allied towns + 2 standalone beacons with Army patrols, manor tracking, defender replenishment, beacon lighting, reinforcement spawning/unloading |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | challenge_towton | Initializes all globals, phase times, booleans, counters |
| `Mission_SetupPlayers` | challenge_towton | Creates 7 players with diplomacy and color config |
| `ChallengeMission_SetupDiplomacy` | challenge_towton | Sets ally/enemy relationships including neutral beacon player |
| `Mission_PreInit` | challenge_towton | Registers global events for destruction, damage, construction |
| `Mission_Start` | challenge_towton | Starts objectives, rules, resources, waves, towns, scouts |
| `GetRecipe` | challenge_towton | Returns recipe with intro NIS and audio settings |
| `HC_Towton_SetProduction` | challenge_towton | Completes upgrades, removes palisade/wall from production |
| `HC_Towton_Update` | challenge_towton | Main 0.25s loop: conqueror check, phase transitions, victory/defeat |
| `HC_Towton_UpdateAgeUpHint` | challenge_towton | Shows/completes Castle Age advancement hint objective |
| `HC_Towton_UpdateProductionHint` | challenge_towton | Shows/completes military production building hint objective |
| `HC_Towton_RevealTrebuchet` | challenge_towton | Reveals FOW around conqueror-mode high-ground trebuchet |
| `HC_Towton_UpdateEnemyWood` | challenge_towton | Refreshes enemy wood to 600 every 30s for rams |
| `HC_Towton_HiddenVillagers` | challenge_towton | Spawns 8 villagers when player discovers hidden camp |
| `HC_Towton_RevealNorthBeacon` | challenge_towton | Reveals north beacon when player units near river |
| `HC_Towton_RevealSouthBeacon` | challenge_towton | Reveals south beacon when player units near cliffs |
| `HC_Towton_InitStartingScouts` | challenge_towton | Deploys 2 enemy scouts for conqueror mode qualification |
| `HC_Towton_RetreatStartingScouts` | challenge_towton | Moves scouts back to enemy base at 71s |
| `HC_Towton_RetreatStartingScouts2` | challenge_towton | Fails conqueror if scouts survive at 74s |
| `HC_Towton_SpawnEnemyUnits` | challenge_towton | Deploys static enemy garrison units at forts/camps |
| `HC_Towton_SpawnPlayerUnits` | challenge_towton | Deploys player starting army and villagers with tasks |
| `HC_Towton_OnDestruction` | challenge_towton | Tracks building losses, medals, wall breaches, outpost upgrades |
| `HC_Towton_OnDamaged` | challenge_towton | Detects player attacking beacons to light them early |
| `HC_Towton_OnConstructionComplete` | challenge_towton | Checks age-up and production hints on build complete |
| `HC_Towton_EndChallenge` | challenge_towton | Stores KPI data and triggers victory intel/completion |
| `HC_Towton_IntroSetup` | challenge_towton | Spawns intro raider units for NIS sequence |
| `HC_Towton_IntroTeardown` | challenge_towton | Cleans up intro units and destroyed house |
| `HC_Towton_InitObjectives` | challenge_towton_obj | Registers all objectives, starts timers and initial UI |
| `HC_Towton_InitStartingAttackUI` | challenge_towton_obj | Shows CTA for first enemy scouts at 15s |
| `HC_Towton_InitStartingAttackUI2` | challenge_towton_obj | Starts initial attacks objective with minimap blips at 60s |
| `HC_Towton_InitObjectiveUI` | challenge_towton_obj | Sets up landmark defense UI and building counter |
| `HC_Towton_BeginNewPhase` | challenge_towton_obj | Starts phase objective with timer, reticule, minimap path |
| `HC_Towton_EndOldPhase` | challenge_towton_obj | Completes phase objective, removes UI elements |
| `HC_Towton_UpdateObjectiveUI` | challenge_towton_obj | Updates building count and phase progress bars at 0.5s |
| `HC_Towton_PulseReinforcementsBlipNW` | challenge_towton_obj | Pulses minimap blip for NW reinforcements every 5s |
| `HC_Towton_PulseReinforcementsBlipNE` | challenge_towton_obj | Pulses minimap blip for NE reinforcements every 5s |
| `HC_Towton_PulseReinforcementsBlipSW` | challenge_towton_obj | Pulses minimap blip for SW reinforcements every 5s |
| `HC_Towton_PulseReinforcementsBlipSE` | challenge_towton_obj | Pulses minimap blip for SE reinforcements every 5s |
| `HC_Towton_InitEnemyWaves` | challenge_towton_waves | Defines all wave compositions, paths, timing, icons |
| `HC_Towton_UpdateWaves` | challenge_towton_waves | Spawns waves when mission time reaches spawn threshold |
| `HC_Towton_AddNewWave` | challenge_towton_waves | Creates Army from wave data with dynamic strength scaling |
| `HC_Towton_AnnounceNewWave` | challenge_towton_waves | Displays CTA and plays alert sounds for new waves |
| `HC_Towton_RevealNewWave` | challenge_towton_waves | Reveals wave via FOW after 5s spawn delay |
| `HC_Towton_UpdateWaveSiege` | challenge_towton_waves | Splits siege from armies near walls, redirects to gates |
| `HC_Towton_UpdateWaveSiegeEast` | challenge_towton_waves | Orders east siege to attack gate then TC then landmark |
| `HC_Towton_UpdateWaveSiegeWest` | challenge_towton_waves | Orders west siege to attack gate then TC then landmark |
| `HC_Towton_UpdateWaveRaiders` | challenge_towton_waves | Splits melee units to raid allied town buildings |
| `HC_Towton_PulseThreatBlip` | challenge_towton_waves | Pulses minimap threat blips for waves 10-30s after spawn |
| `HC_Towton_DelayedStartUpdates1` | challenge_towton_waves | Starts raider update rule after 1s delay |
| `HC_Towton_DelayedStartUpdates2` | challenge_towton_waves | Starts east/west siege update rules after 2s delay |
| `HC_Towton_InitTowns` | challenge_towton_towns | Creates townDataTable for 4 towns + 2 beacons with armies |
| `HC_Towton_InitBeacon` | challenge_towton_towns | Converts beacon entity, sets invulnerable props |
| `HC_Towton_InitDefensiveOutposts` | challenge_towton_towns | Creates EGroups for allied outposts per town sector |
| `HC_Towton_UpdateTowns` | challenge_towton_towns | Replenishes town defenders from manor spawns every 15s |
| `HC_Towton_UpdateTownDefenders` | challenge_towton_towns | Merges reinforcements into patrol groups, issues patrol orders |
| `HC_Towton_ManorDestroyed` | challenge_towton_towns | Lights beacon and dissolves army when manor is killed |
| `HC_Towton_LightBeacon` | challenge_towton_towns | Sets beacon on fire, spawns campfires, triggers reinforcements |
| `HC_Towton_LightTower` | challenge_towton_towns | Spawns campfire effects on signal towers with delay |
| `HC_Towton_SpawnAlliedShip` | challenge_towton_towns | Spawns allied Carrack from north beacon activation |
| `HC_Towton_SpawnAlliedReinforcements` | challenge_towton_towns | Spawns scaled naval/cavalry reinforcements per town index |
| `HC_Towton_UnloadAlliedTransportsNW` | challenge_towton_towns | Unloads NW transport ships and rallies troops to town |
| `HC_Towton_UnloadAlliedTransportsNE` | challenge_towton_towns | Unloads NE transport ships and rallies troops to town |
| `HC_Towton_ChangeReinforcementsOwnerSE` | challenge_towton_towns | Transfers SE cavalry from ally to player ownership |
| `HC_Towton_ChangeReinforcementsOwnerSW` | challenge_towton_towns | Transfers SW cavalry from ally to player ownership |
| `HC_Towton_ChangeReinforcementsOwnerS` | challenge_towton_towns | Transfers south beacon cavalry from ally to player |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Victory` | Battle | Primary: Defend against Yorkist attacks (countdown timer to final wave) |
| `OBJ_Towns` | Battle | Sub-objective: Allied Buildings Remaining (progress bar counter) |
| `SOBJ_Defend` | Battle | Sub-objective: Lancaster Stronghold (landmark) must survive |
| `OBJ_ConquerorMedal` | Bonus | Conqueror Medal: survive all strengthened enemy waves |
| `OBJ_GoldMedal` | Bonus | Gold Medal: save 35+ allied buildings |
| `OBJ_SilverMedal` | Bonus | Silver Medal: save 20+ allied buildings |
| `OBJ_BronzeMedal` | Bonus | Bronze Medal: survive all enemy waves |
| `OBJ_Conqueror` | Bonus | Prove ability to defend allies for conqueror unlock |
| `OBJ_InitialAttacks` | Battle | Yorkist scouting attacks testing defenses |
| `SOBJ_AttackPhaseNW` | Battle | Defend Northwest Town until reinforcements arrive |
| `SOBJ_AttackPhaseSW` | Battle | Defend Southwest Town until reinforcements arrive |
| `SOBJ_AttackPhaseSE` | Battle | Defend Southeast Town until reinforcements arrive |
| `SOBJ_AttackPhaseNE` | Battle | Defend Northeast Town until reinforcements arrive |
| `SOBJ_ReinforcementsNW` | Information | NW naval reinforcements have arrived (select to dismiss) |
| `SOBJ_ReinforcementsNE` | Information | NE naval reinforcements have arrived |
| `SOBJ_ReinforcementsSE` | Information | SE cavalry reinforcements have arrived |
| `SOBJ_ReinforcementsSW` | Information | SW cavalry reinforcements have arrived |
| `SOBJ_ReinforcementsS` | Information | South beacon cavalry reinforcements have arrived |
| `OBJ_Boss` | Battle | Defeat the Duke of York's final attack |
| `OBJ_AgeUpHint` | Tip | Advance to Castle Age hint (at 7 min) |
| `OBJ_ProductionHint` | Tip | Build 4+ military production buildings hint (at 8 min) |

### Difficulty / Dynamic Scaling

No `Util_DifVar` calls. Difficulty is managed through dynamic systems:

| Mechanism | What It Scales |
|-----------|---------------|
| Conqueror mode (1.3x multiplier) | All wave unit counts scaled up when conqueror is active |
| `conquerorModeFailed` wave reduction | Boss wave siege units reduced by 0.8x if conqueror not active |
| Manor destruction scaling | Wave unit counts reduced by 0.75x if prior manor destroyed |
| Silver medal failed scaling | Wave unit counts reduced by 0.825x |
| Gold medal failed scaling | Wave unit counts reduced by 0.9x |
| Reinforcement count scaling | Reinforcement army size proportional to defense duration (time/phaseDuration × base) |
| Player combat unit count | Extra reinforcements added if player has <10/15/20/25/30 combat units |
| Outpost auto-upgrade | Allied outposts upgraded to stone+arrowslits when buildings lost (non-conqueror only) |
| Additional reinforcement unit types | Earls Guard and Culverins added to NE reinforcements if medals failed |

### Spawns

**Enemy Wave System:**
- Waves defined in `enemyWavePattern[]` table with unit makeup, path index, conqueror flag, spawn time, and CTA icon
- 9 paths defined (4 main + 1 boss + 4 alternate flanking routes)
- Wave strength = `ceil(missionTime/60) + 10`, multiplied per unit by `waveUnitMultiplier`
- Conqueror mode scales all counts by 1.3x
- ~60+ total waves across 5 phases plus conqueror-only bonus waves interleaved

**Phase Structure:**
- Intro (0–5:30): 6 waves from all 4 directions, spearmen/archers/horsemen/mangonels
- Phase 1 — NW (5:30–10:00): ~12 waves via path 4/9, spearmen → knights → crossbows → siege
- Phase 2 — SW (10:00–14:30): ~12 waves via path 3/8, archers → cavalry → trebuchets
- Phase 3 — SE (14:30–18:30): ~14 waves via path 2/7, upgraded tier-3 units, bombards
- Phase 4 — NE (18:30–22:30): ~10 waves via path 1/6, tier-4 units, heavy siege
- Final Boss (22:40): Massive wave with spearmen4, archers4, MAA4, knights4, crossbows4, mangonels, trebs, ribauldequins, bombards, and the Duke of York leader unit

**Unit Roster (English):** Spearman T2-4, Archer T2-4, Crossbow T3-4, MAA T1-4, Horseman T2-4, Knight T3-4, Mangonel, Springald, Ram, Trebuchet, Bombard, Ribauldequin, Abbey King

**Raider System:** Melee units within 50 range of allied towns are split off (max 2 at a time for main paths, unlimited for flanking paths), transferred to `enemyPlayer2` (AI disabled), and ordered to attack closest allied building. Merged back if town is fully destroyed.

**Siege Redirection:** Siege units (excluding rams) separated from armies near stone walls; redirected to attack gates → TC → landmark sequentially.

**Allied Reinforcements:**
- NW/NE: Naval transports with Earls Guard 4 + Yeoman 4 (NW) or Crossbow 4 + Yeoman 4 (NE), unloaded at shore
- SW/SE: French Knights T3 (SW) or T4 (SE) spawned from south, transferred to player after passing walls
- North beacon: Allied Carrack ship
- South beacon: 4 French Knights T3

### AI

| Setting | Detail |
|---------|--------|
| `AI_Enable(enemyPlayer2, false)` | Second enemy player (raider owner) has AI disabled |
| Enemy pop cap | Set to 999 with `PopulationCapOn = false` |
| Town defender patrol | `Army_Init` with `TARGET_ORDER_PATROL` and `leashBuffer = 30` for 4 allied towns |
| Enemy wave armies | Created via `Army_Init` with `attackMove = true`, `combatRangeEnRoute/AtTarget = 40-50` |
| Alternate path armies | Use per-waypoint target configs with reduced combat range (1-3) to bypass first defense line |

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| `HC_Towton_Update` | 0.25s | Main game loop: conqueror, phases, victory/defeat checks |
| `HC_Towton_UpdateObjectiveUI` | 0.5s | Updates building counter and phase progress bars |
| `HC_Towton_UpdateWaves` | 0.5s | Checks and spawns waves based on mission time |
| `HC_Towton_UpdateWaveSiege` | 5s | Splits siege units near walls from armies |
| `HC_Towton_UpdateWaveRaiders` | 5s | Splits melee raiders near allied towns |
| `HC_Towton_UpdateWaveSiegeEast` | 5s | Orders east-side siege units to attack |
| `HC_Towton_UpdateWaveSiegeWest` | 5s | Orders west-side siege units to attack |
| `HC_Towton_PulseThreatBlip` | 5s | Pulses minimap threat icons for active waves |
| `HC_Towton_UpdateTowns` | 15s | Replenishes allied town defenders from manors |
| `HC_Towton_UpdateTownDefenders` | 5s | Merges reinforcements and issues patrol orders |
| `HC_Towton_UpdateEnemyWood` | 30s | Refreshes enemy wood to 600 for ram building |
| `HC_Towton_HiddenVillagers` | 0.5s | Checks player proximity to hidden villager camp |
| `HC_Towton_RevealNorthBeacon` | 0.5s | Checks player proximity to reveal north beacon |
| `HC_Towton_RevealSouthBeacon` | 0.5s | Checks player proximity to reveal south beacon |
| `HC_Towton_RevealTrebuchet` | 1s | Reveals FOW when conqueror trebuchet is attacking |
| `HC_Towton_BlipStartingScouts` | 7s | Pulses minimap blips for intro enemy scouts |
| `HC_Towton_InitStartingAttackUI` | OneShot 15s | Shows CTA for first enemy scouts |
| `HC_Towton_InitStartingAttackUI2` | OneShot 60s | Starts initial attacks objective with minimap blips |
| `HC_Towton_RetreatStartingScouts` | OneShot 71s | Retreats enemy scouts back to base |
| `HC_Towton_RetreatStartingScouts2` | OneShot 74s | Fails conqueror mode if scouts still alive |
| `HC_Towton_RetreatLeader` | OneShot 15s | Retreats conqueror mode leader reveal unit |

### Phase Timing

| Phase | Start Time | Duration | Target Town |
|-------|-----------|----------|-------------|
| Intro | 0:00 | 5:30 | All four towns |
| Phase 1 | 5:30 | 5:00 | Northwest |
| Phase 2 | 10:00 | 5:00 | Southwest |
| Phase 3 | 14:30 | 5:00 | Southeast |
| Phase 4 | 18:30 | 4:00 | Northeast |
| Final Boss | 22:40 | Until cleared | Main base |

### Medal System

| Medal | Condition |
|-------|-----------|
| Conqueror Medal | Conqueror mode active + survive all strengthened waves |
| Gold Medal | Save 35+ allied buildings (≤5 lost) |
| Silver Medal | Save 20+ allied buildings (≤20 lost) |
| Bronze Medal | Survive all enemy waves |

### Beacon System

- 6 beacons total: 4 at allied towns (NE, SE, SW, NW) + north river beacon + south cliff beacon
- Town beacons activate automatically when phase timer expires, or early if player attacks the beacon entity
- Manor destruction also triggers the corresponding town's beacon
- Beacon lighting: sets beacon tent on fire, spawns campfire entities, lights signal towers with staggered 2s delays
- North beacon spawns an allied Carrack; south beacon spawns 4 French Knights
- Town beacons spawn scaled reinforcements (naval transports NW/NE, cavalry SW/SE)

## CROSS-REFERENCES

### Imports

All files import:
- `MissionOMatic/MissionOMatic.scar` — Cardinal mission framework
- `missionomatic/missionomatic_artofwar.scar` — Art of War challenge utilities
- `training/coretraininggoals.scar` — Training system
- `cardinal.scar` — Core engine API

Additional imports in `challenge_towton.scar`:
- `MissionOMatic/MissionOMatic_utility.scar` — Utility functions
- `challenge_towton.events` — Event/intel definitions
- `challenge_towton_obj.scar` — Objective definitions
- `challenge_towton_waves.scar` — Wave definitions
- `challenge_towton_towns.scar` — Town/beacon definitions

### Shared Globals

| Global | Set In | Used In |
|--------|--------|---------|
| `conquerorModeActivated` | challenge_towton | challenge_towton_obj, challenge_towton_waves, challenge_towton_towns |
| `conquerorModeFailed` | challenge_towton | challenge_towton_waves |
| `missionTime` | challenge_towton | challenge_towton_waves |
| `phase1-5StartTime` | challenge_towton | challenge_towton_obj, challenge_towton_waves |
| `enemyWavePattern[]` | challenge_towton_waves | challenge_towton_waves (internal) |
| `townDataTable[]` | challenge_towton_towns | challenge_towton_obj, challenge_towton |
| `eg_landmark` | scenario data | challenge_towton, challenge_towton_obj |
| `eg_allAlliedBuildings` | challenge_towton_obj | challenge_towton_obj |
| `alliedBuildingsLost` | challenge_towton | challenge_towton_towns |
| `goldMedalFailed` / `silverMedalFailed` | challenge_towton | challenge_towton_waves, challenge_towton_towns |
| `attackPhase1-4Started` | challenge_towton | challenge_towton_obj, challenge_towton |
| `finalWaveStarted` | challenge_towton_waves | challenge_towton, challenge_towton_towns |
| `eastWallBreached` / `westWallBreached` | challenge_towton | challenge_towton_waves |
| `outerHousesLost` | challenge_towton | challenge_towton |
| `enemyPlayer` / `localPlayer` / `allyPlayer` / `allyPlayer2` / `enemyPlayer2` | challenge_towton | all files |

### Inter-File Function Calls

| Caller File | Calls | Target File |
|-------------|-------|-------------|
| challenge_towton | `HC_Towton_InitObjectives()` | challenge_towton_obj |
| challenge_towton | `HC_Towton_InitObjectiveUI()` | challenge_towton_obj |
| challenge_towton | `HC_Towton_InitEnemyWaves()` | challenge_towton_waves |
| challenge_towton | `HC_Towton_InitTowns()` | challenge_towton_towns |
| challenge_towton | `HC_Towton_BeginNewPhase()` | challenge_towton_obj |
| challenge_towton | `HC_Towton_EndOldPhase()` | challenge_towton_obj |
| challenge_towton | `HC_Towton_LightBeacon()` | challenge_towton_towns |
| challenge_towton | `HC_Towton_UpdateObjectiveUI()` | challenge_towton_obj |

### Blueprint References

- **Lancaster:** Spearman 1, Yeoman 2-4, Hobelar 2-3, Earls Guard 3-4, Mounted MAA 2, Monk 3, Scout 1, Villager 1, Crossbowman 4, Siege Culverin 4, Naval Transport, Naval Carrack, Building Manor, Building Signal Beacon, Building Defense Outpost, Building Defense Palisade, Building Defense Wall
- **English (Enemy):** Spearman 2-4, Archer 2-4, Crossbow 3-4, MAA 1-4, Horseman 2-4, Knight 3-4, Mangonel 3, Springald 3, Ram 3, Trebuchet 4 CW, Bombard 4, Ribauldequin 4, Abbey King 2, Scout 1
- **French (Ally):** Knight 3-4
- **Upgrades:** Wood Fell Rate 1, Synchronized Shot, Ship of the Crown, Siege Engineers, Outpost Stone, Outpost Springald, Outpost Arrowslits
