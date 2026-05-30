# Mongol Chapter 3: Xiangyang 1273

## OVERVIEW

Xiangyang 1273 is a three-phase siege mission where the Mongol player (Imperial age) with leaders Ismail and Liu Zheng besieges the twin Song Dynasty cities of Fancheng and Xiangyang. Phase 1 requires building a Huihui Pao (Great Trebuchet) while defending allied trade camps from Song cavalry raids and maintaining 9 active Silk Road traders. Phase 2 tasks the player with breaching Fancheng by constructing dirt bridges across a moat, entering the city with 6+ units, defeating the garrison, and razing the barbican landmark — all while heavily fortified towers and walls receive massive defensive modifiers. Phase 3 crosses to Xiangyang proper: destroy the keep, repair the burned twin-city bridge, and storm the palace to win. The mission features a dynamic garrison repositioning system that shifts Fancheng defenders toward active bridge construction or siege attack points, an escalating Raiding system with difficulty-scaled cavalry raids, and an achievement tracker for keeping all Huihui Pao alive.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp3_xiangyang_1273.scar | core | Main mission setup: 4 players, variables, restrictions, recipe with modules, raiding system, bridge/wall tracking, defense modifiers, outro parade |
| obj_xiangyang2_phase1.scar | objectives | Phase 1 objectives — build Huihui Pao trebuchet, optional Silk Road trader count |
| obj_xiangyang2_phase2.scar | objectives | Phase 2 objectives — breach Fancheng: moat bridges, enter city, defeat garrison, raze barbican, optional falcon use |
| obj_xiangyang2_phase3.scar | objectives | Phase 3 objectives — sack Xiangyang: destroy keep, repair twin-city bridge, storm palace, final rush waves |
| obj_xiangyang2_secondary.scar | objectives | Secondary objective — protect allied trade partner markets (west and south) |
| training_xiangyang2.scar | training | Tutorial hints for Ismail (falcon), infantry repair, Liu Zheng construction ability, and Silk Road traders (PC + Xbox) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | core | Configure 4 players: Mongol, Song, Yuan ally, Neutral |
| Mission_SetupVariables | core | Init groups, leaders, raiding system, objectives, difficulty vars |
| Mission_SetRestrictions | core | Auto-upgrades, resources, lock gates, boost defences, spawn landmark |
| Mission_Preset | core | Spawn buildings, armies, bridges, traders, wall listeners, modifiers |
| Mission_Start | core | Apply tower range mods, start OBJ_Prepare, delayed hints |
| GetRecipe | core | Define recipe: locations, RovingArmy/Defend/UnitSpawner modules |
| Xiangyang1273_OnConstructionComplete | core | Track Huihui Pao construction, complete trebuchet objective |
| Xiangyang1273_OnSquadBuilt | core | Grant infantry_repair ability to new infantry squads |
| Xiangyang1273_WatchFalcons | core | Complete falcon objective when used near trigger markers |
| Xiangyang1273_UpgradeBridges | core | Convert finished dirt bridges to walkable, set invulnerable |
| Xiangyang1273_OutroParade | core | Spawn cavalry parade and cheering units for outro NIS |
| Xiangyang_BoostDefences | core | Apply massive damage/armor/range/fire modifiers to Song defences |
| Xiangyang1273_RemoveHealthMods | core | Remove received_damage modifiers from towers and walls |
| Xiangyang1273_ManageRaiders | core | Spawn/redirect cavalry raid parties targeting player economy |
| Xiangyang1273_VanishRaiders | core | Despawn raiders that reach exit markers |
| Xiangyang1273_OnEntityKilled | core | Track tower kills, update raid composition, missing bridge VO |
| Xiangyang1273_OnDamageReceived | core | Track siege attack position for garrison aggro shifting |
| Xiangyang1273_IsFailed | core | Fail if no military units + no villagers + no TC |
| Xiangyang1273_ListenForWallDestruction | core | Play positive stinger on first wall section destroyed |
| Xiangyang1273_WatchForMissingStone | core | Offer Silk Road hint if stone < 1000 after 3 minutes |
| Xiangyang1273_HandlePrematureBridgeConstruction | core | Manage twin-city bridge immunity, unlock gates, prevent softlock |
| Xiangyang1273_OnSquadKilled | core | Warn player when units killed in tower danger zones |
| Xiangyang1273_BurnCentralBridge | core | Set twin-city bridge to 30% health and ignite it |
| Xiangyang1273_BridgeReminder | core | Show bridge objective banner or play VO after 150s |
| Xiangyang1273_SpawnXiangyangGuards | core | Spawn difficulty-scaled defenders into 5 Xiangyang Defend modules |
| Achievement_CheckHuiHuiPaoDestroyed | core | Track Huihui Pao deaths for achievement #20 |
| Xiangyang1273_InitObjectives_Phase1 | phase1 | Register OBJ_Prepare, SOBJ_BuildTrebuchet, SOBJ_OptUseSilkRoad |
| Xiangyang1273_CheckTraders | phase1 | Monitor active trader count, update counter objective |
| Xiangyang1273_SilkRoadReminder | phase1 | Play trader hint VO after 90s if incomplete |
| Xiangyang1273_InitObjectives_Phase2 | phase2 | Register OBJ_BreachCity and 6 sub-objectives |
| Xiangyang1273_ShiftFanchengGarrison | phase2 | Reposition defenders toward active bridges or siege attacks |
| Xiangyang1273_CollapseDefense | phase2 | Collapse archer modules into inner garrison on city entry |
| Xiangyang1273_MonitorInnerDefense | phase2 | Rearrange inner defenders when forces shrink by chunk size |
| Xiangyang1273_ArrangeInnerDefense | phase2 | Redistribute remaining defenders to fewer defense positions |
| Xiangyang1273_WatchForHuihuipaoAttack | phase2 | Trigger VO when Huihui Pao damages Song walls |
| Xiangyang1273_WatchForBarbicanBypass | phase2 | Force-complete barbican/garrison objectives to prevent softlock |
| Xiangyang1273_InitObjectives_Phase3 | phase3 | Register OBJ_SackXiangyang, keep/bridge/palace sub-objectives |
| Xiangyang1273_WatchForKeepAttack | phase3 | Spawn counter-attack squads when keep takes damage |
| Xiangyang1273_KeepAvengers | phase3 | Send avenger units across bridge to attack keep assailants |
| Xiangyang1273_WatchForStorm | phase3 | Detect player in Xiangyang, trigger escalating militia rushes |
| Xiangyang1273_SpawnFinalRush | phase3 | Deploy militia waves scaling with wave index |
| Xiangyang1273_Retaliation | phase3 | Periodic counter-attacks from Xiangyang on Normal+ difficulty |
| Xiangyang1273_CheckInCity | phase3 | Play VO when 6+ player units enter Xiangyang |
| Xiangyang1273_InitObjectivesSecondary | secondary | Register OBJ_AlliedTradePartners, track market destruction |
| MissionTutorial_Init | training | Initialize modal hover callback for training hints |
| Xiangyang1273_TriggerIsmailHint | training | Show Ismail falcon ability hint when on screen |
| Xiangyang1273_TriggerInfantryRepairHint | training | Show infantry bridge repair hint when infantry on screen |
| Xiangyang1273_TriggerLiuZhengHint | training | Show Liu Zheng construction ability hint |
| Xiangyang1273_TriggerSilkRoadHint | training | Show Silk Road trader hint at Karakorum landmark |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_Prepare | Primary | Phase 1 — prepare siege by building a Huihui Pao |
| SOBJ_BuildTrebuchet | Sub (Build) | Build one Great Trebuchet (Huihui Pao) |
| SOBJ_OptUseSilkRoad | Sub (Optional) | Have 9 active traders on the Silk Road |
| OBJ_BreachCity | Primary | Phase 2 — breach and capture Fancheng |
| SOBJ_OptUseFalcon | Sub (Optional) | Use falcon ability near two trigger markers |
| SOBJ_CrossMoat | Sub (Build) | Construct dirt bridges across the moat to 100% health |
| SOBJ_MoatHintpoints | Sub (Secret) | Hidden objective providing bridge UI hintpoints |
| SOBJ_EnterCity | Sub (Primary) | Move 6+ player units inside Fancheng walls |
| SOBJ_DefeatGarrison | Sub (Battle) | Kill all Fancheng garrison units (progress bar) |
| SOBJ_RazeLandmark | Sub (Battle) | Destroy Fancheng barbican landmark |
| OBJ_SackXiangyang | Primary | Phase 3 — sack the city of Xiangyang |
| SOBJ_BombKeep | Sub (Battle) | Destroy the Xiangyang keep |
| SOBJ_RepairBridge | Sub (Build) | Repair the twin-city bridge to 100% |
| SOBJ_StormPalace | Sub (Battle) | Burn the Xiangyang palace below 50% health |
| OBJ_AlliedTradePartners | Information | Protect allied west and south trade markets |
| OBJ_DebugComplete | Debug | Cheat: burn palace and complete mission |

