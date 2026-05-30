# Abbasid Mission 8: Cyprus

## OVERVIEW

The Mamluk Sultanate (player1) invades Cyprus in 1426, beginning with a naval landing and the capture of Limassol, then expanding to conquer the island's three Frankish strongholds: Nicosia (primary target), Famagusta (Genoese naval base), and Kyrenia (cavalry garrison). After capturing Limassol as a forward base, the player receives resources and villagers, then must destroy Nicosia's Town Center and two Keeps while fending off timed attack waves from Nicosia and naval raids from Famagusta. Optional objectives include liberating three prison camps (which weaken enemy economies and grant freed villagers) and destroying Kyrenia (which sends cavalry reinforcements to Nicosia). The mission uses 8 players across multiple Frankish factions, BuildingTrainer-based unit production for enemy waves, and the Army/NavalArmy module for coordinated attacks and patrols.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m8_cyprus.scar` | core | Main mission script: player setup, relationships, restrictions, player unit spawns, intro/start flow, naval raid init, HoW workaround, trade ship CTA, ship tracking, debug helpers |
| `abb_m8_cyprus_data.scar` | data | Difficulty scaling (outpost/keep upgrades, tech tiers), `t_difficulty` table with all Util_DifVar parameters, unit composition tables (attackers/defenders/navy), attack route markers, loot tables, recipe/Army module definitions |
| `abb_m8_cyprus_objectives.scar` | objectives | Objective registration (OBJ/SOBJ constants), Limassol capture location init, fail condition (landmarks), win condition (Nicosia destroyed), Famagusta/Kyrenia/Prison objective definitions, post-capture triggers |
| `abb_m8_cyprus_defenders.scar` | spawns | Static defender spawning for Nicosia (wall lines, siege, scattered, keep garrisons), Famagusta (wall lines, xbows, siege), Limassol (horseman/anti-infantry defenders), Famagusta Navy (static + patrol), amortised spawn system |
| `abb_m8_cyprus_encounters.scar` | encounters | Proximity monitors for Nicosia/Famagusta/Kyrenia, Nicosia attack wave logic (BuildingTrainer → Army), naval raid spawning, objective target kill handler, Nicosia/Kyrenia finale army merges and retreats, Famagusta patrol init |
| `abb_m8_cyprus_prison_logic.scar` | other | Prison camp init, guard/tower monitoring, prisoner liberation and ownership transfer, resource deposit refresh, gold/wood camp economy-weakening monitors |
| `abb_m8_cyprus_automated.scar` | automated | Automated test script: checkpoint registration, AI-controlled playthrough phases, army spawning cheats, phase progression through Limassol → Nicosia |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | `_cyprus` | Init 8 players, relationships, upgrades, colours, resources |
| `Mission_SetupVariables` | `_cyprus` | Create shared SGroups, EGroups, state booleans |
| `Mission_SetDifficulty` | `_cyprus` | Delegates to `Init_Cyprus_Difficulty` |
| `Mission_SetRestrictions` | `_cyprus` | Lock market, farms, tithe barns for player |
| `Mission_Preset` | `_cyprus` | Setup data, enemies, objectives, trainers, player troops |
| `Mission_PreStart` | `_cyprus` | Boost player ship sight radius and speed |
| `Mission_Start` | `_cyprus` | Start Limassol capture, proximity monitors, naval raid |
| `Cyprus_InitNavalRaid` | `_cyprus` | Spawn initial Famagusta naval raid force |
| `Cyprus_LaunchInitNavalRaid` | `_cyprus` | Send initial naval raiders to attack destination |
| `Cyprus_LaunchInitKyreniaRaid` | `_cyprus` | Activate Kyrenia cavalry initial raid army |
| `Cyprus_CheckKyreniaRaidProx` | `_cyprus` | Detect when player sees Kyrenia raiders |
| `Cyprus_StartShipAttackCheck` | `_cyprus` | Begin monitoring player ships under attack |
| `Cyprus_CheckPlayerShipAttacked` | `_cyprus` | Trigger CTA and Famagusta raids on ship attack |
| `Cyprus_Ship_Built` | `_cyprus` | Track player-built naval units in sgroups |
| `Cyprus_HoW_Started` | `_cyprus` | Detect House of Wisdom construction start |
| `Cyprus_HoW_Constructed` | `_cyprus` | Auto-queue all four HoW wings on completion |
| `Cyprus_AutoSaveInterval` | `_cyprus` | Periodic autosave every 30 seconds |
| `Tradeship_Timer` | `_cyprus` | Reveal trade post and ping CTA |
| `Init_Cyprus_Difficulty` | `_data` | Apply outpost/keep upgrades and tech per difficulty |
| `Cyprus_SetupData` | `_data` | Define unit tables, attack routes, loot, resources |
| `Cyprus_EnemyMarkerData` | `_data` | Collect AllMarkers for defender spawn positions |
| `GetRecipe` | `_data` | Build MissionOMatic recipe with all Army modules |
| `Cyprus_Init_Objectives` | `_objectives` | Register all OBJ/SOBJ constants |
| `Init_LimassolCapture` | `_objectives` | Setup Limassol capture location and objectives |
| `Cyprus_CheckBuildHoWStart` | `_objectives` | Start HoW objective if not building after 120s |
| `Monitor_Player_Prisons_Prox` | `_objectives` | Start prison objective when player approaches |
| `Init_Nicosia` | `_defenders` | Spawn Nicosia wall lines, siege, scattered, garrisons |
| `Init_Famagusta` | `_defenders` | Spawn Famagusta wall defenders and siege |
| `Init_Famagusta_Navy` | `_defenders` | Spawn static naval defenders and patrols |
| `Init_Limassol` | `_defenders` | Spawn Limassol horseman and anti-infantry defenders |
| `Cyprus_SpawnWallLines` | `_defenders` | Procedural wall garrison spawner across markers |
| `Cyprus_SpawnStandAloneSiege` | `_defenders` | Place siege at markers aimed at target markers |
| `Cyprus_SpawnScatteredDefenders` | `_defenders` | Place individual defenders at marker positions |
| `Cyprus_GarrisonNicosiaKeeps` | `_defenders` | Garrison MaA into Nicosia keeps |
| `Cyprus_UnGarrisonNicosiaKeeps` | `_defenders` | Ungarrison keeps when health < 50% |
| `Amortise_EnemySpawns` | `_defenders` | Staggered Army_Init to prevent load spike |
| `Monitor_Player_Nicosia_Prox` | `_encounters` | Trigger Nicosia sub-objectives on approach |
| `Monitor_Player_Famagusta_Prox` | `_encounters` | Start Famagusta raids when player approaches |
| `Monitor_Player_Kyrenia_Prox` | `_encounters` | Start Kyrenia objective on proximity |
| `Monitor_Nicosia_Attacks_Start` | `_encounters` | Begin Nicosia attack wave cycle after grace |
| `Nicosia_Attacks` | `_encounters` | Train next wave via BuildingTrainer from table |
| `Nicosia_OnSpawn` | `_encounters` | Route spawned units to muster by type |
| `Nicosia_OnComplete` | `_encounters` | Launch attack army 30s after training complete |
| `Nicosia_Launch_Attack` | `_encounters` | Init Army with random attack route |
| `Nicosia_Monitor_Attack` | `_encounters` | Retreat army when below threshold |
| `Nicosia_Attack_Blocked` | `_encounters` | Dissolve army and retreat on blocked path |
| `Init_Famagusta_Patrols` | `_encounters` | Start Famagusta cavalry patrol army |
| `Spawn_Navy_Raids` | `_encounters` | Train naval raid wave from random table |
| `Famagusta_Navy_Raids_Launch_Attack` | `_encounters` | Init NavalArmy patrol with raid targets |
| `Cyprus_CheckSquadDeath` | `_encounters` | Drop naval loot on Famagusta ship death |
| `Cyprus_StartFamagustaRaids` | `_encounters` | Activate recurring naval raids and CTA |
| `Cyprus_StopNavalRaids` | `_encounters` | Remove naval raid rule, dissolve naval armies |
| `Monitor_Kyrenia_Reinforcements` | `_encounters` | Send Kyrenia cavalry to Nicosia defence |
| `Cyprus_CheckNicosiaFinale` | `_encounters` | Merge defenders to final positions, ungarrison |
| `Cyprus_ObjectiveTargetKilled` | `_encounters` | Handle TC/Keep/Dock destruction for objectives |
| `Cyprus_KyreniaDissolveArmies` | `_encounters` | Dissolve and retreat all Kyrenia forces |
| `Init_Prisons` | `_prison_logic` | Setup 3 prison camps with guards and resources |
| `Prisoner_Init` | `_prison_logic` | Spawn prisoners, guards, detect nearby towers |
| `Prisons_Monitor` | `_prison_logic` | Check guards/towers dead → free prisoners |
| `Prisons_RefreshResources` | `_prison_logic` | Reset resource deposits while guards alive |
| `Gold_Camp_Monitor` | `_prison_logic` | Set `b_isLowGold` when gold camp lost |
| `Wood_Camp_Monitor` | `_prison_logic` | Set `b_isLowWood` when wood camp lost |
| `AutoTest_OnInit` | `_automated` | Detect autotest flag, register checkpoints |
| `AutomatedCyprus_RegisterCheckpoints` | `_automated` | Define 4 test checkpoints with timeouts |
| `AutomatedMission_Start` | `_automated` | Begin scripted AI playthrough |
| `AutomatedCyprus_Phase1_CheckPlayStart` | `_automated` | Cheat buffs, attack-move to Limassol |
| `AutomatedCyprus_Phase2_LimassolIsComplete` | `_automated` | Advance to Nicosia after Limassol capture |
| `AutomatedCyprus_CheckArmySpawn` | `_automated` | Spawn reinforcements to maintain 180 pop |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DefendLandmarks` | Information (fail) | Player TC + HoW must survive; fails mission if both destroyed |
| `OBJ_CaptureLimassol` | Primary/Capture | Capture Limassol town as first base; fails if all land units die |
| `SOBJ_DefeatLimassolRebels` | Capture (child) | Defeat Limassol's garrison defenders |
| `SOBJ_LocationLimassol` | Capture (child) | Capture the Limassol location zone |
| `TOBJ_AvoidDestruction` | Tip (child) | Hint: avoid destroying Limassol buildings |
| `OBJ_DestroyNicosia` | Primary | Destroy Nicosia TC + 2 Keeps to win mission |
| `SOBJ_DestroyNicosia_TC` | Primary (child) | Destroy Nicosia's Town Center |
| `SOBJ_DestroyNicosia_Keeps` | Primary (child) | Destroy both Nicosia Keeps (counter: 0/2) |
| `OBJ_HouseOfWisdom` | Optional | Build a House of Wisdom (auto-starts after 120s if not begun) |
| `OBJ_DestroyFamagusta` | Battle | Destroy 3 Genoese docks to stop naval raids |
| `OBJ_DestroyKyrenia` | Battle | Destroy Kyrenia to stop cavalry reinforcements |
| `SOBJ_DestroyKyrenia_TC` | Battle (child) | Destroy Kyrenia's Town Center |
| `OBJ_Prisoners` | Optional | Liberate 3 prison camps (counter: 0/3) |

