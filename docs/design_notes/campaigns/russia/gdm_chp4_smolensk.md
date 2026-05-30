# Russia Chapter 4: Smolensk

## OVERVIEW

This mission recreates the 1514 Moscow–Lithuania conflict over Smolensk, forming Mission 7 of "The Rise of Moscow" campaign. The player controls the Grand Duchy of Moscow (Rus civilization, Castle Age start) against Lithuanian defenders (HRE civilization, Imperial Age). The mission flows in two major phases: first, capture three surrounding villages (Roslavl, Yelnya, Vyazma) — each unlocking a specific military production building — then besiege Smolensk itself by intercepting supply caravans on two trade routes and breaching the city walls. A supply meter mechanic drives escalating attack waves from Smolensk whenever caravans reach the city, while an optional objective at neutral Krasny rewards the player with cannons and a university unlock.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp4_smolensk.scar` | core | Main mission script: player setup, recipe/modules, village attack spawns, outpost logic, utility functions, intro/outro cinematics |
| `obj_capturevillages.scar` | objectives | Phase 1 objectives: capture Roslavl/Yelnya/Vyazma villages, landmark protection, wall breach audio, villager conversion |
| `obj_besiegesmolensk.scar` | objectives | Phase 2 objectives: besiege walls, caravan interception, supply meter, Krasny optional, Smolensk capture, wave system |
| `obj_surrenderui.scar` | other | XAML-based surrender UI gizmo with Accept/Reject buttons (appears unused in final flow) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | gdm_chp4_smolensk | Configure 3 players, ages, relationships, colours |
| `Mission_SetupVariables` | gdm_chp4_smolensk | Init EGroups, SGroups, supply table, attack timings |
| `Mission_SetRestrictions` | gdm_chp4_smolensk | Lock production buildings, pop cap, outpost upgrades |
| `Mission_Preset` | gdm_chp4_smolensk | Register all objectives, set up waves, extra villagers |
| `Mission_Start` | gdm_chp4_smolensk | Start OBJ_CaptureVillages, outpost proximity rules, landmarks |
| `GetRecipe` | gdm_chp4_smolensk | Define MissionOMatic recipe: 7 locations, 20+ modules |
| `Smolensk_IsPlayerEconomyTrapped` | gdm_chp4_smolensk | Check if player has no units and low resources |
| `Smolensk_AddResources` | gdm_chp4_smolensk | Grant 500F/800W/500G/500S on village capture |
| `Smolensk_ProximitySpawner` | gdm_chp4_smolensk | Spawn defenders when player approaches a marker |
| `Smolensk_OverrideBuildTimes` | gdm_chp4_smolensk | Set all unit build times to 1 for waves |
| `Smolensk_OutpostCaptureCheck` | gdm_chp4_smolensk | Convert outpost ownership when defenders eliminated |
| `Smolensk_GetTimeScaledAmount` | gdm_chp4_smolensk | Return time-scaled value with polynomial growth |
| `Smolensk_CheckNearWestOutpost` | gdm_chp4_smolensk | Spawn west outpost defenders on proximity |
| `Smolensk_CheckNearEastOutpost` | gdm_chp4_smolensk | Spawn east outpost defenders on proximity |
| `Smolensk_CheckWestOutpostTrigger` | gdm_chp4_smolensk | Move cannons to firing positions at west outpost |
| `Smolensk_SendAttack` | gdm_chp4_smolensk | Create RovingArmy + Wave for village counter-attacks |
| `Smolensk_ProximityCallFunction` | gdm_chp4_smolensk | Call function when player reaches marker radius |
| `Smolensk_SpawnSmolenskVillagerLife` | gdm_chp4_smolensk | Spawn 23 villagers for Smolensk villager life |
| `Smolensk_SpawnKrasnyVillagerLife` | gdm_chp4_smolensk | Spawn 11 villagers for Krasny villager life |
| `Smolensk_IntroSpawner` | gdm_chp4_smolensk | Deploy intro cinematic parade units |
| `Smolensk_SkippedIntro` | gdm_chp4_smolensk | Place army at final positions if intro skipped |
| `Smolensk_OutroSpawner` | gdm_chp4_smolensk | Deploy outro parade units marching into Smolensk |
| `Smolensk_DelayedAudioStinger` | gdm_chp4_smolensk | Play triumphant stinger and walla celebrate |
| `CaptureVillages_Init` | obj_capturevillages | Register OBJ_CaptureVillages with wall breach events |
| `CaptureVillages_InitRoslavl` | obj_capturevillages | Register Roslavl sub-objectives, unlock cavalry building |
| `CaptureVillages_InitYelnya` | obj_capturevillages | Register Yelnya sub-objectives, unlock archery building |
| `CaptureVillages_InitVyazma` | obj_capturevillages | Register Vyazma sub-objectives, unlock infantry building |
| `CaptureVillages_InitLandmarks` | obj_capturevillages | Register OBJ_ProtectLandmarks fail condition |
| `CaptureVillages_OnComplete` | obj_capturevillages | Spawn villagers, add resources, start village raids |
| `CaptureVillages_ContinueObjectiveFlow` | obj_capturevillages | Flee enemy villagers toward Smolensk |
| `CaptureVillages_PlayIntel` | obj_capturevillages | Play sequential village capture VO |
| `CaptureVillages_TrackLandmarks` | obj_capturevillages | Start protect objective when landmark HP <= 60% |
| `CaptureVillages_WatchForPlayerLandmarks` | obj_capturevillages | Detect player-built Age 3 landmarks |
| `CaptureVillages_ReinforceVillages` | obj_capturevillages | Spawn reinforcements to uncaptured villages (disabled) |
| `CaptureVillages_Roslavl` | obj_capturevillages | Spawn cavalry raids from Roslavl to captured villages |
| `CaptureVillages_Yelnya` | obj_capturevillages | Spawn ranged raids from Yelnya to captured villages |
| `CaptureVillages_Vyazma` | obj_capturevillages | Spawn melee raids from Vyazma to captured villages |
| `CaptureVillages_Breach` | obj_capturevillages | Play audio stinger on village wall destruction |
| `CaptureVillages_OutpostBreach` | obj_capturevillages | Play audio stinger on outpost wall destruction |
| `ConvertVillagers_OnCapture` | obj_capturevillages | Convert villager life to player-owned gatherers |
| `BesiegeSmolensk_InitObjectives` | obj_besiegesmolensk | Register siege phase and caravan objectives |
| `BesiegeSmolensk_InitKrasny` | obj_besiegesmolensk | Register optional Krasny cannon objective |
| `BesiegeSmolensk_SpawnWallDefenders` | obj_besiegesmolensk | Spawn crossbow/handcannon on 4 wall sections |
| `BesiegeSmolensk_DelayKrasnyStart` | obj_besiegesmolensk | Delayed start for Krasny objective |
| `BesiegeSmolensk_CheckNearbyKrasny` | obj_besiegesmolensk | Trigger Krasny VO and objective on proximity |
| `BesiegeSmolensk_EntityKilled` | obj_besiegesmolensk | Detect Smolensk wall/gate destruction for breach |
| `BesiegeSmolensk_DelayedObjectiveCall` | obj_besiegesmolensk | Complete OBJ_BesiegeSmolensk after 3s delay |
| `BesiegeSmolensk_UpdateSupplyUI` | obj_besiegesmolensk | Update supply progress bar each 0.5s |
| `BesiegeSmolensk_SpawnCaravan` | obj_besiegesmolensk | Spawn trade carts with escort on both routes |
| `Caravan_ReachedDestination` | obj_besiegesmolensk | Increase supply, trigger waves when supply full |
| `BesiegeSmolensk_TrackCaravanDeath` | obj_besiegesmolensk | Track killed caravans, close routes at death limit |
| `BesiegeSmolensk_SpawnWaveAttack` | obj_besiegesmolensk | Spawn time-scaled attack wave from Smolensk |
| `BesiegeSmolensk_SetUpWaves` | obj_besiegesmolensk | Create 3 RovingArmy wave pipelines (left/center/right) |
| `BesiegeSmolensk_TimeScaleUnitTable` | obj_besiegesmolensk | Scale unit counts up to 3x via time function |
| `BesiegeSmolensk_PathReveal` | obj_besiegesmolensk | Sequentially reveal FOW along caravan markers |
| `BesiegeSmolensk_RevealTraderPath` | obj_besiegesmolensk | Reveal all caravan path markers at once |
| `SurrenderUI_CreateGizmo` | obj_surrenderui | Create XAML surrender prompt with two buttons |
| `SurrenderUI_AcceptSurrender` | obj_surrenderui | Accept surrender, start OBJ_EnterSmolensk |
| `SurrenderUI_RefuseSurrender` | obj_surrenderui | Reject surrender, start OBJ_CaptureSmolensk |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_CaptureVillages` | Primary | Phase 1: Capture all three surrounding villages |
| `SOBJ_CaptureRoslavl` | Sub (Capture) | Capture Roslavl — unlocks cavalry production |
| `SOBJ_DefeatRoslavlResistance` | Sub (Battle) | Defeat Roslavl garrison |
| `SOBJ_LocationRoslavl` | Sub (Capture) | Roslavl location marker |
| `SOBJ_CaptureYelnya` | Sub (Capture) | Capture Yelnya — unlocks archery production |
| `SOBJ_DefeatYelnyaResistance` | Sub (Battle) | Defeat Yelnya garrison |
| `SOBJ_LocationYelnya` | Sub (Capture) | Yelnya location marker |
| `SOBJ_CaptureVyazma` | Sub (Capture) | Capture Vyazma — unlocks infantry production |
| `SOBJ_DefeatVyazmaResistance` | Sub (Battle) | Defeat Vyazma garrison |
| `SOBJ_LocationVyazma` | Sub (Capture) | Vyazma location marker |
| `OBJ_ProtectLandmarks` | Information | Fail if all player-owned landmarks destroyed |
| `OBJ_BesiegeSmolensk` | Primary | Phase 2: Breach Smolensk's walls |
| `OBJ_StopAttacks` | Primary | Cut off supplies — stop Smolensk attacks |
| `SOBJ_StopTraders` | Sub (Battle) | Intercept traders from both caravan routes |
| `OBJ_SmolenskSupply` | Information | Supply progress bar for next Smolensk attack |
| `OBJ_ForceSurrender` | Primary | Phase 3: Capture Smolensk after wall breach |
| `SOBJ_DefeatSmolenskResistance` | Sub (Battle) | Defeat Smolensk's interior garrison |
| `SOBJ_LocationSmolensk` | Sub (Capture) | Smolensk location marker |
| `OBJ_CaptureKrasny` | Optional | Visit Krasny to receive 4 cannons |
| `OBJ_DebugComplete` | Debug | Instant mission complete cheat |

