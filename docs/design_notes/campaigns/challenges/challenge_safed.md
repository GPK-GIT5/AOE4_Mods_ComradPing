# Historical Challenge: Safed

## OVERVIEW

Historical Challenge: Safed is a Knights Templar defense mission where the player must protect the Fortress of Safed from a Mamluk Sultanate siege. The core gameplay loop requires escorting villagers to 4 sequential mining towns to gather stone, which fuels allied NPC repairs on the fortress while trebuchets and enemy waves continuously assault it. Upon depleting all 4 stone deposits, the player transitions to a final assault objective: clearing the enemy siege camp to stop the bombardment. A hidden "Conqueror Mode" activates if the player keeps all villagers alive and reaches mine 2 before 5:00, spawning additional trebuchets and scaling up enemy unit counts for a harder challenge. Medal scoring is based on fortress health percentage at mission completion.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_safed.scar` | core | Main mission script: player setup, recipe, restrictions, modifiers, fortress repair, stone monitoring, music, conqueror mode, intro NIS |
| `challenge_safed_data.scar` | data | Defines EGroups/SGroups, starting units, encounter compositions, mine town waves, ram units, siege camp defenders, save-villager units, resource pickups |
| `challenge_safed_objectives.scar` | objectives | Registers all OBJ_/SOBJ_ objectives, progress bar, siege camp monitor/count, softlock prevention |
| `challenge_safed_ram_attack.scar` | spawns | Handles ram deployment, wall-breach detection, ram-to-fortress transition, wall breach notification |
| `challenge_safed_treb_attack.scar` | spawns | Manages trebuchet spawning in timed intervals, arrival tracking, staggered attack sequencing against fortress |
| `challenge_safed_training.scar` | other | Training hint to select and protect villagers |
| `challenge_safed_villagerlife.scar` | automated | Custom villager life system for neutral mine-town villagers: work/flee/garrison cycle based on enemy proximity |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | challenge_safed | Initializes 5 players with relationships and colors |
| `Mission_SetupVariables` | challenge_safed | Sets all global variables, modifiers, and thresholds |
| `GetRecipe` | challenge_safed | Returns mission recipe with locations and audio settings |
| `Mission_SetRestrictions` | challenge_safed | Removes buildings/units/upgrades, completes starting upgrades |
| `Mission_Preset` | challenge_safed | Spawns units, encounters, applies modifiers, inits objectives |
| `Mission_PreStart` | challenge_safed | Removes pop cap, sets starting resources, reveals FOW |
| `Mission_Start` | challenge_safed | Starts fortress health rules, stone monitors, primary objective |
| `Safed_Modify_Fortress` | challenge_safed | Disables hardpoints, fire tick, scuttle; scales damage received |
| `Safed_Fortress_Empathy_Damage` | challenge_safed | Reduces fortress damage when health below bronze threshold |
| `Safed_Fortress_Health_Update` | challenge_safed | Updates health globals every tick, fires threshold notifications |
| `Safed_Fortress_Repair` | challenge_safed | Ungarrisons ally villagers to repair if player has stone |
| `Safed_Modify_Stone_Gather_Rates` | challenge_safed | Scales stone efficiency by ratio of gathering villagers |
| `Safed_Modify_Villager_Rates` | challenge_safed | Sets harvest/repair rates, carry capacity for villagers |
| `Safed_Modify_Stone_Node_Amounts` | challenge_safed | Sets each stone deposit to 900 remaining/contained |
| `Safed_Modify_Safed_City` | challenge_safed | Sets wall health, removes scuttle/combat from city buildings |
| `Safed_Modify_Enemy_Tents` | challenge_safed | Removes UI healthbar and targeting from enemy tents |
| `Safed_Arrival_At_Town` | challenge_safed | Detects villager arrival, reveals FOW, starts attack wave |
| `Safed_Monitor_Stone_Resource_Depleted` | challenge_safed | Tracks depleted mines, triggers next-town reveal and gifts |
| `Safed_Stone_Depleted` | challenge_safed | Converts buildings, gifts resources, reveals next stone |
| `Safed_Gift_Villagers` | challenge_safed | Replaces half of lost villagers after mines 1-2 |
| `Safed_Change_Nearby_Entities_Owner` | challenge_safed | Converts nearby buildings to player ownership by type |
| `Safed_Reveal_Stone` | challenge_safed | Reveals stone deposit on map with FOW and objective UI |
| `Safed_Monitor_Player_Stone` | challenge_safed | Shows event cue when player stone inventory is zero |
| `Safed_Show_Event_Cue` | challenge_safed | Utility wrapper for UI_CreateEventCueClickable |
| `Safed_Music` | challenge_safed | Locks/unlocks music intensity based on mine progress |
| `Safed_Music_Fortress` | challenge_safed | Changes music intensity based on fortress health |
| `Safed_CM_Activate` | challenge_safed | Checks conqueror mode conditions and activates if met |
| `Safed_CM_Notifier` | challenge_safed | Shows conqueror mode CTA, triggers unit scaling |
| `Safed_CM_Modify_Unit_Count` | challenge_safed | Scales all existing enemy army unit counts upward |
| `HC_Safed_IntroSetup` | challenge_safed | Spawns intro trebuchets with zero-damage for NIS |
| `HC_Safed_IntroTeardown` | challenge_safed | Cleans intro units, starts real trebuchet attack |
| `Safed_Init_ESG_Data` | challenge_safed_data | Creates all EGroups and SGroups |
| `Safed_On_Launch_Wave` | challenge_safed_data | Launches wave with rotating spawn locations |
| `_Safed_Rotate_Spawns` | challenge_safed_data | Cycles through multiple spawn markers |
| `Safed_Cancel_Wave` | challenge_safed_data | Pauses current wave generator and resets tracking |
| `Safed_Init_Player_Starting_Units` | challenge_safed_data | Deploys player villagers, military, and scouts |
| `Safed_Init_Enemy_Encounters` | challenge_safed_data | Spawns 17 patrol encounter armies along routes |
| `Safed_Trigger_Town_Attack_Wave` | challenge_safed_data | Initializes and launches a WaveGenerator for a town |
| `Safed_Init_Save_Villagers` | challenge_safed_data | Spawns captive villagers guarded by enemy patrol |
| `Safed_Monitor_Save_Villagers` | challenge_safed_data | Converts captives to player when guards eliminated |
| `Safed_Init_Enemy_Siege_Camp_Units` | challenge_safed_data | Spawns 9 siege camp armies (4 static + 5 patrol) |
| `Safed_Init_Pickups` | challenge_safed_data | Spawns wood/food/gold/stone resource pickups on map |
| `Safed_Init_Objectives` | challenge_safed_objectives | Defines and registers all objective tables |
| `Safed_Update_Fortress_ProgressBar` | challenge_safed_objectives | Updates fortress health progress bar each tick |
| `Safed_Init_Siege_Camp` | challenge_safed_objectives | Sets up final siege camp objective with UI and monitoring |
| `Safed_Siege_Camp_Monitor` | challenge_safed_objectives | Tracks defender count, updates progress bar |
| `Safed_Siege_Camp_Count` | challenge_safed_objectives | Counts remaining siege camp defenders |
| `Safed_Siege_Camp_Set_Target` | challenge_safed_objectives | Activates front-row siege armies when player approaches |
| `Safed_Unit_Cost_Init` | challenge_safed_objectives | Caches unit blueprint costs for affordability check |
| `Safed_Player_Can_Afford_Units` | challenge_safed_objectives | Returns true if player can afford any producible unit |
| `Safed_Monitor_Player_Can_Afford` | challenge_safed_objectives | Fails mission if player has no army and no resources |
| `Safed_Init_Enemy_Rams` | challenge_safed_ram_attack | Spawns 2 rams and escort army, modifies wall damage |
| `Safed_Enemy_Ram_Attack_Monitor` | challenge_safed_ram_attack | Detects wall breach, redirects rams to fortress |
| `Safed_Init_Treb_Attack` | challenge_safed_treb_attack | Initializes treb spawning rules and prop trebs |
| `Safed_Treb_Spawn` | challenge_safed_treb_attack | Spawns one treb per interval, cycles spawn points |
| `Safed_Treb_Arrived` | challenge_safed_treb_attack | Flags treb as arrived, triggers first attack |
| `Safed_Treb_Attack_Begin` | challenge_safed_treb_attack | Staggers attack commands across arrived trebs |
| `Safed_Training_Hint_Save_Vills` | challenge_safed_training | Registers training goal to select villagers |
| `Safed_VillagerLife_Create` | challenge_safed_villagerlife | Creates runtime villager life with job SGroups |
| `Safed_VillagerLife_Init` | challenge_safed_villagerlife | Initializes villager life instance, spawns, starts monitor |
| `Safed_VillagerLife_Monitor` | challenge_safed_villagerlife | Main loop: work/flee/garrison based on enemy proximity |
| `Safed_VillagerLife_GoToWork` | challenge_safed_villagerlife | Assigns villagers to harvest gold/food/wood/stone |
| `Safed_VillagerLife_SetWander` | challenge_safed_villagerlife | Moves idle villagers to roaming when resources deplete |
| `Safed_VillagerLife_Wander` | challenge_safed_villagerlife | Orders single villager to wander to random location |
| `Safed_Init_Villager_Life` | challenge_safed_villagerlife | Entry point: creates villager life for 4 mine towns |
| `Safed_Villager_Life_Create` | challenge_safed_villagerlife | Iterates mine towns, spawns villagers per job type |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_SaveFortressPrimary` | Primary | Save the Fortress of Safed from falling; fails if fortress destroyed or all villagers die |
| `OBJ_SaveFortressProgressBar` | Information | Displays fortress health percentage as a progress bar |
| `OBJ_Tip_SaveVillagers` | Tip | Reminder to protect villagers; disappears when all stone mined |
| `OBJ_Bonus_ConqMode` | Bonus | Hints at conqueror mode; completes/updates when CM activates or conditions fail |
| `SOBJ_SecureStone` | Capture (sub) | Mine stone at 4 deposits; counter 0/4; triggers SOBJ_StopBombardment on completion |
| `SOBJ_LocationSecureStone` | Build (sub) | Stone Bounty UI marker on map for current mine location |
| `SOBJ_StopBombardment` | Battle (sub) | Clear the enemy siege camp; triggers on all stone mined |
| `SOBJ_LocationStopBombardment` | Battle (sub) | Clear the siege camp location marker with progress bar |

