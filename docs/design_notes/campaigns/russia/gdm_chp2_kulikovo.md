# Russia Chapter 2: Kulikovo

## OVERVIEW

Battle of Kulikovo (1380), the third mission in "The Rise of Moscow" campaign. The player controls Moscow (Rus, Castle Age) and must defend against 10 waves of Golden Horde (Mongol, Feudal Age) attacks across three successive defense lines: the Smolka River fords, a central hill, and the Don River crossing. The mission begins with a preparation phase where Prince Dmitry visits villages to recruit soldiers and regroups with Rus allied armies. A hidden cavalry detachment accumulates in a forest during the battle and can be signaled once to charge. Allies (Rus Principalities, player3) autonomously hold three lanes via RovingArmy modules while the player reinforces key positions. Victory is achieved by surviving all 10 waves; failure occurs if the Mongols breach the Don River crossing or the player army is destroyed.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp2_kulikovo.scar` | core | Main mission setup: players, recipe, intro/outro cinematics, player spawning, support functions |
| `kulikovo_wavevariables.scar` | data | Unit composition tables for all 10 Mongol waves with difficulty-scaled squad counts |
| `kulikovotraininggoals.scar` | training | Stub training goal for village visit prompts |
| `obj_cavdetachment.scar` | objectives | Cavalry detachment accumulation, custom UI button, signal-to-attack mechanic |
| `obj_defenselines.scar` | objectives | Three defense lines (fords/hill/Don), holding/failing logic, fort construction, ally replenishment |
| `obj_mongolwaves.scar` | spawns | 10 wave sub-objectives, RovingArmy module generation, threat arrows, wave completion monitoring |
| `obj_preparearmy.scar` | objectives | Pre-battle objectives: visit villages, recruit allies, rally at fords, hidden village discovery |
| `training_kulikovo.scar` | training | Tutorial hints for cavalry signal button, hunting bounties, and blacksmith building |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Mission_SetupPlayers` | gdm_chp2_kulikovo | Configure 5 players, alliances, colours, LOS sharing |
| `Mission_SetupVariables` | gdm_chp2_kulikovo | Initialize SGroups, location constants, leader, objective inits |
| `Mission_SetRestrictions` | gdm_chp2_kulikovo | Disable popcap UI, set auto-upgrades, learn units |
| `Mission_Preset` | gdm_chp2_kulikovo | Complete starting upgrades, remove restricted upgrades, spawn intro |
| `Mission_Start` | gdm_chp2_kulikovo | Start OBJ_PrepareArmy, add hint points, begin meat collection |
| `GetRecipe` | gdm_chp2_kulikovo | Define recipe: audio, NIS, locations, ally RovingArmy modules |
| `Kulikovo_TransitionToEvening` | gdm_chp2_kulikovo | Transition game state to night over 120s |
| `Kulikovo_SpawnStartingUnits` | gdm_chp2_kulikovo | Deploy knights, infantry, scouts, escort, allied lane garrisons |
| `Kulikovo_SpawnRoutingUnits` | gdm_chp2_kulikovo | Clear all units, spawn corpse field and outro actors |
| `Kulikovo_MoveAll` | gdm_chp2_kulikovo | Move all 3 ally RovingArmy modules to named marker row |
| `Support_SpawnMainlineReinforcements` | gdm_chp2_kulikovo | Spawn pop-capped reinforcements for hill defense |
| `Support_SpawnLastlineReinforcements` | gdm_chp2_kulikovo | Spawn pop-capped reinforcements for Don defense |
| `Kulikovo_AddToSpawnTable` | gdm_chp2_kulikovo | Add units to spawn table if under 200 pop cap |
| `Kulikovo_CheckPlayerArmyDead` | gdm_chp2_kulikovo | Fail mission if all player squads dead |
| `Mongol_OnStart` | gdm_chp2_kulikovo | Start village raid spawn checks for villages 2 and 3 |
| `Mongol_SpawnVillageRaid` | gdm_chp2_kulikovo | Spawn Mongol raiders when player approaches village |
| `CollectMeat_Kulikovo` | gdm_chp2_kulikovo | Assign villagers to collect abandoned deer corpses |
| `MongolWaves_InitObjectives` | obj_mongolwaves | Register SOBJ_Wave1–10 with per-wave setup and handlers |
| `MongolWaves_SetupWave` | obj_mongolwaves | Play drum stingers, generate threat arrows, schedule lane spawns |
| `MongolWaves_SpawnWave` | obj_mongolwaves | Determine hidden spawn location, generate RovingArmy module per lane |
| `MongolWaves_GenerateModule` | obj_mongolwaves | Create RovingArmy with dynamically generated target list and focus modifier |
| `MongolWaves_CountAlive` | obj_mongolwaves | Complete wave objective when surviving enemies drop below threshold |
| `MongolWaves_GenerateThreatArrow` | obj_mongolwaves | Attach ThreatArrow to focused enemy squad or placeholder marker |
| `MongolWaves_GenerateMinimapBlip` | obj_mongolwaves | Create minimap threat blip at focused lane's current defense line |
| `MongolWaves_MonitorDefenselineStatus` | obj_mongolwaves | Check if defense line is held, start next wave if so |
| `MongolWaves_StartNextWave` | obj_mongolwaves | Stop current wave objective, start next wave objective |
| `MongolWaves_InitializeWaveStats` | obj_mongolwaves | Define focus lane, modifier, unit type per wave |
| `MongolWaves_UpdateModuleTargets` | obj_mongolwaves | Redirect all existing enemy modules to current defense line |
| `MongolWaves_TimedDelayCTA` | obj_mongolwaves | Show call-to-action alert with attack direction |
| `PrepareArmy_InitObjectives` | obj_preparearmy | Register OBJ_PrepareArmy and all sub-objectives |
| `PrepareArmy_CheckCaptured` | obj_preparearmy | Check if Dmitry is near village, convert villagers to player |
| `PrepareArmy_CheckNearArmy` | obj_preparearmy | Check if Dmitry reaches allied army, transfer to RovingArmy |
| `PrepareArmy_RevealFord` | obj_preparearmy | Reveal FOW at ford marker, add UI elements |
| `PrepareArmy_HillContext` | obj_preparearmy | Detect if player crossed hill/forest for VO trigger |
| `PrepareArmy_PlayerGoldPickup` | obj_preparearmy | Start optional village objective when gold collected (Easy/Normal) |
| `DefenseLines_InitObjectives` | obj_defenselines | Register OBJ_RepelMongols, SOBJ_HoldFords/Mainline/Last, ford strengths |
| `DefenseLines_IsMarkerLost` | obj_defenselines | Return true if only Mongols occupy marker; update progress bar |
| `DefenseLines_UpdateHoldStatus` | obj_defenselines | Set holdStatus true when progress bar full or timeout |
| `DefenseLines_ReinforceTimedBypass` | obj_defenselines | Set fallback timeout flag to prevent stalling |
| `DefenseLines_MainlineForts` | obj_defenselines | Spawn villagers to build 2 forts at hill positions |
| `DefenseLines_LastlineForts` | obj_defenselines | Spawn villagers to build 3 forts at Don positions |
| `DefenseLines_CheckConstructionComplete` | obj_defenselines | Monitor fort construction, garrison villagers when done |
| `DefenseLines_ReplenishModule` | obj_defenselines | Respawn ally lane units to full complement |
| `CavDetachment_InitObjectives` | obj_cavdetachment | Register OBJ_SignalCavalry objective |
| `CavDetachment_StartCavalry` | obj_cavdetachment | Begin spawning cavalry, show UI button |
| `CavDetachment_SpawnCavalryUnits` | obj_cavdetachment | Deploy knight batches to forest staging area |
| `CavDetachment_ConvertCavalryToPlayer` | obj_cavdetachment | Transfer cavalry ownership to player, attack-move to front |
| `CavDetachment_CavalryButtonClicked` | obj_cavdetachment | Handle UI button press, complete signal objective |
| `CavDetachment_ShowCavalryUI` | obj_cavdetachment | Create WPF XAML cavalry signal button with counter |
| `CavDetachment_ShowXboxCavalryUI` | obj_cavdetachment | Xbox-specific cavalry UI with controller binding |
| `CavDetachment_UpdateCavalryText` | obj_cavdetachment | Update button text with current/max cavalry count |
| `Kulikovo_InitializeCavalryTrainingHints` | training_kulikovo | Add training hint when cavalry reaches full strength |
| `MissionTutorial_AddHintToHuntingBounties` | training_kulikovo | Show hunting bounty hint when wolves on screen |
| `MissionTutorial_Blacksmith` | training_kulikovo | Show blacksmith selection training hint |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_PrepareArmy` | Primary | Prepare to fight the Mongol threat (parent for preparation phase) |
| `SOBJ_RecruitSoldiers` | Secondary | Regroup with allied Rus armies by bringing Dmitry to center camp |
| `SOBJ_VisitVillages` | Secondary | Visit 2 Rus villages with Dmitry to recruit soldiers |
| `SOBJ_RallyFords` | Secondary | Rally ≥10 player units at center ford; progress bar tracks count |
| `OBJ_HiddenVillage` | Primary (Secret) | Find hidden village for 18 bonus spearmen + blacksmith |
| `OBJ_OptionalFindVillage` | Optional | Find village to spend gold (Easy/Normal only) |
| `OBJ_RepelMongols` | Battle | Parent: Repel the Mongol Horde |
| `SOBJ_Wave1`–`SOBJ_Wave10` | Secondary | Individual wave sub-objectives under OBJ_RepelMongols |
| `SOBJ_HoldFords` | Battle | Defend Smolka River fords (waves 1–3); fails if any ford overrun |
| `SOBJ_HoldMainline` | Battle | Defend central hill (waves 4–7); fails if marker lost |
| `SOBJ_HoldLast` | Battle | Defend Don River crossing (waves 8–10); failure = mission fail |
| `OBJ_FordStrength_L/C/R` | Secret Battle | Per-ford strength progress bars |
| `OBJ_HoldDon` | Information | Informational: Mongols must not cross the Don River |
| `OBJ_SignalCavalry` | Primary | Signal hidden cavalry to attack (one-time use) |

### Difficulty

All 10 waves use `Util_DifVar({Easy, Normal, Hard, Expert})` per unit type:

| Parameter | What It Scales |
|-----------|---------------|
| Wave squad counts | Each unit type per wave has 4-value difficulty array |
| Unit tier upgrades | Hard/Expert substitute tier-2 with tier-3 units (spearman_3, horseman_3, knight_3, manatarms_3) |
| Siege additions | Springalds appear wave 6+ (all difficulties); Mangonels wave 7+ (Normal+) |
| Village raid composition | Easy/Normal: horseman_1 ×8; Hard: horseman_2 ×8 + horse_archer_2 ×6; Expert: knight_2 ×6 + horse_archer_2 ×9 |
| Wave 10 hybrid army | Scales from ~30 squads/lane (Easy) to ~42 squads/lane (Expert) with siege |
| Gold pickup hint | OBJ_OptionalFindVillage only starts on Easy/Normal |

### Spawns

**Pre-battle village raids**: Triggered when player approaches villages 2 and 3. Spawn Mongol raiders via RovingArmy with `onDeathDissolve = true`.

**10 Mongol waves** across 3 lanes (left/center/right):
- Waves alternate unit types: infantry (1,3,6,8,9), cavalry (2,4,5,7), hybrid (10)
- Each wave has a **focus lane** receiving 2–3× the base squad count
- Focus pattern: center→right→left→right→center→left→right→left→right→center
- Spawns use `Util_FindHiddenSpawn` to keep spawn points off-screen
- Each lane creates a `RovingArmy` module with targets at the current defense line
- Wave 10 absorbs the 3 static Mongol main armies into wave modules via `DissolveModuleIntoModule`

**Wave compositions** (per lane base, before focus multiplier):

| Wave | Type | Key Units (Expert) |
|------|------|--------------------|
| 1 | Infantry | Spearman×12, MaA×4, Archer×6 |
| 2 | Cavalry | Horseman×16, Knight×2, HorseArcher×8 |
| 3 | Infantry | Spearman×15, MaA×6, Archer×10 |
| 4 | Cavalry | Horseman×11, Knight×4, HorseArcher×12 |
| 5 | Cavalry | Horseman×16, Knight×4, HorseArcher×10 |
| 6 | Infantry | Spearman×18, MaA×8, Archer×8, Springald×1 |
| 7 | Cavalry | Horseman×22, Knight×8, HorseArcher×8, Mangonel×1 |
| 8 | Infantry | Spearman×14, MaA×6, Archer×10, Springald×1 |
| 9 | Infantry | Spearman×18, MaA×6, Archer×10, Springald×1 |
| 10 | Hybrid | All types ×42+, Springald×1, Mangonel×1 |

**Cavalry detachment**: 6 knights spawn initially, then 1 every 9s up to 40 max. Player signals via custom UI button to convert all to player-owned and attack-move to front line.

**Player reinforcements**: Spawn at village_03 when transitioning to hill (spearmen, MaA, crossbowmen, knights, monks ×8 each, pop-cap checked) and again for Don defense.

**Ally replenishment**: Each defense line transition respawns allied lane units (1 scout, 20 spearmen, 20 archers, 10 MaA per lane).

### AI

- **No AI_Enable calls** — enemies use scripted RovingArmy modules exclusively
- **3 static Mongol main armies**: MongolLeftArmy, MongolCenterArmy, MongolRightArmy — repositioned via `Prefab_DoAction("UpdateTargetLocation")` when defense lines change
- **Dynamic wave modules**: `MongolWaves_GenerateModule` creates per-wave per-lane RovingArmy instances with `onDeathDissolve = true`
- **Target generation**: `MongolWaves_GenerateRowOfTargets` builds ordered target lists prioritizing the module's lane, falling through to other lanes
- **FOW reveals**: Each defense line start reveals positions to player2 (Mongols) so AI engages correctly
- **Allied RovingArmy modules**: `ally_left`, `ally_center`, `ally_right` (player3) — repositioned per phase, replenished at each transition
- **Wave 10 retreat**: On PreComplete, all remaining Mongols receive `Cmd_FormationMove` to retreat toward spawn, RovingArmy modules disbanded

### Timers

| Timer/Rule | Delay/Interval | Purpose |
|------------|---------------|---------|
| `MongolWaves_SpawnWave` (OneShot) | 14s default, 6s focused lane | Delay wave spawn to match drum stinger timing |
| `MongolWaves_CountAlive` (Interval) | 14s delay, 1s interval | Monitor wave squads; complete objective when below threshold |
| `MongolWaves_MonitorDefenselineStatus` (Interval) | 19–37s delay, 1s interval | Check if defense held, start next wave (varies by wave) |
| `CavDetachment_SpawnCavalryUnits` (Interval) | 9s (`cav_spawn_rate`) | Spawn 1 knight every 9s to cavalry staging area |
| `CavDetachment_StartCavalry` (OneShot) | 8s after wave 4 completes | Begin cavalry accumulation |
| `ObjectiveStart_CavDetachment` (OneShot) | 14s after cavalry starts | Show OBJ_SignalCavalry objective |
| `DefenseLines_ReinforceTimedBypass` (OneShot) | 64s (mainline), 45s (lastline) | Prevent holding stall; force holdStatus update |
| `DefenseLines_UpdateHoldStatus` (Interval) | 1s | Check progress bar fill to set holdStatus true |
| `DefenseLines_MainlineCTA` (OneShot) | 56s | Show fort construction CTA for hill |
| `DefenseLines_LastLineCTA` (OneShot) | 62s | Show fort construction CTA for Don |
| `Kulikovo_TransitionToEvening` | 120s transition | Night state triggered at wave 2 start |
| Morning haze transition | 300s | Triggered on wave 9 completion |
| `CollectMeat_Kulikovo` (Interval) | 3s | Assign villagers to collect abandoned deer |
| `Cleanup_MeatCollectors` (Interval) | 5s | Despawn idle meat collector villagers |
| `Kulikovo_CheckPlayerArmyDead` (Interval) | 1s | Fail mission if player has no squads |
| `MongolWaves_TimedDelayCTA` (OneShot) | 15s | Show call-to-action with attack direction |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `gdm_chp2_kulikovo.scar` | `MissionOMatic/MissionOMatic.scar`, `obj_preparearmy.scar`, `obj_defenselines.scar`, `obj_mongolwaves.scar`, `obj_cavdetachment.scar`, `kulikovo_wavevariables.scar`, `training_kulikovo.scar` |
| `obj_mongolwaves.scar` | `gdm_chp2_kulikovo.scar` (circular reference for shared globals) |
| `obj_defenselines.scar` | `gdm_chp2_kulikovo.scar` (circular reference for shared globals) |
| `kulikovotraininggoals.scar` | `training/campaigntraininggoals.scar`, `training/rustrainingconditions.scar` |
| `training_kulikovo.scar` | `training/campaigntraininggoals.scar` |

### Shared Globals

- `player1`–`player5`: Player references used across all files
- `holdStatus[LOCATION_FORDS/MAINLINE/LASTLINE]`: Defense line state flags read by wave and defense systems
- `current_wave`: Current wave index, set in wave objectives, read by spawning/monitoring systems
- `mongol_waves[]`: Wave composition table (defined in wavevariables, consumed by mongolwaves)
- `wave_stats[]`: Per-wave metadata (defined in mongolwaves init, read by setup/spawn functions)
- `laning_starting_group`: Allied lane unit template (defined in core, used in defense replenishment)
- `cavalry_current`, `cavalry_maximum`: Cavalry accumulation state (cavdetachment ↔ training_kulikovo)
- `sg_ally_left/center/right`: Allied SGroups managed by defense lines and core
- `ally_left/center/right`: RovingArmy module references used by core and defense lines
- `sg_leaderDmitry`: Leader SGroup (MissionOMatic leader pattern)
- `mainline_built`, `lastline_built`: Fort construction counters (defense lines)
- `fallbackTimeouts[]`: Timed bypass flags per defense line

### Inter-File Function Calls

| Caller File | Called Function | Defined In |
|-------------|----------------|------------|
| gdm_chp2_kulikovo | `PrepareArmy_InitObjectives()` | obj_preparearmy |
| gdm_chp2_kulikovo | `DefenseLines_InitObjectives()` | obj_defenselines |
| gdm_chp2_kulikovo | `CavDetachment_InitObjectives()` | obj_cavdetachment |
| obj_defenselines | `MongolWaves_InitObjectives()` | obj_mongolwaves |
| obj_mongolwaves (SOBJ_Wave1) | `DefenseLines_MainlineForts()` | obj_defenselines |
| obj_mongolwaves (SOBJ_Wave4) | `CavDetachment_StartCavalry()` | obj_cavdetachment |
| obj_mongolwaves (SOBJ_Wave5) | `DefenseLines_LastlineForts()` | obj_defenselines |
| obj_mongolwaves | `MongolWaves_UpdateModuleTargets()` | obj_mongolwaves (self) |
| obj_defenselines | `MongolWaves_UpdateModuleTargets()` | obj_mongolwaves |
| obj_defenselines | `Support_SpawnMainlineReinforcements()` | gdm_chp2_kulikovo |
| obj_defenselines | `Support_SpawnLastlineReinforcements()` | gdm_chp2_kulikovo |
| obj_defenselines | `DefenseLines_ReplenishModule()` | obj_defenselines (self) |
| obj_cavdetachment | `Kulikovo_InitializeCavalryTrainingHints()` | training_kulikovo |
| obj_preparearmy | `MissionTutorial_Blacksmith()` | training_kulikovo |
| gdm_chp2_kulikovo | `MissionTutorial_AddHintToHuntingBounties()` | training_kulikovo |
| gdm_chp2_kulikovo | `Kulikovo_TransitionToEvening()` | gdm_chp2_kulikovo (called from SOBJ_Wave2) |

### MissionOMatic Integration

- Uses `MissionOMatic/MissionOMatic.scar` framework for recipe, modules, objectives, leader system
- Leader: Prince Dmitry initialized via `Missionomatic_InitializeLeader`
- Modules: 3 ally RovingArmy (persistent), 1 PlayerArmy UnitSpawner, dynamically created enemy RovingArmy per wave/lane
- Locations: 6 villages (player3), 3 townlife positions (player4)
- `Prefab_DoAction` used to control Mongol main army modules
- `MissionOMatic_FindModule` used to locate dynamic wave RovingArmy instances
