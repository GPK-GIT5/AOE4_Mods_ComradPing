# Abbasid Bonus Mission

## OVERVIEW

The Abbasid bonus mission is a multi-front campaign scenario where the player (Crusaders, player 1) must destroy two Rival Crusader (player 2) landmarks while subduing three neutral Holy Order keeps (Templar, Teutonic, Hospitaller — player 3) via capture mechanics. Player 2 fields an economy-driven attack wave system that escalates unit composition over time, supplemented by cavalry raiders and progressive tech research. The Byzantine Empire (player 5) conducts naval raids from three docks, which the player can optionally destroy. Establishing trade with Ayyubid Allies (player 4) unlocks a mercenary reinforcement panel offering horse archers, camel riders, and baghlahs. Difficulty scaling adjusts unit counts, economy strength, research pace, and raid frequency across four tiers.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| abb_bonus.scar | core | Main mission file: player setup, lifecycle hooks, imports all other files, launches all systems |
| abb_bonus_data.scar | data | Defines constants, recipe/module data, patrol units, raider configs, unit/tech tables, P2 attacker setup |
| abb_bonus_objectives.scar | objectives | Registers primary (Destroy Landmarks), optional (Destroy Docks, Establish Trade) objectives |
| abb_bonus_capture.scar | objectives | Registers Holy Order capture sub-objectives for Templar, Teutonic, and Hospitaller keeps |
| abb_bonus_attack.scar | spawns | Economy-driven P2 attack wave system: reinforcement, unit purchasing, army dispatch, retreat logic |
| abb_bonus_raid.scar | spawns | Land and naval raider spawning, monitoring, target cycling, and withdrawal logic |
| abb_bonus_patrol.scar | spawns | Creates and monitors looping patrol routes for P2 units |
| abb_bonus_units.scar | spawns | Spawns initial units for all players, wall/bastion defenders, garrison logic, Holy Order guards |
| abb_bonus_reinforce.scar | training | Mercenary reinforcement panel: horse archers, camel riders, baghlahs purchasable with gold |
| abb_bonus_util.scar | other | Utility helpers for marker collection and siege unit counting |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | abb_bonus.scar | Configures 5 players, diplomacy, difficulty, production locks |
| Mission_SetupVariables | abb_bonus.scar | Calls all data/unit/patrol/raider/tech init functions |
| Mission_Preset | abb_bonus.scar | Sets resources, upgrades outposts, starts landmark/tech monitors |
| Mission_PreStart | abb_bonus.scar | Registers all objectives and capture system |
| Mission_Start | abb_bonus.scar | Launches attacks, patrols, raids, holy orders, reinforcements |
| MonitorLandmarks | abb_bonus.scar | Fails mission if player has no active landmarks |
| UpdateTech | abb_bonus.scar | Progressively researches P2 upgrades on interval |
| AbbBonus_OnConstructionComplete | abb_bonus.scar | Starts trade objective when player builds first landmark |
| GetRecipe | abb_bonus_data.scar | Returns MissionOMatic recipe with locations and army modules |
| AbbBonus_SetupPatrols | abb_bonus_data.scar | Defines patrol unit compositions for P2 |
| AbbBonus_SetupRaiders | abb_bonus_data.scar | Configures P2 cavalry and P5 naval raider parameters |
| AbbBonus_SetupUnitTables | abb_bonus_data.scar | Defines P2 and P5 unit cost/spawn tables |
| AbbBonus_SetupTechData | abb_bonus_data.scar | Builds ordered P2 tech upgrade list |
| AbbBonus_SetupAttackersP2 | abb_bonus_data.scar | Configures P2 attack wave army and unit mixes |
| AbbBonus_StartAttackersP2 | abb_bonus_attack.scar | Starts econ, constraint, and monitor rules for P2 attacks |
| AbbBonus_StopAttackersP2 | abb_bonus_attack.scar | Deactivates P2 and removes all attack rules |
| AbbBonus_UpdateEcon | abb_bonus_attack.scar | Calculates P2 resource pool from time and villagers |
| AbbBonus_UpdateConstraints | abb_bonus_attack.scar | Sets attack target count and unit mix tier by time |
| AbbBonus_MonitorAttackers | abb_bonus_attack.scar | Spawns units, launches attack, handles retreat logic |
| AbbBonus_OnAttackSgroupRemoved | abb_bonus_attack.scar | Retreats attack group to rally point |
| AbbBonus_Capture_Init | abb_bonus_capture.scar | Registers parent capture objective and all three keeps |
| AbbBonus_Capture_InitTemplars | abb_bonus_capture.scar | Registers Templar capture/defeat/location sub-objectives |
| AbbBonus_Capture_InitTeutons | abb_bonus_capture.scar | Registers Teutonic capture/defeat/location sub-objectives |
| AbbBonus_Capture_InitHospitallers | abb_bonus_capture.scar | Registers Hospitaller capture/defeat/location sub-objectives |
| AbbBonus_Capture_MergeTemplars | abb_bonus_capture.scar | Adds Templar units to their army on defeat |
| AbbBonus_Capture_MergeTeutons | abb_bonus_capture.scar | Adds Teutonic units to their army on defeat |
| AbbBonus_Capture_MergeHospitallers | abb_bonus_capture.scar | Adds Hospitaller units to their army on defeat |
| AbbBonus_RegisterObjectives | abb_bonus_objectives.scar | Registers Destroy Landmarks, Destroy Docks, Establish Trade |
| AbbBonus_CheckDocks | abb_bonus_objectives.scar | Monitors dock destruction count, completes objective at 3 |
| AbbBonus_StartDocksObjective | abb_bonus_objectives.scar | Starts the Destroy Docks optional objective |
| AbbBonus_CreatePatrol | abb_bonus_patrol.scar | Spawns patrol group and starts looping movement |
| AbbBonus_MonitorPatrol | abb_bonus_patrol.scar | Restarts patrol loop when group reaches end |
| AbbBonus_StartRaidersP2 | abb_bonus_raid.scar | Starts P2 land raider monitor |
| AbbBonus_StartNavalRaiders | abb_bonus_raid.scar | Starts three P5 naval raider monitors |
| AbbBonus_StopRaidersP2 | abb_bonus_raid.scar | Removes P2 raider monitor rule |
| AbbBonus_StopRaidersP5 | abb_bonus_raid.scar | Removes all P5 naval raider monitor rules |
| AbbBonus_MonitorRaiders | abb_bonus_raid.scar | Spawns raiders, dispatches to targets, handles withdrawal |
| AbbBonus_OnRaidSgroupRemoved | abb_bonus_raid.scar | Retreats raider group to rally point |
| AbbBonus_Reinforce_Init | abb_bonus_reinforce.scar | Creates mercenary hire panel with 3 options |
| AbbBonus_Reinforce_Callback | abb_bonus_reinforce.scar | Spawns purchased mercenary units at ally location |
| AbbBonus_ShowEventCue | abb_bonus_reinforce.scar | Displays UI event notification to player |
| AbbBonus_SpawnInitUnits | abb_bonus_units.scar | Spawns starting units for P1, P2, P5 |
| AbbBonus_SetupHolyOrders | abb_bonus_units.scar | Spawns Holy Order guards and starts capture objective |
| AbbBonus_SpawnUnitSequence | abb_bonus_units.scar | Spawns one unit per numbered marker in sequence |
| AbbBonus_SpawnWallDefenders | abb_bonus_units.scar | Spawns and moves units to wall marker positions |
| AbbBonus_SpawnBastionDefendersP2 | abb_bonus_units.scar | Spawns mixed infantry at 8 bastion positions |
| AbbBonus_GarrisonOutposts | abb_bonus_units.scar | Garrisons units inside each entity in an EGroup |
| AbbBonus_GetMarkers | abb_bonus_util.scar | Collects numbered markers into a table |
| AbbBonus_GetSiegeCount | abb_bonus_util.scar | Counts siege-type squads in an SGroup |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_DestroyLandmarks | Primary | Destroy 2 Rival Crusader landmarks; completes mission (with holy orders) |
| OBJ_SubdueHolyOrders | Capture | Parent: subdue all 3 Holy Order keeps; completes mission (with landmarks) |
| SOBJ_CaptureTemplarKeep | Capture (sub) | Capture the Templar Keep; awards Templar units and production |
| SOBJ_DefeatTemplarResistance | Battle (sub) | Defeat Templar defenders; merges them into army after 10s |
| SOBJ_LocationTemplarKeep | Capture (sub) | UI location marker for Templar Keep |
| SOBJ_CaptureTeutonKeep | Capture (sub) | Capture the Teutonic Keep; awards Teutonic units and production |
| SOBJ_DefeatTeutonResistance | Battle (sub) | Defeat Teutonic defenders; merges them into army after 10s |
| SOBJ_LocationTeutonKeep | Capture (sub) | UI location marker for Teutonic Keep |
| SOBJ_CaptureHospitallerKeep | Capture (sub) | Capture the Hospitaller Keep; awards Hospitaller units and production |
| SOBJ_DefeatHospitallerResistance | Battle (sub) | Defeat Hospitaller defenders |
| SOBJ_LocationHospitallerKeep | Capture (sub) | UI location marker for Hospitaller Keep (triggers merge after 10s) |
| OBJ_DestroyDocks | Optional | Destroy 3 Byzantine docks; counter-tracked |
| OBJ_EstablishTrade | Optional | Send trade unit near allies; unlocks mercenary reinforcement panel |