### Difficulty / Scaling

No `Util_DifVar` is used. Difficulty is managed through the Conqueror Mode system and empathy damage:

| Parameter | Value | Effect |
|-----------|-------|--------|
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE` | 0.145 | Base multiplier on all fortress damage received |
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE_ENDING` | 0.5 | Additional damage reduction after mine 4 depleted |
| `SAFED_FORTRESS_DAMAGE_EMPATHY_THRESHOLD` | 0.35 | Fortress HP% below which empathy damage kicks in |
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE_EMPATHY` | 0.5 | Empathy damage reduction multiplier (bronze medal range) |
| `SAFED_CM_ACTIVATE_TIME` | 300s (5:00) | Deadline to meet conqueror mode conditions |
| `SAFED_CM_VILLAGER_COUNT` | 7 | All villagers alive required for conqueror mode |
| `SAFED_STONE_DEPLETED_COUNT == 2` | — | Must have mined 2 deposits before 5:00 for CM |
| CM unit scaling | 1-10% | Adds units to all existing enemy armies when CM activates |

### Spawns

**Starting Units (player1):**
- 7 villagers, 8 Templar spearmen (T3), 3 men-at-arms, 3 Templar knights (T3), 2 scouts
- 15 allied (player3) villagers garrison in fortress for repairs

**Route Encounters (17 total):**
- Militia, spearmen, archers, horsemen, camel riders, mangonels in varying compositions
- Deployed as Army_Init patrols with high leash range (999) between villages

**Mine Town Waves (4 towns):**
- Town 1: spearman+horseman, 6s delay, 5 waves
- Town 2: camel_rider+2 militia, 5s delay, 5 waves
- Town 3: horseman+2 archers+spearman+man-at-arms, 5s delay, 6 waves (7 in CM)
- Town 4: man-at-arms+camel_rider+spearman+archer, 5s delay, 6 waves (7 in CM)
- Waves use rotating spawn markers for positional variety

**Siege Camp (9 armies):**
- Camps 1-4: static front-row defenders near trebuchets (archers, spearmen, men-at-arms)
- Camps 5-9: patrolling defenders (spearmen, camel riders, archers, mangonels)
- Front-row armies activate combat range when player approaches (`Safed_Siege_Camp_Set_Target`)

**Rams:**
- 2 rams + 3 men-at-arms + 3 militia escort
- Attack walls first (damage modifier 0.175), then fortress on breach (damage modifier 2.5)
- Triggered at stone depleted count == 3

**Trebuchets:**
- Spawned in intervals of 8s via `Safed_Treb_Spawn`
- Move to designated positions, then attack fortress in staggered 2.75s intervals
- Prop trebuchets placed in siege yard for easy kills (skipped in CM)
- CM adds additional trebuchet spawn points (`mkr_cm_enemy_trebuchet` series)

**Save Villagers:**
- 3 Templar villagers + 1 monk held captive, guarded by 6 knights + 4 men-at-arms
- FOW revealed after mine 2; converts to player1 when guards eliminated

### AI

| Setting | Target | Details |
|---------|--------|---------|
| `AI_Enable(player3, false)` | Allied repair crew | Disabled; controlled by scripted repair logic |
| `AI_Enable(player4, false)` | Neutral world player | Disabled; villager life managed by custom system |
| Player2 (enemy) | Mamluk Sultanate | Uses Army_Init encounters and WaveGenerator; no global AI plan |
| Encounter patrols | 17 route armies | `TARGET_ORDER_PATROL`, `combatRange` per marker radius, leash 999 |
| Siege camp front row | 4 armies | Initially `combatRange=0`, `holdPosition=true`; activate on player proximity |

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| `Safed_Fortress_Health_Update` | every tick (`Rule_Add`) | Updates fortress health globals and threshold notifications |
| `Safed_Fortress_Repair` | 1s | Checks player stone, ungarrisons/garrisons repair crew |
| `Safed_Monitor_Player_Stone` | every tick (`Rule_Add`) | Shows depleted-stone event cue with 7min cooldown |
| `Safed_Monitor_Stone_Resource_Depleted` | 1s | Detects empty stone nodes, increments counter |
| `Safed_Arrival_At_Town` | 1s (×4 instances) | Checks villager proximity to each mine town marker |
| `Safed_Modify_Stone_Gather_Rates` | 0.5s | Adjusts stone efficiency by gathering villager ratio |
| `Safed_Fortress_Empathy_Damage` | 0.5s | Applies/removes empathy damage modifier |
| `Safed_CM_Activate` | 1s | Checks conqueror mode activation conditions |
| `Safed_Music` | 1s | Manages music intensity lock/unlock |
| `Safed_Music_Fortress` | 1s | Music intensity tied to fortress health thresholds |
| `Safed_Treb_Spawn` | 8s (`SAFED_TREB_SPAWN_INTERVAL`) | Spawns one trebuchet per interval |
| `Safed_Treb_Arrived` | every tick (`Rule_Add`) | Checks if spawned trebs reached destination |
| `Safed_Treb_Attack_Begin` | 2.75s (`SAFED_TREB_ATTACK_INTERVAL`) | Staggers attack commands to arrived trebs |
| `Safed_Enemy_Ram_Attack_Monitor` | 1s | Monitors wall state, transitions rams to fortress |
| `Safed_Siege_Camp_Monitor` | 0.5s | Updates siege camp defender count and progress |
| `Safed_Siege_Camp_Set_Target` | 1s | Activates front-row armies when player near trigger |
| `Safed_Monitor_Player_Can_Afford` | 1s | Prevents softlock if player has no army/resources |
| `Safed_Monitor_Save_Villagers` | 1s | Watches for guard elimination to free captives |
| `Safed_VillagerLife_Monitor` | 1s (per instance) | Work/flee/garrison cycle for neutral town villagers |
| `_Safed_Wave_Respawn` | variable delay (5-6s) | OneShot to prepare next wave in sequence |
| `Safed_CM_Notifier` | OneShot at 10s delay | Shows conqueror mode notification after treb arrival |
| `Safed_Gift_Villagers` | OneShot at 2.5s | Gifts replacement villagers after mine depletion |

## CROSS-REFERENCES

### Imports

| Import | Source |
|--------|--------|
| `MissionOMatic/MissionOMatic.scar` | Core mission framework (Missionomatic_InitPlayer, LOCATION, recipe system) |
| `challenge_safed_data.scar` | Local data file |
| `challenge_safed_treb_attack.scar` | Local trebuchet system |
| `challenge_safed_ram_attack.scar` | Local ram attack system |
| `challenge_safed_villagerlife.scar` | Local custom villager life system |
| `challenge_safed_objectives.scar` | Local objectives |
| `training.scar` | Shared training/hint framework |
| `challenge_safed_training.scar` | Local training hints |

### Shared Globals

- `t_villagerLifePrefabs` — global table used by villager life system to track all instances
- `t_armyEncounterFamily_allFamilies` — global from Army system; iterated by CM to scale units
- `PLAYERS` — global player table from MissionOMatic
- `eg_allGoldResources`, `eg_allWoodResources`, `eg_allStoneResources` — global Gathering EGroups
- `eg_farms` — populated via `Gathering_FindAllFarms(player4)`
- `EVENTS.*` — event constants (Camera_Intro, PrimaryObjective_Start, Victory, etc.)
- `MUSIC_TENSE_COMBAT_RARE`, `MUS_STINGER_*`, `SFX_VICTORY_TIMER_*` — shared audio constants
- `CE_SAFEDCONQ` — custom challenge event constant for achievement tracking

### Inter-File Function Calls

| Caller File | Callee File | Function |
|-------------|-------------|----------|
| challenge_safed | challenge_safed_data | `Safed_Init_ESG_Data()` |
| challenge_safed | challenge_safed_data | `Safed_Init_Player_Starting_Units()` |
| challenge_safed | challenge_safed_data | `Safed_Init_Enemy_Encounters()` |
| challenge_safed | challenge_safed_data | `Safed_Init_Enemy_Siege_Camp_Units()` |
| challenge_safed | challenge_safed_data | `Safed_Init_Save_Villagers()` |
| challenge_safed | challenge_safed_data | `Safed_Init_Pickups()` |
| challenge_safed | challenge_safed_data | `Safed_Cancel_Wave()` |
| challenge_safed | challenge_safed_data | `Safed_Trigger_Town_Attack_Wave()` |
| challenge_safed | challenge_safed_objectives | `Safed_Init_Objectives()` |
| challenge_safed | challenge_safed_treb_attack | `Safed_Init_Treb_Attack()` |
| challenge_safed | challenge_safed_ram_attack | `Safed_Init_Enemy_Rams()` |
| challenge_safed | challenge_safed_villagerlife | `Safed_Init_Villager_Life()` |
| challenge_safed | challenge_safed_training | `Safed_Training_Hint_Save_Vills()` |
| challenge_safed_objectives | challenge_safed | `Safed_Reveal_Stone()`, `Safed_Init_Siege_Camp()` |
| challenge_safed_objectives | challenge_safed | `Safed_Siege_Camp_Set_Target()`, `Safed_Player_Can_Afford_Units()` |

### Player Architecture

| Player | Role | Color | AI |
|--------|------|-------|----|
| player1 | Human — Knights Templar | Blue | N/A |
| player2 | Enemy — Mamluk Sultanate | Red | Scripted armies/waves only |
| player3 | Ally — Fortress repair crew | Yellow | Disabled; scripted repair |
| player4 | Neutral world — Town villager life | Yellow | Disabled; custom villager life |
| player5 | Fortress owner — Prevents attack alerts | Blue | Implicit |