**Flow:** OBJ_Prepare → OBJ_BreachCity (on trebuchet built) → [SOBJ_CrossMoat + SOBJ_EnterCity → SOBJ_DefeatGarrison + SOBJ_RazeLandmark] → OBJ_SackXiangyang (on Fancheng cleared) → [SOBJ_BombKeep → SOBJ_RepairBridge → SOBJ_StormPalace] → Mission_Complete.

### Difficulty

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| g_allyCounts | 60 | 50 | 45 | 40 | Yuan allied army size (fewer allies on harder) |
| g_enemyCountWalls | 6 | 8 | 12 | 14 | Archer count per wall defence module (×6 modules) |
| g_enemyCountGarrison | 18 | 26 | 34 | 40 | Fancheng garrison size per guard group (×3 groups) |
| raiderComposition horseman | 0.7 | 0.7 | 0.5 | 0.4 | Horseman ratio in raid parties |
| raiderComposition knight | 0.15 | 0.15 | 0.25 | 0.3 | Knight ratio in raid parties |
| raiderComposition firelancer | 0.15 | 0.15 | 0.25 | 0.3 | Fire lancer ratio in raid parties |
| partyLimit | 2 | 2 | 3 | 4 | Max simultaneous raid parties |
| partySize | 12 | 12 | 14 | 18 | Units per raid party (grows +1 each raid) |
| raidTiming | 45 | 45 | 42 | 40 | Seconds between raid spawns |
| partySize max cap | 20 | 20 | 24 | 28 | Maximum raid party size cap |
| Xiangyang guards (per module) | 8-36 | 8-36 | 10-24 | 12-18 | Xiangyang defender counts (5 guard groups) |
| retaliation timer | 180 | 180 | 135 | 90 | Seconds between Xiangyang counter-attacks |
| retaliation militia | 18 | 24 | 0 | 0 | Militia count in retaliation waves |
| retaliation melee | 0 | 0 | 10 | 12 | Spearman count in retaliation waves |
| retaliation ranged | 0 | 0 | 12 | 16 | Crossbowman count in retaliation waves |