### Difficulty

| Parameter | Values (Easy/Normal/Hard/Expert) | What It Scales |
|-----------|----------------------------------|----------------|
| Roslavl defenders (horseman) | 6 / 8 / 8 / 10 | Horseman squads at Roslavl |
| Roslavl defenders (knight) | 4 / 6 / 6 / 14 | Knight squads at Roslavl |
| Yelnya defenders (archer) | 8 / 10 / 10 / 6 | Archer squads at Yelnya |
| Yelnya defenders (crossbow) | 2×2 / 2×3 / 2×4 / 2×6 | Crossbow squads (two spawn points) |
| Yelnya defenders (handcannon) | 2×1 / 2×1 / 2×2 / 2×4 | Handcannon squads (two spawn points) |
| Vyazma defenders (spearman) | 2×4 / 2×5 / 2×5 / 2×8 | Spearman squads (two spawn points) |
| Vyazma defenders (MAA) | 4 / 6 / 6 / 12 | Men-at-arms squads at Vyazma |
| West outpost (spearman) | 2×2 / 2×4 / 2×4 / 2×8 | Spearman squads (two flanks) |
| West outpost (MAA) | 2×2 / 2×4 / 2×4 / 2×6 | MAA squads (two flanks) |
| East outpost (spearman) | 6 / 8 / 8 / 12 | Spearman squads |
| East outpost (MAA) | 4 / 6 / 6 / 8 | MAA squads |
| East outpost (archer) | 6 / 8 / 8 / 12 | Archer squads |
| East outpost (crossbow) | 4 / 6 / 6 / 8 | Crossbow squads |
| Tower upgrades | Springald / Springald / Cannon / Cannon | Smolensk tower weapon type |
| Wall defenders (crossbow) | 8 / 8 / 10 / 10 | Crossbow per wall section |
| Wall defenders (handcannon) | 4 / 4 / 6 / 8 | Handcannon per wall section |
| Smolensk melee (spearman) | 4 / 4 / 6 / 8 | Interior spearman squads |
| Smolensk melee (MAA) | 2 / 4 / 6 / 8 | Interior MAA squads |
| Smolensk ranged (crossbow) | 2×5 / 2×6 / 2×8 / 2×12 | Interior crossbow (two groups) |
| Smolensk ranged (handcannon) | 2×3 / 2×4 / 2×8 / 2×12 | Interior handcannon (two groups) |
| Smolensk cavalry (horseman) | 6 / 8 / 8 / 16 | Interior horseman squads |
| Smolensk siege (cannon) | 1 / 2 / 4 / 4 | Interior cannon squads |
| Smolensk wave attacks | 1 route (E/N) / 2 routes (H) / 3 routes (X) | Number of simultaneous attack routes |
| Extra starting villagers | +4 (Easy) / +0 (Normal+) | Bonus villagers on Story difficulty |
| Village raid compositions | Scaled per type | Horsemen/knights, archers/crossbow, spearmen/MAA |

