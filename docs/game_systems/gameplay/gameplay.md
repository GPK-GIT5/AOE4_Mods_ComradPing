# Gameplay: Gameplay Systems

## OVERVIEW

This module collects the core gameplay-layer systems that operate across all AoE4 game modes and civilizations. It provides **cheat/debug infrastructure** for development, the **diplomacy and tribute** UI (including Xbox controller support), an **event cue** framework for player notifications (age-ups, pop-cap, Call-to-Action), a comprehensive **score tracking** system (military/economy/society/technology), a **shared-vision** system gated by market construction, **dynamic spawn-marker** utilities for generated maps, the **Chinese Dynasty UI**, the **Templar (Order of the Temple) age-up UI**, and a small **Current Age UI** bridge that feeds player age data into the replay-stat system. All systems register as `Core_RegisterModule` modules and follow the standard `OnInit → Start → OnGameOver` lifecycle.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `chatcheats.scar` | other | Implements client-side chat-cheat commands (convert units, gift resources, spawn armies, FoW toggle, invulnerability, instant build, teleport, fire, etc.) |
| `cheat.scar` | other | Thin network-event wrappers around chatcheats for multiplayer/Cardinal broadcast-message cheats; imports `chatcheats.scar` |
| `currentageui.scar` | core | Registers `CurrentAgeUI` module; pushes player age data into the replay-stat viewer via `ReplayStatViewer_RegisterPlayerDataContextUpdater` |
| `diplomacy.scar` | core | Full diplomacy & tribute system — UI creation (WPF/XAML), relation management, tax calculation, network tribute flow, event cues for tribute received |
| `xbox_diplomacy_menus.scar` | other | Xbox/controller-specific diplomacy UI variants (Request Aid, Tribute, Tribute+Settlement, Recruit Champions, Resource Locations); manages focus/input-enable toggling |
| `dynamic_spawning.scar` | core | Utility functions for gathering and filtering dynamic spawn markers by terrain type (land/water) and player-start distance; used by generated-map game modes |
| `event_cues.scar` | core | Event cue manager — handles age-up notifications per civ type, pop-cap warnings, Abbasid Golden Age cues, and the full Call-to-Action (CTA) system with minimap blips and auto-clear |
| `score.scar` | core | Score tracking module — computes military, economy, society, and technology sub-scores from build/kill/upgrade events; writes to state model for telemetry and replay stats |
| `vision.scar` | core | Shared line-of-sight management — disabled at match start, enabled between mutual allies once both build a market; responds to relationship and team changes |
| `current_dynasty_ui.scar` | other | Chinese Dynasty UI — displays current dynasty (Tang/Song/Yuan/Ming), tracks landmark construction for dynasty advancement, handles historic and Rogue variants |
| `templar_age_up_ui.scar` | other | Templar (Order of the Temple) civ age-up UI — populates commanderie data context with unit icons, costs, and production times for 9 commanderies |

---

## FUNCTION INDEX

### Cheats & Debug

| Function | File | Purpose |
|----------|------|---------|
| `CheatConvertSelectedUnits` | chatcheats.scar | Converts selected enemy units to player ownership |
| `CheatReplaceSheepWithWolves` | chatcheats.scar | Replaces all sheep on map with wolves |
| `ResourcesCheatAllBasic` | chatcheats.scar | Grants max of all resource types plus Jeanne XP |
| `CheatSetCurrentPopCapToMax` | chatcheats.scar | Sets pop cap to maximum override value |
| `CheatKillAllGaia` | chatcheats.scar | Kills all non-invincible gaia animals |
| `SpawnCheatArmy` | chatcheats.scar | Spawns core military unit set at town center |
| `SpawnCheatPhotonMan` | chatcheats.scar | Spawns photon_man easter-egg unit |
| `CheatSetFireToBuildings` | chatcheats.scar | Sets fire to selected buildings via modifier override |
| `ManageTheFires` | chatcheats.scar | Interval rule managing active building fires |
| `ChatCheatFOW` | chatcheats.scar | Toggles fog of war reveal for player |
| `ChatCheatInstantBuildAndGather` | chatcheats.scar | Applies 1000x harvest/construction/production modifiers |
| `ChatCheatAgeUpMultiplayer` | chatcheats.scar | Forces next age upgrade for player |
| `ChatCheatInvulnerable` | chatcheats.scar | Toggles invulnerability on all player units/buildings |
| `CheatTeleportSelectedSquads` | chatcheats.scar | Teleports selected squads to cursor position |
| `CheatExploredAll` | chatcheats.scar | Reveals entire map and ghosts all neutral entities |
| `CheatTurbo` / `CheatSlow` | chatcheats.scar | Toggles sim rate to 1000x or 1x |
| `Cheat_Init` | cheat.scar | Registers network cheat table via `GE_BroadcastMessage` |
| `Cheat_Callback` | cheat.scar | Dispatches network cheat messages to handler functions |

