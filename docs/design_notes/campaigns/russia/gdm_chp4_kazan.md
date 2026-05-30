# Russia Chapter 4: Kazan

## OVERVIEW

This mission recreates the 1552 Siege of Kazan from the Russia (Muscovy) campaign. The player controls Ivan IV's forces (Russian civilization) against the Khanate of Kazan (Mongol-type faction). The mission flows in two major phases: first, destroy a Tatar woodcutter settlement and establish a Town Center foothold; then, siege the fortified city of Kazan by breaching its outer and inner walls before eliminating the Khan's elite guards. An escalating intensity system drives increasingly powerful cavalry attack waves from Kazan city, while extensive wall-defense modules (12 outer, 6 inner positions) and a dynamic fallback mechanic create a layered defensive challenge for the AI opponent.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp4_kazan.scar` | core | Main mission script: setup, recipe, wave spawning, intensity system, starting units, villager transport, failure checks |
| `obj_securefort.scar` | objectives | Phase 1 objectives: destroy Tatar settlement, build Town Center, spawn villagers via naval transport |
| `obj_siegekazan.scar` | objectives | Phase 2 objectives: breach outer wall, breach inner wall, defeat Khan's Guards, wall-breach event handlers |
| `obj_clearwestford.scar` | objectives | Optional objective to destroy the west ford military camp to stop flanking attacks |
| `kazan_training.scar` | training | Tutorial goal sequences for Ivan IV's leader ability (gunpowder attack speed aura) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | gdm_chp4_kazan | Init globals, SGroups, wave data, objective inits |
| `Mission_SetupPlayers` | gdm_chp4_kazan | Configure 5 players, relationships, upgrades |
| `Mission_SetRestrictions` | gdm_chp4_kazan | Unlock Russian buildings, speed palisade/TC build |
| `Mission_Preset` | gdm_chp4_kazan | Player colours, outpost/tower upgrades, AI paths, deploy units |
| `Mission_Start` | gdm_chp4_kazan | Start OBJ_SecureFort, give AI resources, weaken settlement |
| `GetRecipe` | gdm_chp4_kazan | Define MissionOMatic recipe with locations and modules |
| `Kazan_InitStartingUnits` | gdm_chp4_kazan | Deploy Ivan's army and initial enemy scouts |
| `Kazan_WeakenTatarSettlement` | gdm_chp4_kazan | Reduce HP and increase fire damage on woodcutter buildings |
| `Kazan_MoveStartingUnits_Archers` | gdm_chp4_kazan | Command archers to attack initial enemy group |
| `Kazan_MoveStartingUnits_Cavalry` | gdm_chp4_kazan | Command cavalry charge after archers engage |
| `Kazan_MoveStartingUnits_Infantry` | gdm_chp4_kazan | Infantry unit parade march to position |
| `Kazan_PositionArchersAndCav` | gdm_chp4_kazan | Reposition archers/cavalry after initial fight ends |
| `Kazan_RetreatScouts` | gdm_chp4_kazan | Enemy scouts retreat to woodcutter camp |
| `Kazan_GroupWallsForObjectives` | gdm_chp4_kazan | Collect outer/inner wall entities into EGroups |
| `Kazan_SpawnCavAttackWave` | gdm_chp4_kazan | Spawn intensity-scaled attack wave from Kazan |
| `Kazan_SetIntensity` | gdm_chp4_kazan | Set kazan_intensity to new value if higher |
| `Kazan_VaryCavSpawn` | gdm_chp4_kazan | Randomize wave strength/timing using flex system |
| `Kazan_AddCavLoop` | gdm_chp4_kazan | Start recurring cavalry wave spawner (Normal+ only) |
| `Kazan_IntensityCheck` | gdm_chp4_kazan | Wait for intensity >= 1, then start wave loops |
| `Kazan_WestFordLoop` | gdm_chp4_kazan | Periodic west ford wave; escalates every 5 cycles |
| `Kazan_SpawnVillagers` | gdm_chp4_kazan | Spawn transport ships with villagers and monk |
| `Kazan_MoveTransport` | gdm_chp4_kazan | Move transport ships to landing points |
| `Kazan_UnloadVillagers` | gdm_chp4_kazan | Ungarrison villagers, transfer to player1 |
| `Kazan_DespawnTransport` | gdm_chp4_kazan | Send transports offscreen, scout loops river |
| `Kazan_ToggleMonkHeal` | gdm_chp4_kazan | Activate monk auto-heal ability |
| `Kazan_CheckFailure` | gdm_chp4_kazan | Mission fail if TC destroyed or no units remain |
| `Kazan_SkipIntro` | gdm_chp4_kazan | Deploy units at final positions when intro skipped |
| `Kazan_CheckDefendNorthOutpostKilled` | gdm_chp4_kazan | Increment intensity when north outpost defenders die |
| `Kazan_CheckDefendFieldGateKilled` | gdm_chp4_kazan | Increment intensity when field gate defenders die |
| `Achievement_CheckAnnihilation` | gdm_chp4_kazan | Fire achievement if all enemy units/buildings destroyed |
| `TriggerContextObjective` | gdm_chp4_kazan | Start optional west ford objective after 2 wave defeats |
| `PreventMultiple_TC` | gdm_chp4_kazan | Enforce single Town Center construction limit |
| `Kazan_AutoSaveLoop` | gdm_chp4_kazan | Auto-save every 900 seconds during siege |
| `Kazan_ProxForSpeech` | gdm_chp4_kazan | Trigger intel events at Volga fords, pastures, walls |
| `SiegeKazan_InitObjectives` | obj_siegekazan | Register siege phase objectives |
| `Kazan_OuterWallBreached` | obj_siegekazan | Handle outer wall segment killed event |
| `Kazan_InnerWallBreached` | obj_siegekazan | Handle inner wall killed; can bypass outer objective |
| `Kazan_GuardSpotted` | obj_siegekazan | Play walla charge when player spots elite guards |
| `Kazan_HasPlayerReachedCity` | obj_siegekazan | Spawn Kazan defenders when player reaches city |
| `Kazan_SpawnKazanDefenders` | obj_siegekazan | Spawn all gate/wall/elite defender squads |
| `Kazan_SpawnWallDefend` | obj_siegekazan | Spawn archers on all 12 outer + 6 inner wall positions |
| `Kazan_WallFormations` | obj_siegekazan | Set spread formation on all wall defender groups |
| `Kazan_WallMove` | obj_siegekazan | Move wall defenders to their wall positions |
| `Kazan_FallbackToInnerDefense` | obj_siegekazan | Retreat outer defenders; transfer to inner modules |
| `Kazan_InitOutro` | obj_siegekazan | Spawn cavalry parade for outro cinematic |
| `Kazan_OutroCavLoop` | obj_siegekazan | Iteratively spawn outro cavalry units |
| `Kazan_SendOutroCav` | obj_siegekazan | Send outro cavalry along waypoint path |
| `SecureFort_InitObjectives` | obj_securefort | Register foothold phase objectives |
| `Kazan_OnEntityDestroyed` | obj_securefort | Track settlement building destruction progress |
| `Kazan_AddMissionFailureCheckLoop` | obj_securefort | Start failure check after 20-second delay |
| `ClearFordBase_InitObjectives` | obj_clearwestford | Register optional west ford objectives |
| `WestFordApproached` | obj_clearwestford | Start sub-objective when player nears west ford |
| `MissionTutorial_KazanLeaderAura` | kazan_training | PC training: select Ivan, view leader ability |
| `MissionTutorial_KazanLeaderAura_Xbox` | kazan_training | Xbox training: D-Pad select Ivan, radial menu |
| `Predicate_UserHasSelectedIvan` | kazan_training | Check if player selected Ivan's squad |
| `Predicate_UserHasLookedAtIvanAbility` | kazan_training | Check if player hovered over gunpowder ability |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_SecureFort` | Primary | Phase 1: Secure a foothold |
| `SOBJ_KillWoodcutters` | Battle | Destroy the Tatar woodcutter settlement |
| `SOBJ_TatarBuildings` | Battle | Dummy objective for remaining building UI hints |
| `SOBJ_BuildFort` | Primary | Construct a Town Center (free cost via modifier) |
| `OBJ_SiegeKazan` | Primary | Phase 2: Siege the city of Kazan |
| `SOBJ_BreachOuter` | Primary | Breach Kazan's outer stone wall (starts with parent) |
| `SOBJ_BreachInner` | Primary | Breach Kazan's inner stone wall |
| `SOBJ_KillKhanGuards` | Primary | Defeat all Khan's elite guards (progress bar) |
| `OBJ_ClearWestFord` | Optional | Destroy west ford camp to stop flanking attacks |
| `SOBJ_ClearWestFordBuildings` | Optional | Destroy military buildings at west ford (counter) |
| `OBJ_Failure` | Primary | Failure/outro trigger wrapper |
| `OBJ_DebugComplete` | Primary | Debug: instant mission complete |