**Win condition:** Both OBJ_DestroyLandmarks and OBJ_SubdueHolyOrders complete → `Mission_Complete()`. Either can finish first.
**Lose condition:** Player has zero active landmarks → `Mission_Fail()`.

### Difficulty

| Parameter | Values (Easy→Expert) | What it scales |
|-----------|----------------------|----------------|
| researchLevel | 1, 2, 3, 4 | P2/P5 outpost upgrade tiers at mission start |
| researchInterval | 420, 360, 300, 240 | Seconds between P2 auto-tech-upgrades |
| econMod | 0.55, 0.70, 0.85, 1.0 | P2 economy strength ramp multiplier |
| unitCount_low | 2, 3, 4, 5 | Squad count for small army/patrol modules |
| unitCount_med | 4, 6, 8, 10 | Squad count for medium army modules |
| unitCount_high | 6, 9, 12, 15 | Squad count for large army modules |
| raidSpawnMod | 1.6, 1.4, 1.2, 1.0 | Raider spawn delay multiplier (higher = slower spawns) |
| extraVillagerCount | {0,0,0,0} | Location extra villagers (unused, all zero) |

### Spawns

**P2 Attack Waves:**
- Economy-driven: `econStrength` ramps from `500*econMod` to `1400*econMod` based on game time and surviving villager ratio. `resourcePool` replenishes every 60s.
- Units purchased from pool at defined costs (spearman=80, archer=80, man-at-arms=120, crossbow=120, horseman=240, knight=240, ram=300, mangonel=600, trebuchet=750).
- 7 unit mix tiers escalate every 400s of game time, progressing from spearman/archer to knight/trebuchet compositions.
- Target count scales to 30% of player's military near base, clamped to 15–50.
- Siege units capped at `SIEGE_LIMIT = 3`.
- Attack army follows 7-waypoint linear path to player base; retreats if outnumbered 3:1 (non-siege only).

