# Gameplay: Game Modes

## OVERVIEW

The Game Modes system defines the complete set of multiplayer and custom match types available in Age of Empires IV. Each mode is a single self-contained SCAR file that registers itself as a `Core_RegisterModule`, imports shared subsystems (win conditions, start conditions, diplomacy, score, UI), and layers mode-specific mechanics on top. All modes share a common `_match` global table pattern for options, speed modifiers, and debug flags. The architecture follows a lifecycle callback convention (`OnGameSetup` → `PreInit` → `OnInit` → `Start` → `OnPlayerDefeated` → `OnGameOver`) driven by the core scripting framework. Modes range from the baseline **Standard Mode** (pure win-condition selection) to highly specialized event modes like **Chaotic Climate** (seasonal buffs/atmosphere), **Full Moon** (werewolf waves), **Map Monsters** (land/sea boss spawns), **King of the Hill** (capture point with reward ticks), **Chart A Course** (tiered upgrade selection), **Combat Mode** (round-based buy/fight), **Season's Feast** (gift haul pickups), **Sandbox** (no win conditions), and **None** (campaign shell).

## FILE ROLES

| File | Role | Purpose |
|---|---|---|
| `standard_mode.scar` | core | Baseline multiplayer mode; configures win conditions, speed, diplomacy, debug options |
| `chaotic_climate_mode.scar` | core | Seasonal atmosphere cycling with random upgrade buffs applied to all players |
| `chart_a_course.scar` | core | Periodic tiered upgrade selection UI where players choose from buff candidates |
| `combat_mode.scar` | core | Round-based arena: buy period → fight → capture outpost → best-of-N rounds |
| `full_moon_mode.scar` | core | Periodic werewolf wave spawns with escalating count and moon rush mechanic |
| `king_of_the_hill_mode.scar` | core | Spawns a central capture point granting timed rewards to the controlling player |
| `map_monsters_mode.scar` | core | Spawns neutral land/sea monsters at equidistant map positions on interval |
| `seasons_feast_mode.scar` | core | Spawns collectible gift haul pickups across the map at regular intervals |
| `none_mode.scar` | other | Minimal mode with no win conditions, used as campaign shell |
| `sandbox_mode.scar` | other | No win conditions; exposed for player experimentation and modding |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|---|---|---|
| `StandardMode_OnGameSetup` | standard_mode | Parse options, register/unregister win condition modules |
| `StandardMode_OnInit` | standard_mode | Apply debug options, speed modifiers, remove units/gaia |
| `StandardMode_SetSpeed` | standard_mode | Apply gather/build/production speed modifiers to all players |
| `StandardMode_OnConstructionComplete` | standard_mode | Accelerate production on newly constructed buildings |
| `ChaoticClimate_OnGameSetup` | chaotic_climate_mode | Parse options, set season duration from match settings |
| `ChaoticClimate_OnInit` | chaotic_climate_mode | Initialize atmosphere, speed, debug options |
| `ChaoticClimate_Start` | chaotic_climate_mode | Schedule first season, create UI widget, FOW |
| `ChaoticClimate_StartPositiveSummer` | chaotic_climate_mode | Select initial buff, grant to all, start timer |
| `ChaoticClimate_EndSeason` | chaotic_climate_mode | Remove active buff, schedule next season |
| `ChaoticClimate_StartNextSeason` | chaotic_climate_mode | Select seasonal buff, apply, transition atmosphere |
| `SelectCurrentSeasonBuff` | chaotic_climate_mode | Weighted-random buff selection per season index |
| `ChaoticClimate_SpawnGaia` | chaotic_climate_mode | Spawn sheep/deer/boar at cached positions (forage) |
| `ChaoticClimate_KillGaia` | chaotic_climate_mode | Kill percentage of gaia animals (heat stress) |
| `ChaoticClimate_UpdateUI` | chaotic_climate_mode | Update season progress bar data context |
| `ChaoticClimate_CreateWidget` | chaotic_climate_mode | Build XAML circular-progress season HUD (PC/Xbox/Caster) |
| `LoadAtmospheres` | chaotic_climate_mode | Pre-load four seasonal atmosphere settings |
| `ChartACourse_OnInit` | chart_a_course | Initialize simulation, register network events, cheats |
| `ChartACourse_Start` | chart_a_course | Schedule first upgrade selection, set FOW |
| `ChartACourse_PrepareUpgradeCandidatesForPlayers` | chart_a_course | Generate upgrade choices, auto-select for AI |
| `ChartACourse_SelectUpgradeNtw` | chart_a_course | Network callback to grant selected upgrade |
| `ChartACourse_DetermineUpgradeTier` | chart_a_course | Set tier (fixed/random/ramp) from options |
| `ChartACourse_AutoSelectForLocalPlayer` | chart_a_course | Auto-pick random upgrade if player hasn't chosen |
| `ChartACourse_UpdateUI` | chart_a_course | Show/hide buff selection UI based on state |
| `ChartACourse_CreateBuffSelectionUIForPC` | chart_a_course | Build XAML 3-choice upgrade selection panel (PC) |
| `ChartACourse_CreateBuffSelectionUIForXbox` | chart_a_course | Build XAML 3-choice upgrade selection panel (Xbox) |
| `ChartACourse_OnGameRestore` | chart_a_course | Re-initialize simulation after save/load |
| `CombatMode_OnInit` | combat_mode | Configure starting age, resources, team LOS |
| `CombatMode_PostInit` | combat_mode | Apply age upgrades, spawn production buildings |
| `CombatMode_Start` | combat_mode | Remove resources, set popcap, begin first buy period |
| `CombatMode_BuyPeriod` | combat_mode | Grant resources, spawn outpost, start buy timer |
| `CombatMode_StartRound` | combat_mode | Add round objective, enable capture checking |
| `CombatMode_CheckObjective` | combat_mode | Monitor outpost capture and team elimination |
| `CombatMode_RoundTimer` | combat_mode | Countdown to round end after outpost captured |
| `CombatMode_EndRound` | combat_mode | Award round win, show stats, check victory |
| `CombatMode_Surrender` | combat_mode | Network event: kill player's squads, disable production |
| `CombatMode_EnableProduction` | combat_mode | Toggle production queues for a player's buildings |
| `CombatMode_ShowEndOfRoundUI` | combat_mode | Display round stats XAML overlay |
| `CombatMode_WinnerPresentation` | combat_mode | Trigger victory stinger and game-over message |
| `FullMoon_OnGameSetup` | full_moon_mode | Parse werewolf intensity, moon surge interval |
| `FullMoon_OnInit` | full_moon_mode | Load atmosphere, apply speed/debug settings |
| `FullMoon_Start` | full_moon_mode | Find spawn points, remove wolves, schedule waves |
| `FullMoon_FindSpawnPoints` | full_moon_mode | Gather per-player spawn locations via DynamicSpawning |
| `FullMoon_SpawnWave` | full_moon_mode | Spawn werewolves per player, escalate wave size |
| `FullMoon_SpawnBackUpWaveForPlayer` | full_moon_mode | Fallback spawn using nearest other player's points |
| `OneShot_EndCurrentMoonRush` | full_moon_mode | Deactivate moon_rush_signal, restore atmosphere |
| `KingOfTheHill_OnGameSetup` | king_of_the_hill_mode | Parse options, bonus starting resources (+500 each) |
| `KingOfTheHill_OnInit` | king_of_the_hill_mode | Find spawn points, spawn initial hill entity |
| `KingOfTheHill_SpawnHill` | king_of_the_hill_mode | Create capture_point entity at closest-to-center pos |
| `KingOfTheHill_OnCapturePointChange` | king_of_the_hill_mode | Handle capture/neutralize/contest state machine |
| `KingOfTheHill_RewardPoints` | king_of_the_hill_mode | Increment capture_point_reward_points statemodel |
| `KingOfTheHill_FindSpawnPoints` | king_of_the_hill_mode | Sort spawn positions by distance to map center |
| `MapMonsters_OnGameSetup` | map_monsters_mode | Parse monster spawn interval, clamp to min/max |
| `MapMonsters_OnInit` | map_monsters_mode | Apply speed/debug, setup spawn system |
| `MapMonsters_Start` | map_monsters_mode | Find spawn points, schedule monster spawn interval |
| `MapMonsters_TryFindSpawnPoints` | map_monsters_mode | Gather land/water markers with fallback to old system |
| `MapMonsters_FindSpawnPointsUsingOldSystem` | map_monsters_mode | Grid-sample map for equidistant spawn positions |
| `MapMonsters_SpawnMonster` | map_monsters_mode | Alternating land/sea monster spawn with event cue |
| `MapMonsters_SpawnMarkerFilter` | map_monsters_mode | Filter markers by player distance and fairness |
| `SeasonsFeast_OnInit` | seasons_feast_mode | Setup gift spawn system, register training hints |
| `SeasonsFeast_Start` | seasons_feast_mode | Calculate gift count, find spawn points, schedule |
| `SeasonsFeast_SpawnGifts` | seasons_feast_mode | Spawn gift_haul entities at random valid positions |
| `SeasonsFeast_FindSpawnPoints` | seasons_feast_mode | Gather spawn positions via DynamicSpawning or animals |
| `None_OnInit` | none_mode | Optionally remove initial units/buildings |
| `Sandbox_OnInit` | sandbox_mode | No win conditions, optional unit removal |