### Spawns

**Starting Forces (Player — Intro Parade):**
- Scouts: 2 scouts
- Cavalry: 8 knights (4 groups of 2)
- Infantry: 12 spearmen, 12 men-at-arms, 24 crossbowmen (in 4 groups of 6)

**Village Defenders (Lithuanian, pre-placed + proximity-spawned):**
- Roslavl (Cavalry): 6-10 horsemen + 4-14 knights
- Yelnya (Ranged): 8-6 archers + 4-12 crossbowmen + 2-8 handcannoneers
- Vyazma (Melee): 8-16 spearmen + 4-12 men-at-arms

**Village Counter-Attack Raids (from uncaptured villages to captured ones):**
- Roslavl: 8 horsemen OR 6-8 knights (random), 240-480s delay
- Yelnya: 1-2 scouts + 6-8 archers OR 4-6 crossbow + 4-6 handcannon, 300-500s delay
- Vyazma: 4-6 spearmen + 2-4 landsknechts OR 4-6 MAA + 2-4 landsknechts, 360-500s delay
- Raids route through captured villages via `mkr_village_attack_routing`

**Outpost Defenders (proximity-triggered):**
- West outpost: outer guards (4-16 spearmen + 4-12 MAA), inner (8 spearmen + 8 MAA), gate (12 spearmen), 2 cannon groups with escort
- East outpost: 6-12 spearmen + 4-8 MAA + 6-12 archers + 4-8 crossbowmen

