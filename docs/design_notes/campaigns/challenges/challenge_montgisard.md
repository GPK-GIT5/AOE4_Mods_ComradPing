# Historical Challenge: Montgisard

## OVERVIEW

The Battle of Montgisard is a historical challenge where the player (Templar faction) must capture all 4 Sacred Sites held by the Ayyubid/Abbasid enemy. The mission features a timed **Conqueror Mode** bonus path: capture Sacred Site 1 within 3 minutes, then destroy an enemy camp within another 3 minutes to activate a harder variant with doubled enemy reinforcements, upgraded enemies, and a 25-minute countdown timer. The map includes 6 Points of Interest (POI)—rams, mining camps, a fortress, and a prison—that reward the player with neutral units, villagers, or buildings upon completion. Enemy AI launches periodic reinforcement waves (every 6 minutes) and attacks (every 7 minutes) along predefined marker paths between Sacred Sites, with escalating unit tiers across 6 wave tables. Medal objectives track completion time: Gold (<17 min), Silver (<25 min), Bronze (<60 min), or Conqueror (<25 min in Conqueror Mode).

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_montgisard_data.scar` | data | Initializes all mission variables, SGroups/EGroups, patrol paths, attack group compositions, diplomacy, and capture-rate modifiers. |
| `challenge_montgisard_objectives.scar` | objectives | Defines all OBJ_/SOBJ_ objective structures, medal objectives, registers and starts objectives, sets up reinforcement/attack interval rules. |
| `challenge_montgisard_reinforcements.scar` | spawns | Contains 6 reinforcement wave tables (tableWave1–6) per fortress, Conqueror Mode unit doubling logic, patrol creation, and reinforce group initialization. |
| `challenge_montgisard.scar` | core | Main mission script: player/enemy setup, POI spawning, Sacred Site tracking, attack/reinforce execution, victory/defeat logic, Conqueror Mode activation, UI updates. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Montgisard_InitData` | data | Initialize all mission booleans, ints, SGroups, EGroups |
| `Montgisard_SetupLocations` | data | Cache Sacred Site marker positions for reuse |
| `Montgisard_InitPatrolPaths` | data | Define 7 patrol marker paths with reverse routes |
| `Montgisard_AttackGroupsData` | data | Define fortress1 starting attack army composition |
| `Montgisard_SetupDiplomacy` | data | Set player relationships for 6 players |
| `Montgisard_SetupModifiers` | data | Apply capture-rate modifiers to all Templar unit types |
| `Montgisard_GetCurrentSites` | data | Return sites owned by a player or count |
| `Montgisard_InitObjectives` | objectives | Register and start all objectives, begin attack/reinforce rules |
| `Mission_SetupVariables` | core | Call data init functions at mission start |
| `Mission_SetupPlayers` | core | Initialize 6 players with AI and personalities |
| `Mission_SetRestrictions` | core | Remove wall/dock production for local player |
| `Mission_Start` | core | Start timers, reveal sites, begin objective init |
| `Montgisard_SpawnPointsOfInterest` | core | Deploy neutral POI units: rams, monks, fortress, mines, prison |
| `Montgisard_ConquerorTriggerSite` | core | Reveal and activate extra enemy camp for Conqueror Mode |
| `Montgisard_UpdatePointsOfInterest` | core | Check completion criteria for all 6 POIs |
| `Montgisard_RewardPointsOfInterest` | core | Spawn ally army and reveal monastery on all POI complete |
| `Montgisard_SpawnAllyArmy` | core | Deploy ally army wave at monastery |
| `Montgisard_LaunchAllyArmy` | core | Send ally army to attack enemy-held site |
| `Montgisard_SpawnNeutralVills` | core | Deploy 10 neutral villagers on farms across map |
| `Montgisard_OnEnemyBuildingDamage` | core | Detect player trebuchets attacking enemy buildings |
| `Montgisard_FocusTrebs` | core | Send enemy cavalry/infantry to target player trebuchets |
| `Montgisard_StartingUnits` | core | Deploy player starting army, villagers, and scout |
| `Montgisard_EnemyUnits` | core | Deploy all enemy starting armies at 4 Sacred Sites |
| `Montgisard_EnemyReinforcements` | core | Spawn reinforcement wave at each enemy-held fortress |
| `Montgisard_EnemyAttacks` | core | Select attack origin/target and launch enemy attack |
| `Montgisard_AttackTarget` | core | Build attack group and queue attack with warning UI |
| `Montgisard_LaunchAttack` | core | Deploy attack units, set Army path, show minimap route |
| `Montgisard_GetAttackUnitBP` | reinforcements | Get unit blueprint for attack wave by type/origin |
| `Montgisard_GetAttackUnitSpawnPoint` | reinforcements | Get spawn marker for unit type at given fortress |
| `Montgisard_GetAttackUnitStrength` | reinforcements | Calculate unit count by type, wave, origin, target |
| `Montgisard_GetAttackPath` | reinforcements | Return marker path between two Sacred Sites |
| `Montgisard_ReinforceData` | reinforcements | Select correct wave table, apply Conqueror scaling |
| `Montgisard_GetConquerorUnits` | reinforcements | Double all reinforcement counts for Conqueror Mode |
| `Montgisard_InitReinforceData` | reinforcements | Define tableWave1–6 with per-fortress unit compositions |
| `Montgisard_CreatePatrol` | reinforcements | Spawn patrol and start tracking rule |
| `Montgisard_TrackPatrol` | reinforcements | Reverse patrol direction when idle, remove if dead |
| `Montgisard_EnemyPatrols` | core | Create 7 patrols (spearmen + archers, 3+3 each) |
| `Montgisard_TrackSacredSites` | core | Main update: victory/defeat, medals, age-up, Conqueror check |
| `Montgisard_UpdateSacredSitesUI` | core | Add/remove minimap objective icons on ownership change |
| `Montgisard_UpdateSacredSitesBonuses` | core | Toggle Sacred Site bonus unit spawn rules on capture |
| `Montgisard_SacredSitesUnits` | core | Spawn 3 bonus units at captured site tent periodically |
| `Montgisard_GetUnitSBP` | core | Return age-appropriate Templar SBP for unit type |
| `Montgisard_SetSacredSiteBonuses` | core | Make tent EGroups invulnerable and non-targetable |
| `Montgisard_BonusUnitsOnAgeUp` | core | Spawn 10 commandery units matching age-up landmark |
| `Montgisard_CheckForRams` | core | Destroy remaining rams when all other attack units die |
| `Montgisard_AttackWarning` | core | Show reticule/hintpoint warning at attack origin |
| `Montgisard_AttackWarningUpdate` | core | Animate inner reticule expanding to outer radius |
| `Montgisard_GetInFormation` | core | Reorder enemy units after recapturing a site |
| `Montgisard_CheckForIdleAroundSS` | core | Command idle enemy units near sites to recapture |
| `Montgisard_GetAvailableSiteForAttack` | core | Pick enemy site without player units nearby for attack |
| `Montgisard_DisplayMinimapPath` | core | Show minimap arrow icons along attack route |
| `HC_Montgisard_IntroSetup` | core | Spawn all units and POIs for intro camera sequence |
| `HC_Montgisard_IntroTeardown` | core | Destroy intro units and create patrol 4 |
| `GetRecipe` | core | Return mission audio/NIS configuration table |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_SacredSitesPrimary` | Primary | Capture all 4 Sacred Sites; counter tracks sites held (0–4) |
| `SOBJ_SacredSitesTip` | Tip | UI hint about Sacred Sites mechanics |
| `SOBJ_SacredSitesTip_Build` | Tip | UI hint about building near sites |
| `OBJ_DefendTC` | Information | Fail mission if starting TC is destroyed |
| `OBJ_PointsOfInterest` | Optional | Complete 6 POIs (counter 0–6) for ally army reward |
| `OBJ_ConquerorMode` | Bonus | Phase 1: Capture SS1 within 3 min; Phase 2: Destroy camp within 3 min |
| `OBJ_ConquerorMedal` | Bonus | Complete all sites within 25 min in Conqueror Mode |
| `OBJ_GoldMedal` | Bonus | Capture all sites within 17 minutes (count-up timer) |
| `OBJ_SilverMedal` | Bonus | Capture all sites within 25 minutes |
| `OBJ_BronzeMedal` | Bonus | Capture all sites within 60 minutes |
| `OBJ_ConquerorTip` | Battle | Placeholder for Conqueror Mode UI |

### Difficulty

No `Util_DifVar` calls are present. Difficulty scaling is handled implicitly:

- **Conqueror Mode doubles** all reinforcement `numSquads` values via `Montgisard_GetConquerorUnits`
- **Conqueror Mode adds** wave-specific bonus units (+2 per type per fortress for waves 2–6)
- **Enemy upgrades** on Conqueror activation: Melee/Ranged Armor I+II, Melee/Ranged Damage I+II
- **Attack strength** (`attackStrenghtCM`) starts at 24 and increases by 4 per attack in Conqueror Mode
- **Post-Bronze scaling** (`attackStrenghtPostBronze`) starts at 20 and decreases by 4 per attack (min 8) after wave 5 in normal mode
- **Player reinforcements** timed to medal thresholds (see Timers section)

### Spawns

**Starting player army:** 5 Knight Templars (Age 3), 10 Archers (Age 2), 1 Ram, 1 Scout, 21 villagers (8 berries, 2 farm, 8 wood, 6 gold)

**Enemy starting garrisons per Sacred Site:**
- **SS1:** 16 Spearmen (Age 1) + 18 Archers (Age 2) = 34 squads
- **SS2:** 15 Archers (Age 2) + 5 MAA (Age 3) + 5 Horsemen (Age 3) + 10 Spearmen (Age 2) + 5 Crossbowmen (Age 3) = 40 squads
- **SS3:** 5 Knights (Age 3) + 10 Archers (Age 3) + 5 Horse Archers + 5 MAA (Age 3) + 10 Spearmen (Age 3) + 5 Crossbowmen (Age 3) = 40 squads
- **SS4:** 16 Spearmen (Age 4) + 5 Crossbowmen (Age 4) + 5 MAA (Age 4) + 5 Horsemen (Age 4) + 8 Archers (Age 4) + 8 Knights (Age 4) = 47 squads

**Reinforcement waves (tableWave1–6):** Each wave defines 4 unit types (archers, infantry, cavalry, siege) per fortress. Units escalate from Age 1–2 (wave 1) to Age 3–4 (wave 6). Typical wave spawns 3–4 squads per type per fortress. Siege appears from wave 2 onward (mangonels/springalds, 1 per fortress).

**Conqueror Mode reinforcements:** All `numSquads` doubled, plus per-wave bonus units (+2 in select categories).

**Attack composition:** 4 unit types (archers/infantry/cavalry/siege) + scaling rams. Unit counts vary by origin fortress emphasis:
- SS1: infantry-heavy (50% infantry, 25% archers, 25% cavalry)
- SS2: archer-heavy (50% archers, 25% infantry, 25% cavalry)
- SS3/SS4: cavalry-heavy (50% cavalry, 25% each other)

**POI defenders (active):**
- Rams POI: 4+4 Archers, 6 Spearmen, 1 Horseman (Age 2–4)
- Mining Camp 1: 3 Spearmen + 3 Archers (Age 1–2)
- Mining Camp 4: 4 Knights, 4 Archers, 2 Springalds (Age 3)
- Prison: 8 MAA + 8 Crossbowmen (Age 3)
- Fortress: 5 Horsemen, 5+5 MAA, 6 Archers, 6 Crossbowmen (Age 4)
- Extra Site (Conqueror): 6 MAA + 6 Crossbowmen + 6 Archers + 6 Spearmen (Age 3)

**Sacred Site capture bonuses:** On first capture, spawns 5–10 commandery/unique units matching site number. Every 90s, spawns 3 age-appropriate units (spearmen/archers/horsemen/knights by site).

**Player bonus reinforcements (non-Conqueror):**
1. Gold+30s: 10 Archers (Age 3)
2. Silver-3min: 12 MAA (Age 4) + 2 Trebuchets
3. Silver+2min: 14 Knight Templars (Age 4) + 3 Springalds
4. 40min mark: 12 Knights (Age 4) + 12 Crossbowmen (Age 4) + 3 Mangonels

**Age-up bonuses:** 10 units of the chosen commandery type per age advance (Hospitaller/Chevalier/Serjeant for Feudal, etc.).

### AI

- `AI_Enable` called for `enemyPlayer`, `enemyPlayer_2`, `neutralPlayer`, `mapPlayer`, `allyPlayer` (all true)
- All AI players use `"default_campaign"` personality
- **7 patrols** created with spearmen+archers (3+3 each), patrolling bidirectionally along marker paths
- `Montgisard_TrackPatrol` reverses patrol direction when idle, removes rule when patrol dies
- `Montgisard_CheckForIdleAroundSS` (30s interval): commands idle enemy units within 40 range of neutral/player sites to attack-move toward the site for recapture
- `Montgisard_FocusTrebs`: on detecting trebuchet damage to enemy buildings, sends cavalry (or infantry fallback) to target trebuchets; cooldown of 120s
- `Montgisard_GetInFormation`: reorders enemy units into archer/infantry/cavalry/siege rally positions after recapturing a site
- `Montgisard_GetAvailableSiteForAttack`: selects enemy-held site with no player units within 40 range as attack origin

### Timers

| Rule | Type | Interval/Delay | Purpose |
|------|------|----------------|---------|
| `Montgisard_EnemyReinforcements` | `Rule_AddInterval` | 360s (6 min) | Spawn reinforcement wave at all enemy-held fortresses |
| `Montgisard_EnemyAttacks` | `Rule_AddInterval` | 420s (7 min) | Launch attack from enemy site to player/neutral site |
| `Montgisard_TrackSacredSites` | `Rule_AddInterval` | 0.125s | Main game state update loop |
| `Montgisard_CheckForIdleAroundSS` | `Rule_AddInterval` | 30s | Command idle enemy to recapture nearby sites |
| `Montgisard_SacredSitesUnits` | `Rule_AddInterval` | 90s | Spawn 3 bonus units at player-held Sacred Site tent |
| `Montgisard_TrackPatrol` | `Rule_AddInterval` | 2s | Monitor and reverse patrol routes |
| `Montgisard_CheckForRams` | `Rule_AddInterval` | 0.5s | Kill orphaned rams in attack groups |
| `Montgisard_AttackWarningUpdate` | `Rule_AddInterval` | 0.125s | Animate reticule expansion for attack warning |
| `Montgisard_InitObjectives` | `Rule_AddOneShot` | 1s | Delayed objective initialization |
| `Montgisard_LaunchAttack` | `Rule_AddOneShot` | 15s | Delay attack spawn after warning |
| `Montgisard_RemoveMinimapPath` | `Rule_AddOneShot` | 120s | Clear minimap attack path arrows |
| `Montgisard_SetupAttackRuleForConqueror` | `Rule_AddOneShot` | 120s | Start Conqueror attack rule (300s interval) |
| `Montgisard_SetupReinforceRuleForConqueror` | `Rule_AddOneShot` | 60s | Start Conqueror reinforce rule (300s interval) |
| `Montgisard_ConquerorTriggerSite` | `Rule_AddOneShot` | 1s | Activate extra site if Conqueror Phase 1 expires |
| `OBJ_ConquerorMode` timer | COUNT_DOWN | 180s (3 min) | Phase 1: capture SS1; Phase 2: destroy camp |
| `OBJ_ConquerorMedal` timer | COUNT_DOWN | 1500s (25 min) | Complete all sites in Conqueror Mode |
| `OBJ_GoldMedal` timer | COUNT_UP | from 0 | Track time, fail at 17 min |
| `OBJ_SilverMedal` timer | COUNT_UP | from elapsed | Fail at 25 min |
| `OBJ_BronzeMedal` timer | COUNT_UP | from elapsed | Fail at 60 min |
| Ally army waves | `Rule_AddOneShot` | 0/5/8/10/15s | Staggered spawns for POI reward ally army |
| `Montgisard_RecaptureVoiceline` | `Rule_AddOneShot` | 15s | Play voice line on first enemy attack |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — imported by all 4 files; provides Cardinal framework, `Objective_*`, `Missionomatic_InitPlayer`, `Army_*`, `UnitEntry_DeploySquads`, `EventCues_CallToAction`
- `MissionOMatic/MissionOMatic_utility.scar` — imported by data, objectives, and reinforcements files; provides `Util_DifVar`, `Util_GetPosition`, `Util_GetPlayerOwner`, `Util_StartIntel`, `Util_ApplyModifier`
- `challenge_montgisard_objectives.scar` — imported by core
- `challenge_montgisard_reinforcements.scar` — imported by core
- `challenge_montgisard_data.scar` — imported by core

### Shared Globals
All files share a flat global namespace. Key shared globals include:
- `localPlayer`, `enemyPlayer`, `enemyPlayer_2`, `neutralPlayer`, `mapPlayer`, `allyPlayer` — player handles
- `eg_SacredSite_1`–`4` — Sacred Site entity groups
- `OBJ_SacredSitesPrimary`, `OBJ_DefendTC`, `OBJ_PointsOfInterest`, `OBJ_GoldMedal`, `OBJ_SilverMedal`, `OBJ_BronzeMedal`, `OBJ_ConquerorMode`, `OBJ_ConquerorMedal` — objective tables
- `conquerorActivated`, `triggerActivated`, `conquerorExpired` — Conqueror Mode state flags
- `totalReinforces`, `totalAttacks` — wave counters
- `reinforceRule`, `attackRule` — rule IDs for removal/replacement
- `sg_fortress1_starting`–`4` — enemy starting army SGroups
- `attackSGroups` — table of 5 SGroups for tracking active attack groups
- `completedPOI`, `totalPOI` — POI progress counters
- `missionTime`, `startTime` — timing state
- `EVENTS.*` — Intel event references (Victory, Defeat, Camera_Intro, etc.)

### Inter-file Function Calls
- Core calls `Montgisard_InitData()`, `Montgisard_InitPatrolPaths()`, `Montgisard_AttackGroupsData()`, `Montgisard_SetupLocations()` from data file
- Core calls `Montgisard_SetupDiplomacy()`, `Montgisard_SetupModifiers()`, `Montgisard_GetCurrentSites()` from data file
- Core calls `Montgisard_InitObjectives()` from objectives file
- Core calls `Montgisard_ReinforceData()`, `Montgisard_GetAttackUnitBP()`, `Montgisard_GetAttackUnitSpawnPoint()`, `Montgisard_GetAttackUnitStrength()`, `Montgisard_GetAttackPath()` from reinforcements file
- Core calls `Montgisard_CreatePatrol()`, `Montgisard_TrackPatrol()` from reinforcements file
- Objectives file references core globals (`conquerorActivated`, `missionTime`, `playerSitesHeld`, etc.) directly

### Blueprint References
- **Player (Templar):** `SBP.TEMPLAR.*` — full Templar roster including unique units (Knight Templar, Hospitaller, Chevalier Confrere, Serjeant, Teutonic Knight, Szlatcha Knight, Condottiero, Genoese Crossbow, Genitour, Heavy Spearman)
- **Enemy (Abbasid/Ayyubid):** `SBP.ABBASID_HA_01.*` — standard Abbasid roster; `SBP.AYYUBID_CMP.UNIT_TURKIC_HORSEARCHER_3_AYY` — Turkic Horse Archer; `SBP.AYYUBID_CMP.UNIT_LEADER_COMMANDER_AYY` / `UNIT_LEADER_SALADIN_KNIGHT_AYY` — Conqueror Mode leaders
- **Buildings:** `EBP.TEMPLAR.*` — Templar buildings (walls, dock removed via restrictions); Trebuchet blueprint `EBP.TEMPLAR.UNIT_TREBUCHET_4_CW_TEM` used for treb-detection
- **Upgrades:** Standard `UPG.COMMON.*` for tower/outpost upgrades, armor/damage upgrades; Templar age-up upgrades checked via `BP_GetUpgradeBlueprint("upgrade_age_*_com_*_tem")`
- **Custom event:** `CE_MONTGISARDCONQ` — sent on Conqueror Mode completion