**Note:** Raiding only targets the player on Normal+ when idle (Story mode retreats raiders). Retaliation system only active on Normal+ difficulty.

### Spawns

**Starting Army (Mongol player):**
- PlayerArmy1: 1 Ismail, 8 MAA, 12 spearmen, 12 archers (at mkr_yuan_army_1)
- PlayerArmy2: 1 Liu Zheng, 16 MAA (Chinese), 20 repeater crossbowmen, 18 fire lancers (at mkr_yuan_army_2)
- PlayerIntroScouts: 1 scout (spawned damaged at 25% HP, march-in)
- PlayerTripwire1/2: 4 spearmen + 4 archers each (outpost positions)
- PlayerVillagersA: 6 villagers (sheep/wood assignments)
- PlayerVillagersB: 3 villagers (wood)
- PlayerTraders1/2: 6 trade carts total (3 per route, auto-trading)

**Player Base:** Mongol buildings spawned programmatically — TC (moving), barracks, archery range, 2 stables, Kurultai, Stupa, 2 houses (moving), 2 pastures, arsenal, smithy, Karakorum (Silk Road landmark).

**Allied Yuan Armies (RovingArmy modules):**
- AllyDefenseWest/South: g_allyCounts units each — 25% spearmen, 25% MAA, 20% crossbowmen, 20% repeater crossbows, 10% grenadiers.

**Song Wall Defenders (6 UnitSpawner modules):**
- SongSiegeDefence1-6: g_enemyCountWalls archers each, positioned at countersiege markers around Fancheng.