## KEY SYSTEMS

### Shared Architecture

All game modes follow an identical structural pattern:

- **Module Registration**: `Core_RegisterModule("ModuleName")` — enables lifecycle callbacks prefixed with the module name
- **Lifecycle Callbacks**: `_OnGameSetup` → `_PreInit` → `_OnInit` → `_Start` → `_OnPlayerDefeated` → `_OnGameOver`
- **Global Table**: `_match` stores options, speed modifiers, cheat flags, and mode-specific data
- **Win Condition Toggling**: Each mode reads `section_inner_win_conditions` options and calls `Core_UnregisterModule()` for disabled conditions (Conquest, Religious, Wonder, Regicide)
- **Speed System**: Every mode implements `{Module}_SetSpeed(speed)` applying `Modifier_Create(MAT_EntityType, ...)` for gather rates, build rate, production speed, and upgrade cost_ticks
- **Debug Options**: Shared `section_debug_options` keys: `option_high_resources`, `option_high_popcap`, `option_reveal_map`, `option_instant_build`
- **Command-Line Flags**: `cheat`, `no_fow`, `no_units`, `no_gaia`, `speed`, `build_speed`, `gather_speed`, etc.

### Common Imports

All event modes import the same subsystem stack:

| Import | Purpose |
|---|---|
| `cardinal.scar` | SFX references, UI templates, Civ/Age helpers |
| `ScarUtil.scar` | Game helper functions |
| `gameplay/score.scar` | Player score tracking |
| `gameplay/diplomacy.scar` | Tribute management |
| `gameplay/vision.scar` | Shared vision options |
| `gameplay/cheat.scar` | Cheat command support |
| `startconditions/classic_start.scar` | Standard start setup |
| `winconditions/annihilation.scar` | Elimination when unable to fight |
| `winconditions/elimination.scar` | Player quit/disconnect |
| `winconditions/surrender.scar` | Player surrender |
| `winconditions/regicide.scar` | King unit loss condition |
| `winconditions/conquest.scar` | Landmark destruction condition |
| `winconditions/wonder.scar` | Wonder victory condition |
| `winconditions/religious.scar` | Sacred site victory condition |
| `gameplay/event_cues.scar` | Event notification system |
| `gameplay/currentageui.scar` | Age display UI |
| `gameplay/chi/current_dynasty_ui.scar` | Chinese Dynasty UI |
| `gameplay/templar/templar_age_up_ui.scar` | Templar faction age UI |
| `training/*traininggoals.scar` | Per-civ training hint goals |
| `replay/replaystatviewer.scar` | Replay stat tabs |
| `gameplay/dynamic_spawning.scar` | Dynamic spawn marker system (event modes) |

