# Mongol Chapter 3: Lumen Shan

## OVERVIEW

Mongol Chapter 3 is a multi-phase blockade mission set at Lumen Shan in the 1260s. The player commands Mongol forces led by Liu Zheng, capturing Song-controlled territory and allied Chinese villages (Lumen, Bohekou), then constructing Chinese walls to block Song forces from moving north through mountain passes. After wall construction, the player must defend against 8 waves of Song wallbreaker armies. If the blockade fails (too many enemies escape north), a remedial Phase 4 launches a final sally the player must stop before 20 units escape south. The mission uses extensive AI pathfinding (cached paths between markers) to evaluate wall blockade effectiveness and guide enemy raiding/attack behavior.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `mon_chp3_lumen_shan.scar` | core | Main mission script: player setup, variables, restrictions, recipe, global rules, intro/outro sequences |
| `obj_lumen_phase1.scar` | objectives | Phase 1: destroy Song fort garrison, claim Lumen area |
| `obj_lumen_phase2.scar` | objectives | Phase 2: build walls to blockade passes, manage raiders and scouts |
| `obj_lumen_phase3.scar` | objectives | Phase 3: defend walls against 8 wallbreaker waves, track enemy escapes |
| `obj_lumen_phase4.scar` | objectives | Phase 4 (remedial): final sally intercept if blockade failed |
| `obj_lumen_secondary.scar` | objectives | Optional objectives: recruit Bohekou village, bridge hints |
| `training_lumen.scar` | training | Tutorial goals for bridge destruction/repair and Liu Zheng's ability |
| `mon_chp3_lumen_shan_automated.scar` | automated | Automated testing: checkpoint system, scripted army movements, wall construction |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Configure 4 players: Mongol, Song, China, Neutral |
| `Mission_SetupVariables` | core | Init SGroups, EGroups, paths, raiding, objectives |
| `Mission_SetRestrictions` | core | Lock resources, remove buildings/units, set tech |
| `Mission_Preset` | core | Color setup, global rules, AI cached paths, pickups |
| `Mission_Start` | core | Start OBJ_ClaimArea, lock music, init tutorial |
| `GetRecipe` | core | Define mission recipe with locations/modules/units |
| `Lumen_OnConstructionStart` | core | Track player wall construction positions for AI |
| `Lumen_CheckForExit` | core | Delete Song units at exit markers, increment counters |
| `Lumen_StartIntro` | core | Move intro unit groups to destination markers |
| `Lumen_StartOutro` | core | Deploy outro units, Song retreat sequence |
| `Lumen_GetValidPath` | core | Build randomized valid path through channel markers |
| `Lumen_SpawnPickups` | core | Spawn gold/food/wood pickups at marker positions |
| `Lumen_ResendMongolBuildings` | core | Replenish missing Mongol production buildings |
| `Lumen_OnEntityKilled` | core | Play stinger and walla when player walls destroyed |
| `Lumen_WatchForBridges` | core | Detect bridge onscreen, trigger hint objective |
| `Lumen_WatchIdleScouts` | core | Redirect idle Song scouts to exit markers |
| `Lumen_CheatDeleteEnemies` | core | Debug: destroy Song garrison modules and buildings |
| `LumenShan_InitObjectives_Phase1` | phase1 | Register OBJ_ClaimArea and SOBJ_DestroyFort |
| `Lumen_WatchPlayerPassage` | phase1 | Trigger Song ambush when Liu Zheng enters area |
| `Lumen_WatchPlayerBreach` | phase1 | Play positive stinger when player breaches fort |
| `Lumen_CheckLossLumen` | phase1 | Monitor if player lost Lumen village buildings |
| `Lumen_DisbandStartingAmbushers` | phase1 | Disband resist modules when player swarms area |
| `Lumen_RevealAroundLumen` | phase1 | Reveal fog of war around Lumen village |
| `LumenShan_InitObjectives_Phase2` | phase2 | Register OBJ_Blockade, SOBJ_Walls, SOBJ_Towers |
| `Lumen_EvaluateBlockade` | phase2 | Check cached paths to determine wall blockade success |
| `Lumen_UpdateCachedPath` | phase2 | Request AI high paths between Song markers |
| `Lumen_ManageRaiders` | phase2 | Spawn/redirect raid parties against player villages |
| `Lumen_RetreatBlockedRaiders` | phase2 | Redirect blocked raiders to alternate exits/gates |
| `Lumen_VanishBlockedRaiders` | phase2 | Despawn raiders that reach exit after blockage |
| `Lumen_NewScout` | phase2 | Spawn scout probe along randomized valid path |
| `Lumen_CheckChineseLoss` | phase2 | Fail if player loses all Chinese TCs and villagers |
| `Lumen_SetupLeaderHint` | phase2 | Show Liu Zheng construction boost ability hint |
| `LumenShan_InitObjectives_Phase3` | phase3 | Register OBJ_Defense, SOBJ_BlockadeSuccess/Failure |
| `Lumen_SpawnWallbreakers` | phase3 | Spawn attack waves with melee/ranged/siege composition |
| `Lumen_MaintainSallies` | phase3 | Collect idle Song units into roving army modules |
| `Lumen_RecallExistingUnits` | phase3 | Disband non-push modules, send units to staging |
| `Lumen_UpdatePathDisplay` | phase3 | Render enemy path icons on minimap |
| `Lumen_WarnPlayer` | phase3 | Alert player when enemies approach exit markers |
| `Lumen_IncrementStoppedSong` | phase3 | Increment blockade counter when wave defeated |
| `Lumen_OnWallDamage` | phase3 | Trigger speech on first wall damage event |
| `Lumen_OnWallDestroyed` | phase3 | Play stinger when player wall segment destroyed |
| `LumenShan_InitObjectives_Phase4` | phase4 | Register OBJ_Remedial, SOBJ_FinalChance |
| `Lumen_LaunchSongSally` | phase4 | Spawn large Song army heading south through villages |
| `Lumen_SecretCleanup` | phase4 | Delete unseen Song units to simplify Phase 4 |
| `Lumen_RedirectRemainingUnits` | phase4 | Disband all modules, redirect to attack villages |
| `Lumen_SetupStragglerModules` | phase4 | Create roving armies for Lumen/Bohekou stragglers |
| `Lumen_ManageStragglerModules` | phase4 | Split stragglers between towns, manage convergence |
| `Lumen_AssignStragglers` | phase4 | Merge nearby Song units into ReturnSally module |
| `LumenShan_InitObjectivesSecondary` | secondary | Register OBJ_Bohekou, SOBJ_GeneralToVillage, OBJ_HintBridge |
| `Lumen_StartBohekou` | secondary | Delayed start for Bohekou recruitment objective |
| `Lumen_CheckLossBohekou` | secondary | Monitor if player lost Bohekou village buildings |
| `Lumen_RevealAroundBohekou` | secondary | Reveal fog of war around Bohekou village |
| `MissionTutorial_Init` | training | Initialize tutorial system (currently disabled) |
| `MissionTutorial_AddHintToBrokenBridge` | training | Training goal for bridge repair with villagers |
| `Lumen_TriggerZhengHint` | training | Trigger Liu Zheng ability hint when onscreen |
| `AutoTest_OnInit` | automated | Initialize automated testing if CampaignAutoTest arg |
| `AutomatedLumen_RegisterCheckpoints` | automated | Register 4 test checkpoints with timeouts |
| `AutomatedLumen_Phase2_MovePlayerArmy` | automated | Deploy and move test army toward Song fort |
| `AutomatedLumen_Phase3_BuildWall_1` | automated | Spawn villagers and construct first test wall |
| `AutomatedLumen_Phase3_BuildWall_2` | automated | Spawn villagers and construct second test wall |
| `_AutomatedLumen_UnitReplenish` | automated | Replenish unit group when count drops below half |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_ClaimArea` | Primary | Phase 1: destroy Song fort and claim Lumen area |
| `SOBJ_DestroyFort` | Battle (child) | Destroy all buildings in `eg_song_military_camp` |
| `OBJ_Blockade` | Build | Phase 2: build walls to block all paths north |
| `SOBJ_Walls` | Build (child) | Evaluate blockade via cached path lengths (threshold: 15) |
| `SOBJ_Towers` | Build (child) | Build and upgrade a tower with springald/cannon (Easy/Normal only) |
| `OBJ_Defense` | Primary | Phase 3: survive 8 wallbreaker waves |
| `SOBJ_BlockadeSuccess` | Battle (child) | Counter tracking defeated wallbreaker waves (target: 8) |
| `SOBJ_BlockadeFailure` | Tip (child) | Fail counter: mission fails if 20 Song units escape north |
| `OBJ_Remedial` | Primary | Phase 4 (on Phase 3 fail): stop the Song return sally |
| `SOBJ_FinalChance` | Battle (child) | Fail counter: mission fails if 20 Song units escape south |
| `OBJ_Bohekou` | Optional | Recruit Bohekou village by sending units nearby |
| `SOBJ_GeneralToVillage` | Optional (child) | Move any Mongol unit near Bohekou marker |
| `OBJ_HintBridge` | Optional (secret) | Hint to destroy a wooden bridge when spotted onscreen |
| `OBJ_DebugComplete` | Primary (hidden) | Debug: force mission complete |

### Difficulty

All `Util_DifVar` arrays are ordered `{Easy, Normal, Hard, Expert}`.

| Parameter | Values | What it scales |
|-----------|--------|----------------|
| Raider horseman ratio | {0.8, 0.8, 0.6, 0.4} | Proportion of horsemen in raid parties |
| Raider knight ratio | {0.0, 0.0, 0.2, 0.3} | Knights added on Hard/Expert |
| Raider firelancer ratio | {0.2, 0.2, 0.2, 0.3} | Fire lancers in raids |
| Raider party limit | {1, 1, 2, 3} | Max concurrent raid parties |
| Raider party size | {12, 12, 18, 24} | Units per raid party |
| Raid timing | {30, 30, 25, 20} | Seconds between raids |
| Wallbreaker spawn delay | {15, 15, 30, 30} | Initial delay before first wallbreaker wave |
| Wallbreaker unit count | {12, 14, 16, 20} | Melee/ranged squad count per wave |
| Wallbreaker rams | {1, 1, 1, 1} | Battering rams per wave |
| Wallbreaker springalds | {0, 0, 1, 0} | Springalds on Hard |
| Wallbreaker mangonels | {0, 0, 0, 1} | Mangonels on Expert |
| Raid frequency modulo | {4, 4, 3, 2} | Wallbreaker wave interval for bonus raids |
| Song sally men-at-arms | {15, 15, 20, 25} | Phase 4 sally melee count |
| Song sally spearmen | {12, 12, 16, 20} | Phase 4 sally spear count |
| Song sally archers | {10, 10, 12, 14} | Phase 4 sally ranged count |
| Song sally crossbowmen | {8, 8, 10, 12} | Phase 4 sally crossbow count |
| Song sally repeater xbow | {6, 6, 9, 12} | Phase 4 sally elite ranged |
| Song sally grenadiers | {2, 2, 6, 10} | Phase 4 sally grenadiers |

**Difficulty-gated melee units**: Easy/Normal wallbreakers include militia; Hard adds grenadiers to ranged pool; Expert uses repeater crossbows and mangonels.

**SOBJ_Towers** only starts on Easy/Normal/Hard (not Expert).

### Spawns

- **Player start**: Liu Zheng (leader) + 25 fire lancers, 30 horse archers (2 groups of 15), 50 knights, 2 scouts
- **Song fort garrison**: 6 men-at-arms + 6 crossbowmen (Defend module)
- **Song resist groups**: 4 Defend modules (SongResist2–5) with spearmen/archers (8–20 per group, total ~62 units)
- **Allied villages**: Lumen (5 villagers) and Bohekou (6 villagers + 16 garrison troops: 8 spearmen + 8 repeater crossbows)
- **Wallbreaker waves** (Phase 3): 8 total waves, spawning every 50 seconds from southern markers. Each wave has randomized melee type + ranged type + rams (+ springald/mangonel on higher difficulty). Alternates between west/east spawn markers with modulo variation.
- **Bonus raids** (Phase 3): Triggered every N wallbreaker waves (difficulty-scaled), sending cavalry raid parties at player villages or random squads.
- **Song return sally** (Phase 4): Single large army (53–93 units depending on difficulty) spawns at northern marker, attacks through Lumen → Bohekou → south exit.
- **Straggler modules** (Phase 4): Disbanded enemy units reorganized into roving armies targeting Lumen and Bohekou.

### AI

- `AI_Enable(g_playerNeutral, false)` — neutral player AI disabled
- **Raiding_Init**: Configures Song raider system with 2 spawn locations (`mkr_song_south_2`, `mkr_song_south_3`), scout targets at north markers, cavalry composition scaled by difficulty. No probes, no active scouting, no rams.
- **AIPlayer_SetMarkerToUpdateCachedPathToPosition**: 16+ cached paths configured between north/south/village markers for Song pathfinding evaluation. Updates every 5 seconds.
- **RovingArmy_Init**: Used extensively for wallbreaker waves (ARMY_TARGETING_DISCARD), idle unit sallies (ARMY_TARGETING_CYCLE), straggler modules, and the return sally.
- **Defend modules**: SongFortGarrison, SongResist2–5 with 55-unit leash range and 35-unit combat range.
- **Raider blocking logic**: `Lumen_RetreatBlockedRaiders` cycles through alternate exits and player gates; `Lumen_VanishBlockedRaiders` despawns raiders that reach exits.
- **Idle scout management**: `Lumen_WatchIdleScouts` redirects idle Song scouts to map exits for despawn.

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| `Lumen_CheckForExit` | 1s | Continuously delete Song units at exit markers, increment fail counters |
| `Lumen_OnConstructionStart` | Global event | Track wall construction for AI raider targeting |
| `Lumen_OnEntityKilled` | Global event | Stinger/walla on player wall destruction (20s cooldown) |
| `Lumen_WatchForBridges` | 1s | Detect bridge onscreen, start hint objective |
| `Lumen_WatchIdleScouts` | 3s | Redirect idle enemy scouts to exits |
| `Lumen_UpdateCachedPath` | 3s | Refresh AI pathfinding between Song markers |
| `Lumen_NewScout` | 20s | Spawn new scout probe along random path |
| `Lumen_ManageRaiders` | 1s | Manage raid party creation and targeting |
| `Lumen_StartBohekou` | OneShot 60s | Delayed start for Bohekou optional objective |
| `Lumen_SpawnWallbreakers` | OneShot {15/15/30/30}s, then 50s interval | Spawn wallbreaker waves in Phase 3 |
| `Lumen_MaintainSallies` | 2s | Collect idle Song units into roving armies |
| `Lumen_UpdatePathDisplay` | 5s | Render enemy path markers on minimap |
| `Lumen_WarnPlayer` | 1s | Alert cue when enemies near exit (45s cooldown) |
| `Lumen_CheckLossLumen` | 3s | Monitor Lumen village building count |
| `Lumen_CheckLossBohekou` | 3s | Monitor Bohekou village building count |
| `Lumen_ManageStragglerModules` | 3s | Split/redirect Phase 4 stragglers between towns |
| `Lumen_AssignStragglers` | 1s | Merge roaming Song into return sally module |
| `Lumen_ResendMongolBuildings` | Interval | Replenish missing Mongol production structures |
| `Lumen_WatchPlayerPassage` | 1s | Trigger ambush when Liu Zheng passes marker |
| `Lumen_DelayedHalfBlockedVO` | OneShot 1.5s | Play VO after one side of map blocked |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `mon_chp3_lumen_shan.scar` | `MissionOMatic/MissionOMatic.scar`, `obj_lumen_phase1.scar`, `obj_lumen_secondary.scar`, `training_lumen.scar`, `mon_chp3_lumen_shan_automated.scar` |
| `obj_lumen_phase1.scar` | `obj_lumen_phase2.scar` |
| `obj_lumen_phase2.scar` | `obj_lumen_phase3.scar` |
| `obj_lumen_phase3.scar` | `obj_lumen_phase4.scar` |
| `training_lumen.scar` | `training/campaigntraininggoals.scar` |
| `mon_chp3_lumen_shan_automated.scar` | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/modules/module_rovingarmy.scar` |