### Difficulty

All difficulty scaling uses `Util_DifVar({easy, normal, hard, expert})` via `t_difficulty`:

| Parameter | Easy | Normal | Hard | Expert | What it scales |
|-----------|------|--------|------|--------|----------------|
| `prisoner_guardAmount` | 3 | 4 | 5 | 10 | MaA guarding each prison |
| `navalLootChance` | 35% | 30% | 25% | 20% | Loot drop chance per enemy ship |
| `nicosia_grace_timer` | 220 | 160 | 100 | 40 | Seconds before Nicosia attacks begin |
| `nicosia_attacks_timer` | 420 | 360 | 300 | 240 | Interval between Nicosia attack waves |
| `navy_raid_timer` | 400 | 350 | 300 | 240 | Interval between naval raids |
| `init_navy_raid_delay` | 420 | 360 | 300 | 240 | Delay before first naval raid |
| `init_kyrenia_raid_delay` | 690 | 660 | 630 | 600 | Delay before first Kyrenia raid |
| `nicosia_retreat_threshold` | 7 | 7 | 8 | 9 | Squad count to trigger retreat |
| `nicosia_keep_garrisonAmount` | 0 | 5 | 10 | 15 | MaA garrisoned in each Nicosia keep |
| Outpost upgrades | — | Arrowslits | Springald | Cannon | Defensive structure emplacement tier |
| Keep upgrades | — | Arrowslits | Springald | Cannon | Keep emplacement tier |
| Enemy tech tiers | Mil 0/Unit 3 | Mil 2/Unit 3 | Mil 3/Unit 4 | Mil 4/Unit 4 | Military and unit upgrade levels |
| Factional upgrades (Hard+) | — | — | Yes | Yes | Armor-Clad (Nicosia), Crossbow buffs (Famagusta), Cavalry barding (Kyrenia) |