### Mode-Specific Mechanics

#### Standard Mode
- Pure multiplayer baseline; no unique mechanics
- Configures win conditions, speed, diplomacy, FOW, nomad start
- Delegates all game logic to imported win condition modules

#### Chaotic Climate (Winds of Change)
- **Seasons**: Summer → Autumn → Winter → Spring cycle (index 0–3)
- **Timing**: `season_duration_time` (default 1 min), `season_cooldown_time` (1 min), `initial_delay_time` (30s)
- **Buffs**: All players receive a random upgrade via `Player_CompleteUpgrade`, removed at season end via `Player_RemoveUpgrade`
- **Season Buffs** (weighted 70% season-specific, 30% all-season):
  - All-season: CALMING_BREEZE, CLEAR_SKIES, DELUGE, EARTHQUAKE, FIERCE_GALES
  - Summer: PRODUCTIVE_ATMOSPHERE, HEAT_STRESS, INTENSE_HEAT, POTENTIAL_ENERGY, WARM_GLOW
  - Autumn: PRODUCTIVE_ATMOSPHERE, ABUNDANT_KINDLING, FORAGE_SEASON, PILFERED_FIELDS, SHORTER_DAYS
  - Winter: PRODUCTIVE_ATMOSPHERE, COLD_STEEL, FROSTED_BLANKET, SNOW_STORM, WARM_PELTS
  - Spring: PRODUCTIVE_ATMOSPHERE, DAYLIGHT_SAVINGS, NEW_BEGINNINGS, POLLEN_CLOUDS, SWARM_OF_INSECTS