**Smolensk Wall Defenders (spawned at OBJ_BesiegeSmolensk start):**
- 4 wall sections: each gets 4 archers (Easy/Normal only) + 8-10 crossbowmen + 4-8 handcannoneers

**Smolensk Interior (spawned at OBJ_ForceSurrender):**
- Melee: 4-8 spearmen + 2-8 MAA
- Ranged: 2× (5-12 crossbow + 3-12 handcannon)
- Cavalry: 6-16 horsemen
- Siege: 1-4 cannons + 3 counterweight trebuchets
- Wall defenders dissolved into city defense modules

**Caravan System (during OBJ_StopAttacks):**
- Spawned every 48s on both west and east routes
- Base: 1 trade cart + 2 spearmen escort
- After 2 kills: +6 spearmen
- After 6 kills: +8 landsknechts
- After 8 kills: +4 crossbowmen
- Death limit: 5 per route (10 total to complete objective)

**Smolensk Attack Waves (triggered when supply reaches max):**
- Base composition: 4 spearmen + 4 MAA + 6 archers + 2 crossbowmen (difficulty-scaled)
- Time scaling: unit counts grow up to 3x via polynomial `Smolensk_GetTimeScaledAmount`
- First wave is lighter (2 spearmen + 2 archers)
- Easy/Normal: 1 random route; Hard: 2 random routes; Expert: all 3 routes
- Routes: left (gate left → Roslavl), center (gate right → Yelnya), right (gate right → Vyazma)

**Krasny (Optional):**
- 4 Rus cannons spawned on completion + university unlocked + pop cap +20
- Neutral villager life: 4 roaming + 7 food villagers (player3-owned, converted on capture)

### AI