### Shared Globals

- **Players**: `g_playerMongol`, `g_playerSong`, `g_playerChina`, `g_playerNeutral`
- **Leader**: `g_leaderLiuZheng` (Liu Zheng campaign leader, initialized via `Missionomatic_InitializeLeader`)
- **Path system**: `g_pathChecks` (4 cached paths: west, westAlt, east, eastAlt), `g_validPathStructures` (marker adjacency graph)
- **Raiding**: `g_raidSystem` (via `Raiding_Init`), `g_idleTracker`, `g_maxIdleLeeway`, `g_lastWallPos`
- **Phase 3**: `g_wallbreakerWaveCount` (8), `g_songAttackersPhase3`, `g_attackersSoFar`, `g_wallbreakerNextIdx`, `g_songPushComplete`
- **Phase 4**: `g_moduleReturnSally`, `g_songReliefActive`, `g_songSallyActive`, `g_stragglersLumen`, `g_stragglersBohekou`
- **Exit tracking**: `g_escapeWarningTimer` (45s), `g_escapeWarningCount`, `g_failureThresholdCrossed`, `g_finaleThresholdCrossed`
- **SGroups**: `sg_all_intro_mongols`, `sg_bohekou_troops`, `sg_outro_*` (multiple)
- **EGroups**: `eg_song_fort_keep`, `eg_village_lumen`, `eg_village_bohekou`, `eg_bridges_wood`, `eg_player_walls`, `eg_songterritory`, `eg_song_walls`