- **Special Effects**: FORAGE_SEASON spawns gaia animals (40% of initial count); HEAT_STRESS kills 50% of gaia
- **Atmosphere**: Transitions via `Game_TransitionToState()` with named atmosphere presets
- **UI**: XAML circular progress bar widget (PC, Xbox, Caster variants)

#### Chart A Course
- **Upgrade Selection**: Players choose 1 of 3 upgrade candidates at periodic intervals
- **Timing**: `initial_selection_time` (30s), `upgrade_selection_interval` (1 min configurable), up to 3 rounds
- **Tier System**: Tier 0/1/2 (fixed, random, or ramp via `option_buff_tier_setting`)
- **Auto-Select**: 10s before next round, unchosen upgrades are auto-selected randomly
- **AI Handling**: AI players get random selections via `Game_ChartACourseGetRandomBuffSelectionIndexForLocalPlayer`
- **Network Sync**: `Network_RegisterEvent("ChartACourse_SelectUpgradeNtw")` for cross-client sync
- **Engine API**: `Game_ChartACourseInitializeSimulation`, `Game_ChartACoursePrepareUpgradeCandidates`, `Game_ChartACourseGrantPlayerUpgradeChoice`, `Game_ChartACourseSetUpgradeTier`
- **Save/Restore**: `Game_SetGameRestoreCallback` / `Game_RemoveGameRestoreCallback` for mid-game saves

#### Combat Mode
- **Round Structure**: Buy Period (80s) → Fight → Round End → next round
- **Victory**: First team to win `victoryThreshold` (3) rounds
- **Buy Period**: Resources granted (scaled by team size ratio); production buildings spawned with 100x speed
- **Capture Point**: Central outpost (`building_defense_outpost_neu`), invulnerable, world-owned between rounds
- **Round End Conditions**: Last team standing OR timer expires (120s default after capture)
- **Age Configuration**: Starting age 1–4 with corresponding buildings and upgrade unlocks
- **Resources Per Round**: Med (2000F/1000W/1000G) or High (3000F/1500W/1500G)
- **Restrictions**: Bombards, cannons blocked; siege engineers, arrow slits, etc. restricted
- **Surrender**: Per-round surrender via network event
- **Stats UI**: XAML overlay showing rounds won, units, kills, losses per team

#### Full Moon
- **Werewolf Waves**: Spawn every `wave_interval` (6 min default, configurable via `option_moon_surge_interval`)
- **Intensity Levels** (3 presets): Starting count {2, 3, 5}, multiplier {0.3, 0.5, 0.5}, decay {0.8, 0.75, 0.75}
- **Blueprints**: Age-scaled `gaia_werewolf_1` through `gaia_werewolf_4` based on median player age
- **Spawn Logic**: Per-player spawn groups, positions filtered by `spawn_distance_cutoff_percent` (10%)
- **Moon Rush**: `Entity_SetStateModelBool(entity, "moon_rush_signal", true)` activates rush; deactivated after half the wave interval
- **Atmosphere**: Transitions between initial and `seasonal_variations/full_moon` during surges
- **Fallback**: If DynamicSpawning markers unavailable, falls back to animal-position-based spawning