### Diplomacy & Tribute

| Function | File | Purpose |
|----------|------|---------|
| `Diplomacy_DiplomacyEnabled` | diplomacy.scar | Initializes `_diplomacy` data context, sets enabled state |
| `Diplomacy_TributeEnabled` | diplomacy.scar | Disables tribute as match option when false |
| `Diplomacy_OnInit` | diplomacy.scar | Registers network events and global event listeners |
| `Diplomacy_ToggleDiplomacyUI` | diplomacy.scar | Opens/closes diplomacy panel, manages ESC handler |
| `Diplomacy_ShowDiplomacyUI` | diplomacy.scar | Force-opens or force-closes diplomacy panel |
| `Diplomacy_SendTribute` | diplomacy.scar | Validates resources and sends tribute over network |
| `Diplomacy_SendTributeNtw` | diplomacy.scar | Network handler — transfers resources, applies tax, shows cues |
| `Diplomacy_ClearTribute` | diplomacy.scar | Resets all queued tribute amounts to zero |
| `Diplomacy_AddTribute` | diplomacy.scar | Adjusts tribute amount for one player/resource slot |
| `Diplomacy_GetTaxRate` | diplomacy.scar | Returns tribute tax rate (default 30%) |
| `Diplomacy_SetTaxRate` | diplomacy.scar | Sets tribute tax rate for a player |
| `Diplomacy_OverrideSettings` | diplomacy.scar | Override tribute/subtotal/score/team visibility flags |
| `Diplomacy_OverridePlayerSettings` | diplomacy.scar | Override per-player tribute visibility and resource enables |
| `Diplomacy_CreateDataContext` | diplomacy.scar | Builds full data context with player list, civ flags, tributes |
| `Diplomacy_CreateUI` | diplomacy.scar | Creates WPF XAML diplomacy panel (PC) or delegates to Xbox |
| `Diplomacy_OnPlayerDefeated` | diplomacy.scar | Hides/disables tribute for eliminated players |
| `Diplomacy_ShowEventCue` | diplomacy.scar | Shows event cues for received tribute (food/wood/gold/stone) |
| `DiplomacyMenus_Open` / `Close` | xbox_diplomacy_menus.scar | Opens/closes Xbox diplomacy panel with input toggling |
| `DiplomacyMenus_EnableMultiplier` | xbox_diplomacy_menus.scar | Switches tribute increment to 500 (controller trigger held) |
| `DiplomacyMenus_CreateXboxTributeUI` | xbox_diplomacy_menus.scar | Creates Xbox-specific tribute-only XAML layout |
| `DiplomacyMenus_CreateXboxTributeAndSettlementUI` | xbox_diplomacy_menus.scar | Creates Xbox tribute + settlement purchase layout |
| `DiplomacyMenus_CreateXboxRecruitChampionsUI` | xbox_diplomacy_menus.scar | Creates Xbox recruit-champions layout |
| `DiplomacyMenus_CreateXboxResourceLocationsUI` | xbox_diplomacy_menus.scar | Creates Xbox resource-locations layout |

### Event Cues