**P2 Cavalry Raiders:**
- Horsemen from cavalry building, spawn delay = `14 * raidSpawnMod` seconds.
- Start with 3 units, max 6. Uses Army system with 13 random targets.
- Withdraw if outnumbered 2:1, then grow target count by 1.

**P5 Naval Raiders (3 groups):**
- Group 1: war galleys, spawn delay 90*raidSpawnMod, 1→3 units, 4 targets.
- Group 2: war galleys, spawn delay 120*raidSpawnMod, 1→2 units, 4 targets.
- Group 3: combat ships, spawn delay 240*raidSpawnMod, 1 unit max, 5 targets.
- No army system; patrol target markers then return if outnumbered or idle.

**P2 Patrols (7 routes):**
- 2 cavalry patrols (horsemen + knights), 1 infantry patrol (crossbow + men-at-arms + spears), 4 spear patrols.
- Loop through marker waypoints; restart on idle.

**Static Defenders:**
- P2: 17 wall archers, 8 bastion positions (man-at-arms + crossbow each), garrisoned outposts, 7 guard spearmen, 3 naval ships.
- P3: Templar (2 guards + 6 crossbow), Teutonic (8 guards), Hospitaller (2 guards + 6 archers).
- P5: 4 guard archers.

### AI

- No `AI_Enable` calls; all AI behavior is hand-scripted via Army modules and rule-based monitors.
- **Army modules** (MissionOMatic recipe): 6 P2 defend armies (patrol at fixed positions, combatRange=50), 1 P2 stronghold defend army, 3 P3 holy order armies (patrol, combatRange=30), 2 P5 naval defend armies (patrol, combatRange=50).
- All single-target armies get `activeRange` from marker proximity radius (default 45) and `useCustomDirection = true`.
- **Attack army:** P2 attack uses `TARGET_ORDER_LINEAR` through 7 waypoints to player base, builds rams when blocked.
- **Raid army:** P2 raiders use `TARGET_ORDER_RANDOM` over 13 targets.
- **Outnumbered retreat:** Attackers retreat at 3:1 disadvantage (non-siege), raiders at 2:1.

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| `AbbBonus_UpdateEcon` | 60s | Recalculates P2 resource pool from game time and villager ratio |
| `AbbBonus_UpdateConstraints` | 120s | Updates P2 attack target count and unit mix tier |
| `AbbBonus_MonitorAttackers` | 5s | Spawns units into attack wave, dispatches or retreats army |
| `AbbBonus_MonitorRaiders` | 2s | Spawns raiders, dispatches to targets, handles withdrawal |
| `AbbBonus_MonitorPatrol` | 2s | Restarts patrol loop when group reaches end |
| `UpdateTech` | researchInterval (240–420s) | Auto-researches next upgrade for P2 from ordered list |
| `AbbBonus_CheckDocks` | 2s | Counts destroyed P5 docks, completes objective at 3 |
| `MonitorLandmarks` | every tick (Rule_Add) | Checks if player has active landmarks; fails mission if none |
| `AbbBonus_StartAttackersP2` | OneShot @ 60s | Activates P2 attack wave system |
| `AbbBonus_StartRaidersP2` | OneShot @ 180s | Activates P2 cavalry raiders |
| `AbbBonus_StartDocksObjective` | OneShot @ 600s | Starts Destroy Docks optional objective |
| `AbbBonus_StartNavalRaiders` | OneShot @ 600s | Activates all 3 P5 naval raider groups |
| `AbbBonus_StartSubdueHolyOrders` | OneShot @ 5s | Starts the Holy Orders capture objective |
| `AbbBonus_Capture_MergeTemplars` | OneShot @ 10s | Merges Templar squads into their army on defeat |
| `AbbBonus_Capture_MergeTeutons` | OneShot @ 10s | Merges Teutonic squads into their army on defeat |
| `AbbBonus_Capture_MergeHospitallers` | OneShot @ 10s | Merges Hospitaller squads into their army on defeat |