- No explicit `AI_Enable` calls; AI is managed through MissionOMatic Defend modules
- Player2 (Lithuanians) given 30,000 wood + 1,000 each of other resources for ram construction
- `PlayerUpgrades_Auto` applied to all 3 players (player1 with `true` flag)
- Player2 has Siege Engineers upgrade pre-completed
- All outposts upgraded to arrowslits; armed outposts upgraded to stone + springald
- Smolensk towers upgraded to springald (Normal-) or cannon (Hard+)
- Village defenders use static Defend modules (no reinforcement system — commented out)
- Smolensk defenders use segmented Defend modules: 4 wall positions, melee/ranged/cavalry/siege/wall interior groups, 3 trebuchet positions
- Wall defenders dissolve into `smolensk_wall` module when city capture phase begins

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `Rule_AddInterval(Smolensk_CheckNearWestOutpost, 1)` | 1s | Spawn west outpost defenders on proximity |
| `Rule_AddInterval(Smolensk_CheckNearEastOutpost, 1)` | 1s | Spawn east outpost defenders on proximity |
| `Rule_AddInterval(Smolensk_OutpostCaptureCheck, 1)` | 1s | Check if outpost defenders dead, convert to player |
| `Rule_AddInterval(CaptureVillages_TrackLandmarks, 1)` | 1s | Monitor landmark HP for protect objective |
| `Rule_AddInterval(CaptureVillages_WatchForPlayerLandmarks, 1)` | 1s | Detect player-built Age 3 landmarks |
| `Rule_AddInterval(BesiegeSmolensk_CheckNearbyKrasny, 1)` | 1s | Check proximity to Krasny VO markers |
| `Rule_AddInterval(Smolensk_ProximityCallFunction, 1)` | 1s | Generic proximity → function caller (Krasny, Smolensk villager life) |
| `Rule_AddInterval(Smolensk_CheckWestOutpostTrigger, 1)` | 1s | Move cannons when player reaches trigger |
| `Rule_AddInterval(BesiegeSmolensk_UpdateSupplyUI, 0.5)` | 0.5s | Update supply progress bar |
| `Rule_AddInterval(BesiegeSmolensk_SpawnCaravan, 48)` | 48s | Spawn caravan convoys on both routes |
| `Rule_AddInterval(BesiegeSmolensk_PathReveal, 0.125)` | 0.125s | Sequentially reveal FOW along caravan paths |
| `Rule_AddOneShot(CaptureVillages_Roslavl, 240-480)` | Random | First cavalry raid from Roslavl |
| `Rule_AddOneShot(CaptureVillages_Yelnya, 300-500)` | Random | First ranged raid from Yelnya |
| `Rule_AddOneShot(CaptureVillages_Vyazma, 360-500)` | Random | First melee raid from Vyazma |
| `Rule_AddOneShot(BesiegeSmolensk_DelayKrasnyStart, 30)` | 30s | Delayed start for Krasny optional objective |
| `Rule_AddOneShot(BesiegeSmolensk_DelayedObjectiveCall, 3)` | 3s | Complete wall breach objective after delay |
| `Rule_AddOneShot(Smolensk_DelayedAudioStinger, 1)` | 1s | Play breach celebration audio |
| `Game_TransitionToState("taiga_sunset", 600)` | 600s | Transition lighting to sunset after 10 minutes |

### Supply Meter System

The `smolensk_supply` table drives Smolensk's attack waves during the siege phase:
- `current`: starts at 600 (out of `max` 1000)
- Each successful caravan arrival adds `increase` (100) to current supply
- When `current >= max`: resets to 0, launches prepared waves, prepares new wave set
- First wave uses reduced composition (2 spearmen + 2 archers)
- Difficulty determines how many of 3 routes launch simultaneously
- Unit counts scale over time via `Smolensk_GetTimeScaledAmount` (polynomial: `min + 0.25*(t/60) + 10⁻⁹*(t/60)⁶`)
- Killing 5 trade carts on each route (10 total) completes the caravan objective

### Village Capture Progression

Each village captured provides:
- Bonus resources: 500 food, 800 wood, 500 gold, 500 stone
- Villagers converted from enemy villager life to player gatherers (9 on first, 3 on subsequent)
- Pop cap increase: +20 per village (first village also re-enables pop cap display)
- Military building unlock: Roslavl → cavalry, Yelnya → archery, Vyazma → infantry
- Landmark invulnerability removed (was at 5% min cap, set to 0)
- Remaining uncaptured villages begin sending periodic counter-attack raids

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (includes Cardinal scripts)
- `obj_capturevillages.scar` — village capture objectives and counter-attack raids
- `obj_besiegesmolensk.scar` — siege phase, caravan system, Krasny optional, Smolensk capture
- `obj_surrenderui.scar` — XAML surrender UI (Accept/Reject buttons)