**Fancheng Garrison (3 UnitSpawner modules):**
- FanchengGuards1-2: g_enemyCountGarrison units — 25% spearmen, 25% MAA, 20% crossbowmen, 20% repeater crossbows, 10% grenadiers.
- FanchengGuards3: g_enemyCountGarrison × 0.5 — spearmen + MAA only.

**Xiangyang Guards (spawned on Phase 2 complete):**
- Guards1-2: 4-6 spearmen, 0-6 MAA, 4-8 archers, 0-4 repeater crossbows, 0-2 grenadiers.
- Guards3: 20-32 spearmen + 8-20 MAA (large melee garrison).
- Guards4: 12-16 MAA + 1-3 springalds.
- Guards5: 18-36 knights + 0-18 fire lancers.

**Song Raiding Parties:** Cavalry raids from mkr_song_harass_1/2, targeting Yuan camps. Composition: horsemen/knights/fire lancers (difficulty-scaled ratios). After 8 tower kills, mangonels added at 5% ratio; after 16 kills, 10%.

**Final Rush Waves (Phase 3):** Triggered when 12×waveIdx player units enter Xiangyang. Each wave spawns 30+(waveIdx×4) militia. Up to 4 waves, minimum 15s apart.

**Keep Avengers:** When keep attacked, spawn 3 spearmen + 3 MAA + 6 archers on 10s cooldown, attack the keep's assailants.

**Xiangyang Retaliation (Normal+):** Periodic attacks every 90-180s when no player units in city. Militia/spearmen/crossbowmen composition varies by difficulty. If bridge destroyed, Song spawns 4 villagers to repair it.

### AI

- **AI_Enable:** `g_playerNeutral` AI disabled (neutral-holder only). Song and Yuan use MissionOMatic modules.
- **Raiding_Init:** Full raiding system for Song — 2 spawn locations, 3 scout targets, party limits/sizes/timing all difficulty-scaled. `sendProbes = false`, `activeScouting = false`.
- **Raiding_UpdateComposition:** Dynamically adds mangonels to raid parties after player scores tower kills (8 and 16 thresholds).
- **Defend modules:** XiangyangGuards1-5 with combatRange 30-45 and leashRange 40-55.
- **RovingArmy modules:** AllyDefenseWest/South with `ARMY_TARGETING_REVERSE` (patrol between two markers).
- **Garrison shifting:** `Xiangyang1273_ShiftFanchengGarrison` dynamically splits 6 SongSiegeDefence modules across 3 bridge positions based on bridge health thresholds (0.33, 0.66) and siege attack aggro position. Overrides to focus all defenders on the bridge closest to active siege.
- **Inner defense collapse:** On city entry, all archer modules merge into `sg_fancheng_last_stand`, distributed across 12 inner defense markers, progressively consolidated as units are lost.
- **PlayerUpgrades_Auto:** Mongol (selective), Song (full), Yuan (full).

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| Xiangyang1273_ManageRaiders | 120s delay, 75s interval | Spawn and direct Song cavalry raid parties |
| Xiangyang1273_UpgradeBridges | 1s interval | Check bridge health, convert to walkable at 100% |
| Xiangyang1273_WatchForMissingStone | 1s interval | Offer Silk Road hint if stone low after 180s |
| Xiangyang1273_ShiftFanchengGarrison | 1s interval | Reposition wall defenders toward active threats |
| Xiangyang1273_WatchForBarbicanBypass | 1s interval | Force-complete objectives if player bypasses to Xiangyang |
| Xiangyang1273_MonitorInnerDefense | 1s interval | Rearrange inner defenders when chunk lost |
| Xiangyang1273_BridgeReminder | 150s one-shot | Remind player to build moat bridges |
| Xiangyang1273_DelayLiuZhengHint | 30s one-shot | Show Liu Zheng construction hint after delay |
| Xiangyang1273_DelayedHint | 60s one-shot | Show Ismail hint after mission start |
| Xiangyang1273_HandlePrematureBridgeConstruction | 20s delay, 0.5s interval | Manage bridge fire immunity and gate unlocking |
| Xiangyang1273_WatchForKeepAttack | EGroup event | Spawn defenders when keep takes damage (10s cooldown) |
| Xiangyang1273_KeepAvengers | 1s interval | Send avenger units to attack keep assailants |
| Xiangyang1273_TrackCooldown | 1s interval | Decrement keep defense cooldown timer |
| Xiangyang1273_WatchForStorm | 1s interval | Detect player in Xiangyang, trigger militia rushes |
| Xiangyang1273_Retaliation | 90s delay, 1s interval | Periodic counter-attacks from Xiangyang (Normal+) |
| Xiangyang1273_CheckInCity | 1s interval | Play VO when player enters Xiangyang |
| Xiangyang1273_CheckTraders | 1s interval | Monitor active trader count for Silk Road objective |
| Xiangyang1273_SilkRoadReminder | 90s one-shot | Play trader hint VO if objective incomplete |
| Xiangyang1273_Unreveal | 0.125s one-shot | Remove full map reveal after initial explore |