## CROSS-REFERENCES

### Imports
- All files import `cardinal.scar` and `MissionOMatic/MissionOMatic.scar`.
- `abb_bonus_reinforce.scar` imports `CampaignPanel.scar` instead of MissionOMatic.
- `abb_bonus.scar` imports `abb_bonus.events` (NIS events file) plus all 8 other .scar files.

### Shared Globals
- **Player handles:** `player1`–`player5` (defined in `abb_bonus.scar`, used everywhere).
- **player2_data:** Economy/attack state table (defined in `abb_bonus.scar`, used by `_attack.scar`).
- **t_difficulty:** Difficulty parameter table (defined in `abb_bonus.scar`, used by `_data.scar`, `_units.scar`).
- **p2_unitTable / p5_unitTable / p5_unitTableNaval:** Unit cost tables (defined in `_data.scar`, used by `_attack.scar`).
- **p2_unitMix:** Attack composition tiers (defined in `_data.scar`, used by `_attack.scar`).
- **p2_attackers1 / p2_raiders1 / p5_naval_raiders1–3:** Attacker/raider config tables (defined in `_data.scar`, used by `_attack.scar` and `_raid.scar`).
- **patrols_data:** Patrol tracking table (defined in `_data.scar`, used by `_patrol.scar`).
- **sg_temp / eg_temp:** Shared temporary SGroup/EGroup (used across multiple files).
- **OBJ_DestroyLandmarks / OBJ_SubdueHolyOrders:** Primary objectives (defined in `_objectives.scar` and `_capture.scar`, cross-checked for mission completion).
- **sg_templars / sg_teutons / sg_hospitallers:** Holy Order sgroups (created in `_units.scar`, used in `_capture.scar`).
- **P1_FOOD/WOOD/GOLD/STONE, SIEGE_LIMIT:** Constants from `_data.scar` used in `_attack.scar` and `abb_bonus.scar`.

### Inter-File Function Calls
- `abb_bonus.scar` → calls init/setup/start/stop functions from all other files.
- `_objectives.scar` `OnComplete` → calls `AbbBonus_StopAttackersP2()` (`_attack.scar`) and `AbbBonus_StopRaidersP2()` (`_raid.scar`).
- `_objectives.scar` `OnComplete` → checks `Objective_IsComplete(OBJ_SubdueHolyOrders)` (from `_capture.scar`).
- `_capture.scar` `OnComplete` → checks `Objective_IsComplete(OBJ_DestroyLandmarks)` (from `_objectives.scar`).
- `_attack.scar` → calls `AbbBonus_GetUnitDataByName()` (local) and `AbbBonus_GetSiegeCount()` (`_util.scar`).
- `_reinforce.scar` → calls `AbbBonus_ShowEventCue()` (local) and `ReinforcementPanel_Init/Create/Enable` (from `CampaignPanel.scar`).

### Blueprint References
- **Crusader CMP:** Holy Order Templar/Teuton/Hospitaller units and masters, naval hulk, cannon units (removed), ram tower (removed), landmark buildings.
- **Ayyubid CMP:** Turkic horse archer, camel rider, baghlah (mercenaries).
- **Byzantine:** Horse archer merc, naval combat/warships (P5 defenders).
- **English:** Naval war galley and combat ships (P2 naval).
- **HRE:** Man-at-arms upgrade tier 3 (P2 tech).
- **Common UPG:** Full melee/ranged damage/armor I–III, siege engineers, spearman/archer/horseman upgrades, naval and outpost upgrades.