#### King of the Hill
- **Capture Point**: `capture_point` entity spawned at most central viable position
- **Spawn Timing**: Found on init, sorted by distance to center; markers sorted via `SortByClosestToCenter`
- **Reward System**: StateModel-driven: `capture_point_reward_points`, `capture_point_control_timer`, `capture_point_reward_iteration`
- **Reward Interval**: {90, 60, 30} seconds per preset option
- **Capture Events**: Full state machine via `GE_StrategicPointChanged` with 12 change types (Captured, Reverting, Secured, UnCaptured, Seized, StartedCapture, StartedCooldown, StartedRevertingCooldown, Halted, Init, CapturedContested, CapturedContestedEnded)
- **Audio**: Distinct SFX for player/ally/enemy capture and neutralization events
- **Bonus Resources**: +500 of each resource at start for all players

#### Map Monsters
- **Monster Types**: Land (`gaia_monster_land`) and Water (`gaia_monster_water`)
- **Spawn Interval**: Default 8 min, configurable, clamped to [5, 20] minutes
- **Alternating Spawns**: Alternates between land and sea each interval
- **Spawn Finding**: Two systems — DynamicSpawning markers (preferred) with fairness filter, or grid-sampled map positions
- **Fairness Filtering**: `spawn_threshold_player_min` (15%), `spawn_threshold_from_mid` (15%), `spawn_threshold_diff` (28%)
- **Single Player**: Separate thresholds `single_player_threshold_min` (45%) and `_max` (90%)
- **Despawn**: Previous monster despawned before new one spawns
- **Ownership**: Monsters set to world-owned (neutral) via `SGroup_SetWorldOwned`

#### Season's Feast
- **Gift Haul**: Collectible resource pickups spawned at intervals
- **Gift Count**: `#PLAYERS + wave_increase` per wave (doubled if `option_double_gift_spawn_rate`)
- **Spawn Interval**: Every 110s after initial 1min delay
- **Blueprints**: `resource_pickup_gift_haul_land` and `resource_pickup_gift_haul_water` based on terrain
- **Spacing**: Minimum 32-unit distance between gifts; skips positions with uncollected gifts
- **Training Hints**: Registered training goal sequence pointing at scout/khan unit

#### None Mode
- Minimal campaign shell — no win conditions, no scoring
- Optionally removes all units/buildings (`option_initial_units` = none)
- Imports only `cardinal.scar`, event_cues, currentageui, dynasty UI, cheat

#### Sandbox Mode
- Explicitly no win conditions — designed for player experimentation and modding
- Imports score, diplomacy, vision, cheat, classic_start
- Diplomacy disabled, tribute enabled by default

### Timers

| Timer/Rule | Mode | Interval | Purpose |
|---|---|---|---|
| `ChaoticClimate_StartPositiveSummer` | chaotic_climate | OneShot 30s | First season activation |
| `ChaoticClimate_EndSeason` | chaotic_climate | OneShot `season_duration_time` | End current season buff |
| `ChaoticClimate_StartNextSeason` | chaotic_climate | OneShot `season_cooldown_time` | Begin next season |
| `ChaoticClimate_UpdateUI` | chaotic_climate | Interval (every frame) | Refresh season progress widget |
| `ChartACourse_PrepareUpgradeCandidatesForPlayers` | chart_a_course | Interval `upgrade_selection_interval` | Generate new upgrade choices |
| `ChartACourse_AutoSelectForLocalPlayer` | chart_a_course | OneShot (interval - 10s) | Force-pick if player hasn't chosen |
| `CombatMode_BuyPeriod` | combat_mode | Timer 80s | Buy period countdown |
| `CombatMode_CheckObjective` | combat_mode | Every tick | Monitor capture/elimination |
| `CombatMode_RoundTimer` | combat_mode | Interval 1s | Countdown after outpost captured |
| `CombatMode_CheckStartRound` | combat_mode | Interval 1s | Wait `timeToNextRound` (20s) between rounds |
| `FullMoon_SpawnWave` | full_moon_mode | Interval 6min | Spawn next werewolf wave |
| `OneShot_EndCurrentMoonRush` | full_moon_mode | OneShot (wave_interval * 0.5) | End moon rush state |
| `KingOfTheHill_NotifyHillSpawn` | king_of_the_hill | OneShot 10s | Notify players about hill spawn |
| `KingOfTheHill_RewardPoints` | king_of_the_hill | Interval 1s | Tick reward points on capture |
| `MapMonsters_SpawnMonster` | map_monsters | Interval 8min | Spawn next monster |
| `SeasonsFeast_SpawnGifts` | seasons_feast | Interval 110s | Spawn gift haul wave |
| `SeasonsFeast_StartGiftSpawning` | seasons_feast | OneShot 1min | Initial gift spawn trigger |