### Difficulty

| Parameter | Values (Easy/Normal/Hard/Expert) | What It Scales |
|-----------|----------------------------------|----------------|
| `kazan_waveinterval` | 210 / 210 / 180 / 150 | Seconds between cavalry attack waves |
| Villager count | 11 / 8 / 8 / 8 | Villagers per transport group |
| NorthGate archers | 3 / 6 / 6 / 6 | Archer squads at north gate |
| NorthGate handcannon | 2 / 2 / 2 / 6 | Handcannon squads at north gate |
| Wall defenders (typical) | 5 / 8 / 8 / 10 archers | Archers per wall section |
| Wall handcannon (typical) | 2 / 4 / 4 / 8 | Handcannon per wall section |
| Elite knights | 14 / 20 / 24 / 28 | Khan's Guard knight squads |
| Elite handcannon | 8 / 12 / 16 / 20 | Khan's Guard handcannon squads |
| Outer wall archers | 3-4 / 5 / 5 / 8 | Archers per outer wall segment |
| Inner wall mixed | 0-4 / 2-4 / 2-4 / 6-8 | Archers+handcannon per inner wall segment |
| Outpost upgrades | Springald / Springald / Springald / Cannon | Outpost weapon type |
| Tower upgrades | Springald / Springald / Cannon / Cannon | Tower weapon type |
| Murder Holes | excluded for player2 | AI cannot research murder holes |
| DefendWoodcutters spearman | — / — / 4 / 4 | Extra spearmen on Hard/Expert only |
| DefendNorthOutpost1 units | 4 spear (E/N) / 6 MAA (H/X) | Unit type swaps by difficulty |
| DefendWestRoad2 units | +4 spear (E/N) / +6 MAA (H/X) | Extra defenders by difficulty |
| Wave compositions | Smaller (E/N) / Larger + siege (H/X) | Per-intensity wave unit counts |
| West ford loop | Skipped on Easy | No west ford waves on Easy |
| Cavalry waves | Skipped on Easy | No recurring waves on Easy difficulty |