### Inter-file Function Calls

- Core calls: `LumenShan_InitObjectives_Phase1()`, `LumenShan_InitObjectives_Phase2()`, `LumenShan_InitObjectives_Phase3()`, `LumenShan_InitObjectives_Phase4()`, `LumenShan_InitObjectivesSecondary()` (from `Mission_SetupVariables`)
- Phase chain: Phase 1 complete → starts `OBJ_Blockade` (Phase 2) → complete → starts `OBJ_Defense` (Phase 3) → fail → starts `OBJ_Remedial` (Phase 4)
- Phase 3 references `Lumen_RecallExistingUnits`, `Lumen_SpawnWallbreakers`, `Lumen_MaintainSallies`, `Lumen_UpdatePathDisplay`, `Lumen_WarnPlayer` (defined in phase3 file)
- Phase 4 calls `Lumen_SecretCleanup`, `Lumen_LaunchSongSally`, `Lumen_RedirectRemainingUnits` (defined in phase4 file)
- Secondary calls `Lumen_RevealAroundBohekou` (defined in secondary file)
- Training: `MissionTutorial_Init()` called from `Mission_Start()`; `MissionTutorial_AddHintToBrokenBridge()` called from `Lumen_WatchForBridges`
- Automated: `AutoTest_OnInit()` called from `Mission_Preset()`; references `OBJ_ClaimArea`, `OBJ_Bohekou`, `OBJ_Blockade`, `OBJ_Defense` from objective files
- MissionOMatic prefabs used: `RovingArmy`, `Defend`, `UnitSpawner`, `TownLife`, `Raiding`, `MarkerPaths`, `Location`