| Function | File | Purpose |
|----------|------|---------|
| `EventCues_Start` | event_cues.scar | Initializes player ages, schedules registration |
| `EventCues_Register` | event_cues.scar | Registers `GE_UpgradeComplete` and `GE_BuildItemComplete` listeners |
| `EventCues_Enable` | event_cues.scar | Enables/disables event cue processing |
| `EventCues_OnUpgradeComplete` | event_cues.scar | Detects age-up upgrades per civ (standard, Abbasid, Templar, etc.) |
| `EventCues_OnAbilityExecuted` | event_cues.scar | Detects Abbasid Golden Age ability |
| `EventCues_OnItemComplete` | event_cues.scar | Triggers pop-cap warning when at population limit |
| `EventCues_NotifyAgeUp` | event_cues.scar | Creates age-up event cue for self or other players |
| `EventCues_HighPriority` | event_cues.scar | Creates a high-priority center-screen cue |
| `EventCues_CallToAction` | event_cues.scar | Full CTA system — minimap blip, auto-clear on look, click handler |
| `EventCues_ClearCallToAction` | event_cues.scar | Clears active CTA, removes blip and timer rules |
| `CallToAction_OnEventCueClicked` | event_cues.scar | Handles CTA click — moves camera, executes callback/intel |
| `CallToAction_ClearOnLook` | event_cues.scar | Auto-clears CTA when position visible on screen |

### Score Tracking

| Function | File | Purpose |
|----------|------|---------|
| `Score_OnInit` | score.scar | Creates data context, registers global event listeners |
| `Score_Start` | score.scar | Accounts for initial squads, sets starting ages |
| `Score_DiplomacyEnabled` | score.scar | Stores diplomacy mode for score display |
| `Score_OnConstructionComplete` | score.scar | Adds building cost to military/economy/society score |
| `Score_OnItemComplete` | score.scar | Adds squad production cost to military/economy score |
| `Score_OnEntityKilled` | score.scar | Decrements score when entities/squads are killed |
| `Score_OnUpgradeStart` | score.scar | Caches upgrade cost at purchase time |
| `Score_OnUpgradeComplete` | score.scar | Applies upgrade cost to technology/society score |
| `Score_ModifyEconomicScore` | score.scar | Updates economy sub-score and total, writes state model |
| `Score_ModifyMilitaryScore` | score.scar | Updates military sub-score and total, writes state model |
| `Score_ModifySocietyScore` | score.scar | Updates society sub-score and total, writes state model |
| `Score_ModifyTechnologyScore` | score.scar | Updates technology sub-score and total, writes state model |
| `Score_TotalCost` | score.scar | Sums food + gold + stone + wood from cost table |
| `Score_GetCurrentAge` | score.scar | Returns 1–4 based on player upgrade state |
| `Score_UpdatePlayerStats` | score.scar | Replay stat callback — feeds current score |

### Vision

| Function | File | Purpose |
|----------|------|---------|
| `Vision_OnGameSetup` | vision.scar | Disables all shared LOS at match start |
| `Vision_Start` | vision.scar | Checks existing markets, grants vision between allies |
| `Vision_OnConstructionComplete` | vision.scar | Grants shared LOS when market constructed |
| `Vision_OnPlayerJoinedTeam` | vision.scar | Updates vision on team change |
| `Vision_OnRelationshipChanged` | vision.scar | Updates vision on diplomacy change |
| `Vision_UpdateVisionBetweenPlayers` | vision.scar | Enables LOS if mutual allies both have markets |
| `Vision_UpdateVisionForPlayer` | vision.scar | Updates LOS between one player and all others |

### Dynamic Spawning

| Function | File | Purpose |
|----------|------|---------|
| `DynamicSpawning_IsEnabled` | dynamic_spawning.scar | Checks if dynamic spawn markers are available |
| `DynamicSpawning_GatherAllSpawnMarkers` | dynamic_spawning.scar | Collects all spawn markers with optional filter |
| `DynamicSpawning_GatherLandSpawnMarkers` | dynamic_spawning.scar | Collects land-only spawn markers |
| `DynamicSpawning_GatherWaterSpawnMarkers` | dynamic_spawning.scar | Collects water-only spawn markers |
| `DynamicSpawning_FilterByPlayerStartDistance` | dynamic_spawning.scar | Filter callback — rejects markers too close to starts |
| `DynamicSpawning_DebugSetMarkerVisibility` | dynamic_spawning.scar | Toggles marker visibility for debugging |