### Spawns

**Starting Forces (Player):**
- 12 archer squads, Ivan the Terrible leader, 6 horsemen, 4 knights (Easy/Normal only)
- Infantry parade: 8 spearmen, 8 men-at-arms, 10 handcannoneers, 1 scout

**Villager Transport (after settlement cleared):**
- 2 transport ships + 1 scout ship from player5 (Ivan's Navy)
- Villagers: 2 groups of 11 (Easy) or 8 (Normal+), plus 1 monk
- Ships move to landing points, ungarrison, monk auto-heals, transports despawn

**Kazan City Defenders (spawned when player reaches city or inner wall objective starts):**
- 6 gate/wall sectors: NorthGate, SouthGate, NorthWall, SouthWall, EastWall, Central — each gets archers, handcannoneers, men-at-arms, spearmen (difficulty-scaled)
- 12 outer wall positions: archers in spread formation (3-8 per segment)
- 6 inner wall positions: archers + handcannoneers (difficulty-scaled)
- Elite guards: knights (14-28) + handcannoneers (8-20) on player4

**Cavalry Attack Waves (intensity system, 8 tiers):**
- Tier 1: 2 horsemen + 2 horse archers
- Tier 2: 5 horsemen + 3 horse archers
- Tiers 3-8: Multiple composition options mixing horsemen, horse archers, knights, spearmen, archers, men-at-arms, mangonels, traction trebuchets; counts scale from ~10 to ~34 squads
- Hard/Expert adds mangonels at tier 3+ and trebuchets at tier 5+
- Route: from inner Kazan through north gate, bridge, field gate, to player TC

**West Ford Waves:**
- Base: 2 spearmen + 2 men-at-arms + 3 archers via `Wave_New` system
- Escalates every 5 cycles: +1 men-at-arms + 2 archers
- Attacks via west road toward player TC; stops if Easy or camp destroyed

**Patrol Forces (RovingArmy modules):**
- WestRoad patrol: 8 horsemen + 4 horse archers (+ 4 knights on Expert)
- WestForest patrol: 4 spearmen + 2 archers (+ 2 MAA on Expert)
- EastForest patrol: 4 spearmen + 2 archers (E/N/H) or 6 horsemen (Expert)
- NorthGatePatrol: 8 MAA + 6 archers (+ 4 MAA + 4 archers on Expert)
- SouthGatePatrol: 8 MAA + 6 archers (+ 4 MAA + 4 archers on Expert)

### AI

- `AI_Enable(player3, false)` — player3 (Ivan ally/neutral holder) has AI disabled
- Player2 (Kazan) popcap set to 500-1000; given 10,000 of each resource
- `PlayerUpgrades_Auto` applied to players 1-4 (player2 excludes murder holes)
- `AIPlayer_SetMarkerToUpdateCachedPathToPosition` — two cached paths for ford attack routes
- All Kazan defense modules use `reinforcements` from "KazanVillagers" TownLife at 80% threshold
- `Kazan_FallbackToInnerDefense` — on inner wall breach, disables reinforcements, retreats 1/3 of outer defenders, transfers remaining to inner defense modules via `TransferModuleIntoModule`

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `Rule_AddInterval(Kazan_ProxForSpeech, 5)` | 5s | Check player proximity for speech triggers (Volga, pastures, walls) |
| `Rule_AddInterval(Kazan_AutoSaveLoop, 900)` | 900s (15min) | Periodic auto-save during siege phase |
| `Rule_AddInterval(Kazan_CheckDefendNorthOutpostKilled, 10)` | 10s | Check if north outpost defenders eliminated |
| `Rule_AddInterval(Kazan_CheckDefendFieldGateKilled, 10)` | 10s | Check if field gate defenders eliminated |
| `Rule_AddInterval(Kazan_HasPlayerReachedCity, 5)` | 5s | Check if player has reached Kazan city marker |
| `Rule_AddInterval(Kazan_IntensityCheck, 10)` | 10s | Wait for intensity >= 1 to start wave system |
| `Rule_AddInterval(Kazan_CheckFailure, 5)` | 5s | Check TC/unit loss for mission failure |
| `Rule_AddOneShot(Kazan_AddMissionFailureCheckLoop, 20)` | 20s | Delay before starting failure checks |
| `Rule_AddOneShot(Kazan_AddCavLoop, 90)` | 90s | Delay before first cavalry wave loop |
| `Rule_AddInterval(Kazan_VaryCavSpawn, kazan_waveinterval)` | 150-210s | Recurring cavalry wave spawner |
| `Rule_AddInterval(Kazan_WestFordLoop, 120)` | 120s | Recurring west ford attack wave |
| `Rule_AddInterval(Kazan_GuardSpotted, 1)` | 1s | Check if player can see elite guards |
| `Rule_AddOneShot(Kazan_WallFormations, 1)` | 1s | Set wall defenders to spread formation |
| `Rule_AddOneShot(Kazan_SpawnWallDefend, 1)` | 1s | Spawn wall defender archers |
| `Rule_AddOneShot(Kazan_WallMove, 5)` | 5s | Move wall defenders to positions |
| `Rule_AddOneShot(Kazan_MoveTransport, 1)` | 1s | Start transport ship movement |
| `Rule_AddOneShot(Kazan_UnloadVillagers, 15)` | 15s | Ungarrison villagers from transports |
| `Rule_AddOneShot(Kazan_DespawnTransport, 4)` | 4s | Send transports offscreen |
| `Rule_AddInterval(PreventMultiple_TC, 1)` | 1s | Enforce single TC construction |
| `Rule_AddInterval(WestFordApproached, 1)` | 1s | Check player proximity to west ford |

### Intensity System

The `kazan_intensity` variable drives wave escalation (starts at 0):
- +1 when woodcutter settlement destroyed (SOBJ_KillWoodcutters complete)
- +1 when north outpost defenders eliminated
- +1 when field gate defenders eliminated
- +1 every 5th wave (wave counts 5, 10, 15, 20)
- +1 when outer wall breached
- `kazan_intensityFlex` adds randomized bonus tiers (max +2) with a spend/pool mechanic

### Fallback Mechanic

When inner wall is breached (`Kazan_FallbackToInnerDefense`):
1. Reinforcements disabled on all outer modules
2. Every 3rd unit in outer modules retreats to random retreat markers and self-destructs
3. Remaining gate/wall units transferred to "KazanInnerDefense" module
4. Outer wall archers redistributed across 6 inner wall modules (2 outer → 1 inner each)
5. Inner Kazan units attack-move to inner Kazan marker

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (Cardinal scripts)
- `obj_securefort.scar` — foothold phase objectives
- `obj_siegekazan.scar` — siege phase objectives
- `obj_clearwestford.scar` — optional west ford objective
- `kazan_training.scar` — tutorial goal sequences
- `training/campaigntraininggoals.scar` — shared campaign training framework (imported by kazan_training)

### Shared Globals
- `g_leaderIvan` — leader data structure from `Missionomatic_InitializeLeader`
- `kazan_intensity` / `kazan_intensityFlex` / `kazan_wavecount` — wave system state
- `kazanDefendersSpawned` — flag preventing duplicate defender spawns
- `khan_guard_max` — initial elite guard count for progress bar
- `pos_rus_tc` — player TC position, updated when TC built
- `wave_ford1` — Wave object for west ford attacks
- `b_VolgaIntelPlayed` / `b_PastureIntelPlayed` / `b_WallsSightedIntelPlayed` — speech triggers
- `b_attackWaveContextTriggered` / `i_timesDefeated` — optional objective trigger tracking

### Inter-File Function Calls
- `gdm_chp4_kazan.scar` calls `SecureFort_InitObjectives()`, `SiegeKazan_InitObjectives()`, `ClearFordBase_InitObjectives()` during setup
- `obj_securefort.scar` calls `Kazan_SpawnVillagers()`, `Kazan_GroupWallsForObjectives()`, `Kazan_IntensityCheck()`, `Kazan_CheckDefendNorthOutpostKilled/FieldGateKilled()`, `Kazan_HasPlayerReachedCity()`, `Kazan_CheckFailure()`, `Kazan_AddMissionFailureCheckLoop()`, `PreventMultiple_TC()`
- `obj_siegekazan.scar` calls `Kazan_SpawnKazanDefenders()`, `Kazan_FallbackToInnerDefense()`, `Achievement_CheckAnnihilation()`, `Mission_Complete()`, `CheckMarkerForUnits()`
- `obj_clearwestford.scar` uses `eg_mon_westroad` EGroup defined in recipe modules
- `kazan_training.scar` references `g_leaderIvan.sgroup`, `player1`
- `TriggerContextObjective()` (core) starts `OBJ_ClearWestFord` (clearwestford) after 2 wave defeats

### MissionOMatic Modules Used
- **TownLife**: KazanVillagers, WestRoadVillagers, FieldGateVillagers (zero population, serve as reinforcement source)
- **RovingArmy**: CavAttackWave (reverse targeting toward player), AttackWest (with withdraw threshold 0.4), WestRoad/WestForest/EastForest patrols, NorthGatePatrol, SouthGatePatrol
- **Defend**: DefendWoodcutters, DefendNorthOutpost1-3, DefendWestRoad1-2, DefendFieldGate1-3, NorthGate, SouthGate, NorthWall, SouthWall, EastWall, Central, KazanOuterWall1-12, KazanInnerWall1-6, KazanInnerDefense, KazanElite (player4)

### Recipe Metadata
- Campaign: `gdm`, Chapter: `chapter4`, Phase: `mission_kazan`
- Audio: `gdm` / `rts1552kazan`
- Title Card: Date 1552, Location "Kazan"
- Intro NIS: `EVENTS.Intro`, Outro NIS: `EVENTS.Kazan_Outro_Camera`
- Achievement: `CE_ACHIEVDESTROYALLSIEGEOFKAZAN` (destroy all enemy units and production buildings)