Unit count variables scale linearly (e.g., `num_12_to_20` = {12,14,16,20}, `num_15_to_30` = {15,20,25,30}).

### Spawns

**Player Starting Forces:** 15 spearmen, 15 MaA, 15 crossbowmen, 14 knights, 4 combat ships, 3 warships, 2 scouts. 12 villagers granted after Limassol capture. Starting resources: 2000 food, 2000 wood, 1400 gold, 0 stone.

**Nicosia Attack Waves:** 10 cycling compositions trained via `BuildingTrainer` from `Unit_Trainer_Nicosia` (10s build time override). Waves include infantry-heavy, cavalry-heavy, and "boss" waves with siege (cannons, trebuchets, ribauldequins). Every 4th wave is a boss wave. Waves cycle back to index 4 after exhausting the table. Units muster by type (cav/siege/misc) then form an Army on a random attack route (3 routes). Armies retreat when below threshold count, abandoning siege.

**Famagusta Naval Raids:** 3 raid compositions trained via `Unit_Trainer_Famagusta_Navy`, randomly selected. Spawned ships muster then form NavalArmy patrols across 6 destination markers. Naval loot (food/wood/gold pickups) drops on Famagusta ship death with difficulty-scaled chance, capped at 15.

**Famagusta Land Patrols:** Horsemen + knights patrol 5 locations south of Famagusta.