### Shared Globals
- `player1` / `player2` / `player3` — Moscow / Lithuanians / Neutrals
- `difficulty` — cached `Game_GetSPDifficulty()` for branching
- `villages_captured` — counter (0-3) tracking capture progress
- `villagesAttacking` — flag to start village raid timers only once
- `village_attack_timings` — table with min/max delays per village type
- `smolensk_supply` — table with current/max/increase/kill counts for supply meter
- `attack_wave` — incrementing counter for unique RovingArmy descriptors
- `starting_time` — baseline for `Smolensk_GetTimeScaledAmount` polynomial
- `first_wave` / `first_caravan_death` — one-time VO trigger flags
- `roslavl_wave` / `yelnya_wave` / `vyazma_wave` — Wave objects for Smolensk attacks
- `west_path_active` / `east_path_active` — caravan route UI state
- `b_roslavl_breached` / `b_yelnya_breached` / `b_vyazma_breached` — wall breach audio flags
- `b_west_outpost_breached` / `b_east_outpost_breached` — outpost breach audio flags
- `last_village_vo` — name of third captured village for completion VO selection
- `eg_player_landmarks` / `eg_player_built_landmark` — tracked player landmarks

### Inter-File Function Calls
- `gdm_chp4_smolensk.scar` calls `CaptureVillages_Init()`, `CaptureVillages_InitRoslavl/Yelnya/Vyazma()`, `CaptureVillages_InitLandmarks()`, `BesiegeSmolensk_InitObjectives()`, `BesiegeSmolensk_InitKrasny()`, `BesiegeSmolensk_SetUpWaves()`, `BesiegeSmolensk_CheckNearbyKrasny()`
- `obj_capturevillages.scar` calls `Smolensk_SendAttack()`, `Smolensk_DelayedAudioStinger()`, `Smolensk_AddResources()`, `ConvertVillagers_OnCapture()`, `BesiegeSmolensk_CheckNearbyKrasny()`
- `obj_besiegesmolensk.scar` calls `Smolensk_GetTimeScaledAmount()`, `Smolensk_SpawnSmolenskVillagerLife()`, `Smolensk_IsPlayerEconomyTrapped()`, `Smolensk_DelayedAudioStinger()`, `Mission_Complete()`, `Mission_Fail()`
- `obj_capturevillages.scar` references `OBJ_BesiegeSmolensk` (starts siege phase on village completion)
- `obj_besiegesmolensk.scar` references `OBJ_CaptureKrasny`, `OBJ_StopAttacks`, `OBJ_ForceSurrender` across objective chain
- `obj_surrenderui.scar` references `OBJ_EnterSmolensk` and `OBJ_CaptureSmolensk` (defined externally, possibly cut content)

### MissionOMatic Modules Used
- **Defend (Villages)**: roslavl_defend, yelnya_defend, vyazma_defend — cavalry/ranged/melee garrisons with `Util_DifVar` scaling
- **Defend (Outposts)**: west_outpost_defend, west_outpost_inner_defend, west_outpost_gate_defend, east_outpost_defend
- **Defend (Smolensk Walls)**: smolensk_defend_e_1, smolensk_defend_e_2, smolensk_defend_w_1, smolensk_defend_w_2
- **Defend (Smolensk Interior)**: smolensk_defend, smolensk_melee, smolensk_ranged_1, smolensk_ranged_2, smolensk_cavalry, smolensk_siege, smolensk_wall, smolensk_trebuchet_1/2/3
- **Defend (Staging)**: gather_left, gather_center, gather_right, gather_smolensk_left/center/right
- **RovingArmy**: roving_attack_N (dynamic village raids), smolensk_left/center/right_wave_assault (Smolensk attack waves with ARMY_TARGETING_DISCARD/CYCLE)
- **Wave**: smolensk_left/center/right_wave (with staging modules and auto_launch), wave_N (dynamic village counter-attacks)

### Recipe Metadata
- Campaign: `gdm`, Mission: `rts1514smolensk`
- Title Card: `$11160678` (title), `$11160679` (date)
- Icon: `icons/campaign/campaign_moscow_empire_to_superpower`
- Intro NIS: `EVENTS.Intro`, Outro NIS: `EVENTS.Victory`
- 7 locations: roslavl, yelnya, vyazma, krasny, smolensk, west_outpost, east_outpost
- Smolensk location has `blockCivConversionOnCapture = true`