### Atmosphere & Audio

- `Xiangyang_BoostDefences`: Walls receive 0.06× received damage, towers 0.5× received damage + 50× armor + 5× cannon damage + 0.1× reload + 2.0× range. Keep gets 8× damage and 2.4× range on 22 hardpoints.
- Tower range temporarily set to 2.0× during intro, reduced to 1.7× at `Mission_Start`.
- `Game_TransitionToState`: "subtropical_morning_smoky" at Phase 3 start, "subtropical_morning_hazy" at Phase 3 complete.
- `Music_LockIntensity`: MUSIC_TENSE_COMBAT for 20s at start, MUSIC_TENSE_RARE at city entry, MUSIC_TENSE_COMBAT_RARE at Phase 3.
- Twin-city bridge set invulnerable to prevent cannon hitbox damage.
- Khan spawning disabled via `khan_spawning_enabled = false`.
- Trader speed boosted 2× and build time halved to prevent grind.
- Achievement #20 "Boom Boom Pao": tracked via `huihuiPaoDestroyed` flag, sends `CE_ACHIEVHUIHUIPAOSURVIVES` on mission complete if no Huihui Pao lost.

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core campaign framework
- `obj_xiangyang2_secondary.scar` — Secondary objectives (imported by core)
- `obj_xiangyang2_phase1.scar` — Phase 1 objectives (imported by core)
- `obj_xiangyang2_phase2.scar` — Phase 2 objectives (imported by phase1, chains to phase2)
- `obj_xiangyang2_phase3.scar` — Phase 3 objectives (imported by phase2, chains to phase3)
- `training_xiangyang2.scar` — Tutorial hints (imported by core)
- `training.scar` + `training/campaigntraininggoals.scar` — Shared training system (imported by training file)

### Shared Globals
- `g_playerMongol`, `g_playerSong`, `g_playerYuan`, `g_playerNeutral`: Player references across all files
- `g_leaderIsmail`, `g_leaderLiuZheng`: Leader tables used by core, objectives, training
- `sg_huihuipao`: Tracks all player Huihui Pao across core and objectives
- `sg_intro_troops`: Starting army shared between core cheat functions and Phase 2 cheat
- `eg_moat_bridges`, `eg_bridge_1/2/3`: Bridge egroups shared between core (upgrade) and Phase 2 (completion)
- `eg_twin_city_bridge`: Twin-city bridge shared between core (invulnerability) and Phase 3 (repair objective)
- `eg_fancheng_barbican`, `eg_xiangyang_keep`, `eg_xiangyang_palace`: Landmark egroups for Phase 2/3 objectives
- `eg_fancheng_walls`, `eg_xiangyang_walls`: Wall egroups for destruction listening
- `g_highestMoatHealth`: Bridge progress tracked in core and Phase 2
- `g_siegeAttackAggro`: Aggro position table shared between core damage handler and Phase 2 garrison shift
- `sg_fancheng_last_stand`: Created in Phase 2 collapse, monitored by inner defense system
- `g_innerDefense`: 12-marker table for inner city defense positions
- `g_raidSystem`: Raiding system table (from Raiding_Init) referenced by ManageRaiders
- `g_wallDestructionStung`: Flag preventing repeated wall destruction stingers
- `g_bridgeBurnt`: Prevents double-burning the twin-city bridge
- `huihuiPaoDestroyed`: Achievement flag set by core, checked in Phase 3 completion
- `EVENTS.*`: Intel event references (FallOfXiangyang_Intro/Outro, HuihuiPao, Fancheng_Complete, BridgeComplete, InFancheng, Xiangyang_Start, Keep_Start, KeepDown, Palace_Start, ProtectAllies, etc.)
- `eg_market_1`, `eg_market_2`: Allied market egroups for secondary objective failure check