**Kyrenia Raids:** Initial cavalry raid force (knights + horsemen) marches through 3 waypoints toward player base. On proximity detection, dissolves after 12s and retreats. Later, 3 Kyrenia cavalry armies reinforce Nicosia when player reaches final defence zone.

**Limassol Defenders:** Crossbowmen at capture point, horsemen at patrol markers, spearmen + springalds for anti-ship, archers + spearmen for anti-infantry.

**Prison Guards:** MaA guards (3–10 per camp) + outpost towers per camp.

**Static Defenders:** Wall lines (procedural marker-based placement), stand-alone siege (mangonels, cannons, trebuchets, culverins aimed at target markers), scattered crossbowmen/handcannoneers, keep garrisons.

### AI

- **No AI_Enable for enemies** — all enemy behaviour is scripted via Army modules, BuildingTrainer, and manual commands
- **Army modules** (via `GetRecipe`): 5 Nicosia defender armies (player7/player8), 2 Nicosia cavalry patrols, 2 Nicosia infantry patrols, 1 Nicosia init raider army, 1 Nicosia bridge guard, 3 Famagusta defender armies (player5), 1 Famagusta cavalry patrol, 2 Kyrenia defender armies, 3 Kyrenia cavalry armies, 1 Kyrenia init raider army
- **Army behaviours:** `TARGET_ORDER_LINEAR` for static defenders, `TARGET_ORDER_PATROL` for cavalry patrols, `TARGET_ORDER_RANDOM` for Famagusta patrols
- **Blocked handling:** `Nicosia_Attack_Blocked` dissolves army, removes siege, retreats; `ramsBuiltWhenBlocked = 1`, `brokenWallThreshold = 40`
- **Unit cap:** `CYPRUS_UNIT_CAP = 200` per enemy player prevents over-spawning
- **Autotest only:** `AI_Enable(player1, true)` + `Game_AIControlLocalPlayer()` for automated testing