### Chinese Dynasty UI

| Function | File | Purpose |
|----------|------|---------|
| `DynastyUI_OnInit` | current_dynasty_ui.scar | Detects Chinese civ, initializes dynasty data context |
| `DynastyUI_Start` | current_dynasty_ui.scar | Creates UI, registers construction/kill/player-change events |
| `DynastyUI_Update` | current_dynasty_ui.scar | Reads state model for current dynasty, updates unlock states |
| `DynastyUI_SetCivData` | current_dynasty_ui.scar | Configures wonders/upgrades/buildings for standard/historic/rogue |
| `DynastyUI_CreateDataContext` | current_dynasty_ui.scar | Populates upgrade/building/squad/wonder BP info for all 4 dynasties |
| `DynastyUI_ToggleDropdown` | current_dynasty_ui.scar | Toggles dynasty dropdown panel visibility |
| `DynastyUI_OnConstructionComplete` | current_dynasty_ui.scar | Triggers dynasty update when player constructs a building |
| `DynastyUI_OnEntityKilled` | current_dynasty_ui.scar | Re-evaluates dynasty if a completed building is destroyed |
| `CreateCostData` | current_dynasty_ui.scar | Utility — converts entity BP cost into icon+cost table |

### Templar Age-Up UI

| Function | File | Purpose |
|----------|------|---------|
| `TemplarAgeUpUI_OnInit` | templar_age_up_ui.scar | Detects Templar civ, creates commanderie data context |
| `TemplarAgeUpUI_CreateDataContext` | templar_age_up_ui.scar | Populates 9 commanderies with unit icons, costs, and timers |

### Current Age UI

| Function | File | Purpose |
|----------|------|---------|
| `CurrentAgeUI_OnInit` | currentageui.scar | Registers age-update callback with replay stat viewer |
| `CurrentAge_UpdatePlayerStats` | currentageui.scar | Sets `scarModel.Age` (0–3) from player upgrade state |

---

## KEY SYSTEMS

### Diplomacy & Tribute System
- **Module**: `Diplomacy` (registered via `Core_RegisterModule`)
- **Tribute flow**: Player increments resource amounts in UI → `Diplomacy_SendTribute()` validates locally → `Network_CallEvent("Diplomacy_SendTributeNtw")` → server executes `Player_GiftResource` with 30% tax deduction
- **Prerequisites**: Must reach Age II AND build a market (`trade_post` entity type)
- **Tax rate**: Default 30% (`_diplomacy.tribute.tax_rate = 0.3`), adjustable via `Diplomacy_SetTaxRate()`
- **Increment**: 100 per click (normal), 500 with Xbox left-trigger held
- **Limit**: 9999 per resource per target player
- **Xbox variants**: 4 separate XAML layouts — Tribute-only, Tribute+Settlement, Recruit Champions, Resource Locations
- **Override API**: `Diplomacy_OverrideSettings()` and `Diplomacy_OverridePlayerSettings()` for game-mode customization
- **Mongol exception**: Stone tribute disabled when target is Mongol or Golden Horde

### Event Cue System
- **Module**: `EventCues`
- **Age-up detection**: Handles standard upgrades (`feudal_age`, `castle_age`, `imperial_age`) plus special paths for Abbasid (`abbasid_wing_upgrade`), Ayyubid, Templar, and Golden Horde (`age_up_upgrade`)
- **Pop-cap warning**: Fires on `GE_BuildItemComplete` when `current_pop == pop_cap` (excludes Mongol sheep)
- **Abbasid Golden Age**: Detected via `GE_AbilityExecuted` with ability match
- **Call-to-Action (CTA)**: Full subsystem with 4 types:
  - `CTA_ALARM` — alert stinger
  - `CTA_CELEBRATE` — celebration stinger
  - `CTA_UNIQUE_STAKES` — raised stakes
  - `CTA_UNIQUE_CHANGE` — focus change