### Inter-File Function Calls
- Core → `Xiangyang1273_InitObjectives_Phase1()`, `Xiangyang1273_InitObjectives_Phase2()`, `Xiangyang1273_InitObjectives_Phase3()`, `Xiangyang1273_InitObjectivesSecondary()` (in respective objective files)
- Phase 1 → `Xiangyang1273_ManageRaiders()` (in core, via Rule_AddInterval)
- Phase 2 → `Xiangyang1273_ShiftFanchengGarrison()`, `Xiangyang1273_SpawnXiangyangGuards()`, `Xiangyang1273_BurnCentralBridge()`, `Xiangyang1273_RemoveHealthMods()`, `Xiangyang1273_IsFailed()` (in core)
- Phase 3 → `Xiangyang1273_SpawnXiangyangGuards()`, `Xiangyang1273_BurnCentralBridge()`, `Xiangyang1273_IsFailed()`, `Mission_Complete()`, `Mission_Fail()` (in core)
- Training → `MissionTutorial_Init()` called from core's `Mission_Start()`

### MissionOMatic Module References
- `Missionomatic_InitializeLeader()`: Initialize Ismail and Liu Zheng leaders with neutral holder
- `MissionOMatic_FindModule()`: Locate SongSiegeDefence1-6, XiangyangGuards1-5 modules by descriptor
- `Defend_AddSGroup()`: Add spawned guard units to Defend modules
- `Missionomatic_SetGateLock()`: Lock/unlock Song and allied gates
- `Raiding_Init()`, `Raiding_TriggerRaid()`, `Raiding_CountParties()`, `Raiding_PruneParties()`, `Raiding_SetPartyLimit()`, `Raiding_UpdateComposition()`, `Raiding_CountIdleRaiders()`, `Raiding_RemoveParty()`: Full raiding system API
- `RovingArmy_SetTarget()`: Redirect retreating raiders
- `MissionOMatic_HintOnHover()` / `MissionOMatic_HintOnHover_Xbox()`: Training hint system
- `MissionOMatic_SGroupCommandDelayed()`: Delayed attack commands for keep avengers
- `SpawnGarrisonsIntoEGroup()`: Garrison Xiangyang keep with 15 archers
- `UnitEntry_DeploySquads()`: Used extensively for spawning armies, guards, and parade units
- `PlayerUpgrades_Auto()`: Auto-upgrade system for all players
- `Util_UnitParade()`: Outro cavalry parade

### Blueprint References
- `SBP.MONGOL.UNIT_ISMAIL_CMP_MON`: Campaign Ismail leader
- `SBP.MONGOL.UNIT_LIU_ZHENG_CMP_MON`: Campaign Liu Zheng leader
- `SBP.MONGOL.UNIT_GREAT_TREBUCHET_CMP_MON`: Huihui Pao (Great Trebuchet)
- `SBP.MONGOL.BUILDING_*_MOVING_MON`: Mobile Mongol structures (TC, house, all military)
- `EBP.CHINESE.BUILDING_DEFENSE_WALL_CHI`, `WALL_GATE_CHI`, `WALL_BASTION_CHI`, `TOWER_CHI`, `KEEP_CHI`: Song fortification blueprints
- `EBP.MONGOL.BUILDING_WONDER_AGE2_KARAKORUM_MON`: Silk Road landmark (Karakorum)
- `EBP.MONGOL.BUILDING_WONDER_AGE1_KURULTAI_MON`, `AGE3_STUPA_MON`: Player base landmarks
- `BP_GetAbilityBlueprint("infantry_repair")`: Granted to all Mongol infantry for bridge construction
- `BP_GetAbilityBlueprint("leader_falcon_sight")`: Ismail falcon ability
- `BP_GetAbilityBlueprint("leader_construction_activated")`: Liu Zheng construction ability
- `BP_GetEntityBlueprint("bridge_dirt_long_unfinished")` / `"bridge_dirt_long"`: Bridge conversion blueprints
- `UPG.COMMON.UPGRADE_TOWER_CANNON`, `UPGRADE_KEEP_ARROWSLITS`, `UPGRADE_KEEP_CANNON`: Defence upgrades