### Timers

| Timer Call | Delay/Interval | Purpose |
|------------|----------------|---------|
| `Rule_AddOneShot(Monitor_Nicosia_Attacks_Start, grace_timer)` | 40–220s | Grace period after Limassol before Nicosia attacks |
| `Rule_AddInterval(Nicosia_Attacks, attacks_timer)` | 240–420s | Recurring Nicosia attack wave spawns |
| `Rule_AddInterval(Spawn_Navy_Raids, navy_raid_timer)` | 240–400s | Recurring Famagusta naval raids |
| `Rule_AddOneShot(Cyprus_LaunchInitNavalRaid, init_delay)` | 240–420s | First Famagusta naval raid |
| `Rule_AddOneShot(Cyprus_LaunchInitKyreniaRaid, init_delay)` | 600–690s | First Kyrenia cavalry raid |
| `Rule_AddOneShot(Tradeship_Timer, 200)` | 200s | Reveal trade post after Limassol capture |
| `Rule_AddOneShot(Cyprus_StartShipAttackCheck, 30)` | 30s | Begin monitoring player ships |
| `Rule_AddOneShot(Cyprus_CheckBuildHoWStart, 120)` | 120s | Prompt HoW objective if not started |
| `Rule_AddOneShot(Init_Famagusta_Patrols, 15)` | 15s | Start Famagusta cavalry patrols |
| `Rule_AddOneShot(Nicosia_OnComplete → Launch, 30)` | 30s | Muster delay before attack wave launches |
| `Rule_AddInterval(Cyprus_AutoSaveInterval, 600)` | 600s | Periodic autosave |
| `Rule_AddInterval(Prisons_Monitor, 1)` | 1s | Check prison guard status |
| `Rule_AddInterval(Prisons_RefreshResources, 10)` | 10s | Reset prison resource deposits |
| `Rule_AddInterval(Monitor_Kyrenia_Reinforcements, 4)` | 4s | Check if Kyrenia should reinforce Nicosia |
| `Amortise_EnemySpawns` | 0.125s stagger | Delayed spawns to prevent load spikes |
| `UnitTrainer_OverrideBuildTime` | 10s (all units) | Uniform build time for enemy trainers |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `abb_m8_cyprus.scar` | `MissionOMatic.scar`, `module_rovingarmy.scar`, `abb_m8_cyprus_objectives.scar`, `abb_m8_cyprus_data.scar`, `abb_m8_cyprus_automated.scar`, `abb_m8_cyprus_defenders.scar` |
| `abb_m8_cyprus_data.scar` | `MissionOMatic.scar`, `module_rovingarmy.scar` |
| `abb_m8_cyprus_objectives.scar` | `MissionOMatic.scar`, `module_rovingarmy.scar`, `abb_m8_cyprus_prison_logic.scar`, `abb_m8_cyprus_encounters.scar` |
| `abb_m8_cyprus_defenders.scar` | `cardinal.scar`, `MissionOMatic.scar` |
| `abb_m8_cyprus_encounters.scar` | `cardinal.scar`, `MissionOMatic.scar` |
| `abb_m8_cyprus_prison_logic.scar` | `cardinal.scar`, `MissionOMatic.scar` |
| `abb_m8_cyprus_automated.scar` | `cardinal.scar`, `MissionOMatic.scar`, `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals

- **Players:** `player1`–`player8` (defined in core, used everywhere)
- **Difficulty table:** `t_difficulty` (defined in `_data`, read by `_defenders`, `_encounters`, `_objectives`, `_prison_logic`)
- **Unit tables:** `CYPRUS_UNITS`, `P1_UNITS`, `CYPRUS_ATTACK_ROUTES`, `CYPRUS_MARKER_LOCATIONS` (defined in `_data`, used by `_defenders`, `_encounters`)
- **SGroups:** `sg_p1_land_units`, `sg_p1_warships`, `sg_player_ships`, `sg_limassol_defenders`, `sg_nicosia_retreat`, `sg_famagusta_navy`, `sg_init_kyrenia_raid`, `sg_kyrenia_retreat`, `sg_trade_ships` (created in core/variables, used across files)
- **EGroups:** `eg_nicosia_keeps`, `eg_nicosia_tc`, `eg_famagusta_tc`, `eg_famagusta_dock`, `eg_famagusta_keep`, `eg_kyrenia_tc`, `eg_limassol`, `eg_limassol_tc`, `eg_p1_how` (scenario-placed or created, used across encounters/objectives)
- **State booleans:** `b_limassolCaptureStarted`, `b_kyreniaDestroyed`, `b_famagustaRaidsTriggered`, `b_nicosiaFinaleTriggered`, `b_nicosiaTCDestroyed`, `b_nicosiaKeepsDestroyed`, `b_isLowGold`, `b_isLowWood`, `house_of_wisdom_started`, `house_of_wisdom_complete`
- **Counters:** `i_prisonsFreed`, `nicosiaKeepsDestroyed`, `nicosia_raid_index`, `naval_loot_index`, `naval_loot_count`
- **Trainers:** `Unit_Trainer_Nicosia`, `Unit_Trainer_Famagusta`, `Unit_Trainer_Famagusta_Navy` (init in core, used in encounters)
- **Army arrays:** `naval_armies`, `kyrenia_armies` (populated via encounters, dissolved on objective complete)

### Inter-File Calls

| Caller File | Called Function | Defined In |
|-------------|-----------------|------------|
| `_cyprus` | `Cyprus_SetupData()` | `_data` |
| `_cyprus` | `Cyprus_EnemyMarkerData()` | `_data` |
| `_cyprus` | `Cyprus_Init_Objectives()` | `_objectives` |
| `_cyprus` | `Init_Limassol()` | `_defenders` |
| `_cyprus` | `Init_Famagusta()` | `_defenders` |
| `_cyprus` | `Init_Nicosia()` | `_defenders` |
| `_cyprus` | `Init_Famagusta_Navy()` | `_defenders` |
| `_cyprus` | `Init_Prisons()` | `_prison_logic` |
| `_cyprus` | `AutoTest_OnInit()` | `_automated` |
| `_objectives` | `Init_LimassolCapture()` | `_objectives` (self) |
| `_objectives` | `Monitor_Player_Prisons_Prox()` | `_objectives` (self) |
| `_objectives` | `CyprusDebug_*()` | `_encounters` |
| `_encounters` | `Cyprus_StartFamagustaObjective()` | `_encounters` (self) |
| `_encounters` | `Cyprus_StopNavalRaids()` | `_encounters` (self) |
| `_encounters` | `Cyprus_KyreniaDissolveArmies()` | `_encounters` (self) |
| `_encounters` | `Init_Famagusta_Patrols()` | `_encounters` (self) |
| `_encounters` | `Nicosia_Attacks()` | `_encounters` (self) |
| `_objectives (OnComplete)` | `Monitor_Nicosia_Attacks_Start()` | `_encounters` |
| `_objectives (OnComplete)` | `Gold_Camp_Monitor()`, `Wood_Camp_Monitor()` | `_prison_logic` |
| `_objectives (OnComplete)` | `Tradeship_Timer()` | `_cyprus` |
| `_objectives (OnComplete)` | `Cyprus_StartShipAttackCheck()` | `_cyprus` |
| `_objectives (OnComplete)` | `Cyprus_LaunchInitNavalRaid()` | `_cyprus` |
| `_objectives (OnComplete)` | `Cyprus_LaunchInitKyreniaRaid()` | `_cyprus` |
| `_data` | `Nicosia_Attack_Blocked()` | `_encounters` |