## CROSS-REFERENCES

### Shared Globals
- **`_match`**: Every mode uses this global table with identical base structure (`options`, `is_cheat_enabled`, `is_diplomacy_enabled`, `is_tribute_enabled`, `speed{}`)
- **`PLAYERS`**: Global player table iterated by all modes for setup/debug
- **`TEAMS`**: Global team table used by Combat Mode for round tracking
- **`_combat_mode`**: Combat Mode-only global for round state, resources, UI

### Inter-System Dependencies
- All event modes depend on `gameplay/dynamic_spawning.scar` for spawn position finding (`DynamicSpawning_IsEnabled()`, `DynamicSpawning_GatherLandSpawnMarkers()`, `DynamicSpawning_GatherWaterSpawnMarkers()`, `DynamicSpawning_GatherAllSpawnMarkers()`, `DynamicSpawning_FilterByPlayerStartDistance()`)
- All modes call `Core_CallDelegateFunctions("DiplomacyEnabled", ...)` and `Core_CallDelegateFunctions("TributeEnabled", ...)` to configure diplomacy subsystem
- Replay stat tabs populated via `ReplayStatViewer_PopulateReplayStatTabs({"CurrentResourcesTemplate", "IncomeTemplate", "MilitaryTemplate"})`
- Win conditions are loaded via import but conditionally unregistered via `Core_UnregisterModule()`
- `Setup_GetWinConditionOptions(_match.options)` populates options from lobby settings

### Engine API Functions (Mode-Specific)
- **Chart A Course**: `Game_ChartACourseInitializeSimulation`, `Game_ChartACourseShutdownSimulation`, `Game_ChartACoursePrepareUpgradeCandidates`, `Game_ChartACourseGrantPlayerUpgradeChoice`, `Game_ChartACourseSetUpgradeTier`, `Game_ChartACourseGetRandomTierIndex`, `Game_ChartACourseGetRandomBuffSelectionIndexForLocalPlayer`, `Game_ChartACourseDoesPlayerHaveUpgradeChoicesAvailable`, `Game_ChartACourseGetPlayerUpgradeUIInfo`, `Game_ChartACourseSetUpgradeMenuVisibility`, `Game_ChartACoursePurgePlayerSelectionAndQueue`, `Game_ChartACourseGetPlayerAvailableUpgradeCandidatesTier`, `Game_ChartACourseGetPlayerUpgradeChoices`, `Game_ChartACourseSetPlayerUpgradeSelection`
- **Atmosphere**: `Game_LoadAtmosphereSettings`, `Game_TransitionToState`, `Game_SaveInitAtmosphereSettings`
- **KotH**: `World_KingOfTheHillDestroyTreesNearPoint`, `World_KingOfTheHillGetNumNonTreeNeutralEntitiesNearPoint`, `World_KingOfTheHillGetNumTreesNearPoint`, `Entity_GetStrategicPointRawRadius`

### Network Events
- `ChartACourse_SelectUpgradeNtw` — syncs upgrade selection across clients
- `ChartACourse_GrantUpgradeChoiceNtw` — cheat: grant upgrade choice
- `CombatMode_Surrender` — syncs per-round surrender

### Shared Function Patterns
- `{Mode}_SetSpeed(speed)` — identical implementation across all event modes
- `{Mode}_OnConstructionComplete(context)` — identical production acceleration on GE_ConstructionComplete
- `{Mode}_OnGameSetup()` — identical win condition option parsing logic
- FOW options: `FOW_ExploreAll()`, `FOW_ForceRevealAllUnblockedAreas()`, `FOW_PlayerRevealAll()`
- Nomad start: `Player_SetStateModelBool(player.id, "nomad_bonus_claimed", false)`