- **CTA features**: Minimap blip, auto-clear when camera looks at position (80% screen threshold), configurable duration (default 45s), click-to-camera-move, Intel event queuing with 2.75s speech delay
- **Cue templates**: `high_priority` (10s lifetime), `cta_alarm` (65s lifetime)

### Score Tracking System
- **Module**: `Score`
- **Sub-scores**: Military, Economy, Society, Technology
- **Multipliers**: All 20% of resource cost (`_score.multiplier = 0.2` for military, economy, society, technology); resources at 10%
- **Military entities**: wall, tower, outpost, castle, barracks, stable, archery_range, siege_workshop, siege
- **Society entities**: landmark, wonder
- **Score flow**: `GE_ConstructionComplete` → classify by entity type → add cost × multiplier; `GE_BuildItemComplete` → classify squad as military/other; `GE_EntityKilled` → subtract cost × multiplier; `GE_UpgradeComplete` → technology score (or society for Abbasid wings)
- **Upgrade cost caching**: Cost recorded at `GE_UpgradeStart` to handle Sultanate time-cost and blueprints that change cost
- **Telemetry**: Writes `economy_score`, `military_score`, `society_score`, `technology_score`, `total_score` to player state model
- **Replay stats**: Registers with `ReplayStatViewer` for `PlayerScoreTemplate` tab

### Shared Vision System
- **Module**: `Vision`
- **Prerequisite**: Both players must have built a `trade_post` (market)
- **Logic**: Enabled only between mutual allies (`R_ALLY` in both directions) who both have markets
- **Events**: Responds to `GE_ConstructionComplete`, `OnPlayerJoinedTeam`, `OnRelationshipChanged`

### Chinese Dynasty System
- **Module**: `DynastyUI`
- **Dynasties**: Tang (1), Song (2), Yuan (3), Ming (4)
- **Upgrades**: `player_dynasty0_chi` through `player_dynasty3_chi`
- **Dynasty units**: Repeater Crossbowman (Song), Fire Lancer (Yuan), Grenadier (Ming)
- **Dynasty buildings**: Village (Song), Granary (Yuan), Pagoda (Ming)
- **State model keys**: `current_dynasty_chi`, `dynasty_X_was_completed_chi`, `district_spec_permanent_dynasty_bonuses_chi`
- **Wonder tracking**: Checks pairs of landmarks per age tier; uses `Player_HasEntity` to verify construction
- **Variants**: Standard Chinese, Historic Chinese (`_ha_01` suffix), Rogue mode
- **Historic landmarks**: Different landmark set (Prefecture, Meditation Gardens, Shaolin Temple, etc.)

### Templar Commanderie System
- **Module**: `TemplarAgeUpUI`
- **Commanderies** (9 total): Knight Hospitaller, Chevalier Confrere, Serjeant, Heavy Spearman, Genoese Crossbow, Genitour, Szlachta Knight, Teutonic Knight, Condottiero
- **Venice special**: Commanderie 9 has 3 units (Condottiero, Galleass, Venetian Trader)
- **Data**: Icons, costs, production times populated from blueprint lookups at runtime

### Dynamic Spawn Markers
- **Terrain types**: `eTerrainType` enum — sky (0), land (1), water (2)
- **Marker source**: `dist_dynamic_spawn_marker` EGroup from map data
- **Filter API**: Accepts callback `function(marker_entity, context_data) → bool` for custom filtering
- **Built-in filter**: `DynamicSpawning_FilterByPlayerStartDistance(marker, minDistance)` — rejects markers within `minDistance` of any player start

### Cheat System
- **Architecture**: Two-layer — `cheat.scar` handles network broadcast (`GE_BroadcastMessage`) dispatch; `chatcheats.scar` implements per-player commands
- **Guard**: Network cheats only execute if `-dev` command-line flag is set
- **Cheat registry** (in `Cheat_Init`): `AGEUP`, `ECONOMY`, `FOW`, `INVULNERABLE`, `INSTANTBUILD`, `DESTROYHOVERED`, `TELEPORTSELECTED`
- **Chat cheats** add more: resources (per type + all), convert units, spawn army, photon man, fire, kill gaia, explored map, turbo/slow sim, hide UI, invulnerable toggle, lose instantly

---

## CROSS-REFERENCES

### Imports
- `cheat.scar` → `import("gameplay/chatcheats.scar")`
- `diplomacy.scar` → `import("gameplay/xbox_diplomacy_menus.scar")` (conditional on `UI_IsXboxUI()`)
- `currentageui.scar` → `import("replay/replaystatviewer.scar")`
- `score.scar` → `import("replay/replaystatviewer.scar")`

### Shared Globals & Data
- `PLAYERS` table — used by diplomacy, score, event cues, vision for iterating all players
- `Core_GetPlayersTableEntry()` / `Core_GetPlayersTableEntryFromIndex()` — shared player-lookup API
- `_diplomacy` — global state for diplomacy module, accessed by both `diplomacy.scar` and `xbox_diplomacy_menus.scar`
- `_events` — global state for event cues
- `_score` — global state for score tracking
- `_vision` — global state for vision module
- `_dynasty` — global state for Chinese dynasty UI
- `gFoWCheat`, `gInstantBuildCheat`, `gInvulnerableCheat`, `gModifierList`, `gHideUICheat` — cheat toggle state tables

### Core Lifecycle Callbacks
All modules implement standard callbacks dispatched by `core.scar`:
- `*_OnInit()` — called by `Core_OnInit()`
- `*_Start()` — called by `_StartMission()`
- `*_OnGameOver()` — called by `Core_OnGameOver()`
- `*_OnGameRestore()` — called by `Core_OnGameRestore()`
- `*_OnPlayerDefeated()` — called by `Core_SetPlayerDefeated()`

### Inter-Module Calls
- `Score_OnRelationshipChanged()` — called by diplomacy via `Core_CallDelegateFunctions("OnRelationshipChanged")`
- `Core_CallDelegateFunctions("OnTributeSent")` — fired from `Diplomacy_SendTributeNtw` after tribute completes
- `ReplayStatViewer_RegisterPlayerDataContextUpdater()` — used by both `currentageui.scar` and `score.scar`
- `ReplayStatViewer_PopulateReplayStatTabs({"PlayerScoreTemplate"})` — registered by score module
- `PlayerColour_SetConfigChangedCallback(Diplomacy_UpdateNameColours)` — diplomacy hooks into color config changes
- `Vision_OnRelationshipChanged` and `Vision_OnPlayerJoinedTeam` — called as delegate functions from core

### UI Data Contexts
- `"DiplomacyUI"` — diplomacy panel data context
- `"DynastyUI"` → `DynastyUI` — Chinese dynasty panel
- `"TemplarAgeUpDataContext"` — Templar commanderie data context
- All use `UI_AddChild("ScarDefault"/"ScarNotReplay"/"ScarAlwaysVisible")` for WPF XAML injection

### Network Events
- `"Diplomacy_ChangeRelationNtw"` — relationship change (currently commented out)
- `"Diplomacy_SendTributeNtw"` — tribute resource transfer
- Cheat system uses `GE_BroadcastMessage` (type 0) for network cheat dispatch

### Blueprint Cross-References
- Age upgrades: `feudal_age`, `castle_age`, `imperial_age` — shared across score, event cues, current age UI, diplomacy
- Chinese dynasties: `player_dynasty0_chi` – `player_dynasty3_chi`
- Templar units: 9 unique squad BPs across commanderies
- Cheat unit spawns: `scar_spearman`, `scar_archer`, `scar_manatarms`, `scar_handcannon`, `scar_crossbowman`, `scar_horseman`, `scar_knight`, `unit_photon_man`
