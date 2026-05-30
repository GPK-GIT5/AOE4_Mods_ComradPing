# Onslaught SCAR Pattern Library

> Canonical code patterns extracted from Onslaught source. Use these as
> templates when adding new modules, options, rewards, debug suites, or
> UI elements.

Auto-generated on 2026-04-02. Source: `Gamemodes/Onslaught/assets/scar/`

---

## 1. Module Registration (AGS Lifecycle)

Every gameplay system is a **registered module** with standard lifecycle hooks.
The Core framework calls these delegates in order during game startup.

**Canonical example:** `conditions/ags_annihilation.scar`

```lua
import("conditions/conditiondata/ags_annihilation_data.scar")

AGS_ANNIHILATION_MODULE = "AGS_Annihilation"
AGS_ANNIHILATION_OBJECTIVE = nil
AGS_ANNIHILATION_ACTIVE = true

Core_RegisterModule(AGS_ANNIHILATION_MODULE)

-- Called first: gate module on settings. Unregister if disabled.
function AGS_Annihilation_UpdateModuleSettings()
    if not AGS_GLOBAL_SETTINGS.Annihilation then
        Core_UnregisterModule(AGS_ANNIHILATION_MODULE)
    end
end

-- Called before game start: setup data tables and resources.
function AGS_Annihilation_PresetFinalize()
    AGS_Annihilation_DefineCheapestSquads()
end

-- Called when gameplay begins: register event handlers.
function AGS_Annihilation_OnPlay()
    Rule_AddGlobalEvent(AGS_Annihilation_OnEntityKilled, GE_EntityKilled)
    Rule_AddGlobalEvent(AGS_Annihilation_OnLandmarkDestroyed, GE_EntityLandmarkDestroyed)
    Rule_AddGlobalEvent(AGS_Annihilation_OnConstructionComplete, GE_ConstructionComplete)
    Rule_AddGlobalEvent(AGS_Annihilation_OnDamageReceived, GE_DamageReceived)
    AGS_Annihilation_CreateObjective()
end

-- Called on player defeat: cleanup for that player.
function AGS_Annihilation_OnPlayerDefeated(player, reason)
    AGS_Annihilation_RemoveObjective()
end

-- Called on game end: remove all event handlers.
function AGS_Annihilation_OnGameOver()
    Rule_RemoveGlobalEvent(AGS_Annihilation_OnEntityKilled)
    Rule_RemoveGlobalEvent(AGS_Annihilation_OnLandmarkDestroyed)
    Rule_RemoveGlobalEvent(AGS_Annihilation_OnConstructionComplete)
    Rule_RemoveGlobalEvent(AGS_Annihilation_OnDamageReceived)
end
```

**Lifecycle delegate order:**
1. `UpdateModuleSettings()` — gate on settings
2. `PresetFinalize()` — pre-play setup
3. `OnPlay()` — event registration
4. `TreatyStarted()` / `TreatyEnded()` — pause hooks
5. `OnPlayerDefeated(player, reason)` — per-player cleanup
6. `OnGameOver()` — final cleanup

**Naming convention:** `AGS_ModuleName_DelegateName()`

---

## 2. Option Declaration & Parsing

Options flow from the lobby UI through `AGS_GLOBAL_SETTINGS` to runtime branching.

**Declaration** (`ags_global_settings.scar` ~L89):
```lua
AGS_GLOBAL_SETTINGS = {
    Annihilation = false,
    Elimination = false,
    Treaty = 0,
    StartingAge = 1,
    TeamVictory = true,
    -- Onslaught-specific:
    Option_Reward_Age = false,
    Option_SiegeLimit = 0,
    Option_BuildingLimit = 0,
}
```

**Parsing** (`ags_global_settings.scar` ~L233):
```lua
function AGS_GlobalSettings_DefineWinConditions(category)
    if category.option_win_condition_annihilation ~= nil then
        AGS_GLOBAL_SETTINGS.Annihilation = category.option_win_condition_annihilation
    end
end
```

**Runtime branching** (`gameplay/cba_options.scar`):
```lua
function CBA_Options_UpdateModuleSettings()
    if AGS_GLOBAL_SETTINGS.Option_SiegeLimit == 0
       and AGS_GLOBAL_SETTINGS.Option_BuildingLimit == 0 then
        Core_UnregisterModule(CBA_OPTIONS_MODULE)
    end
end
```

---

## 3. Blueprint Resolution (Civ-Aware)

Entity lookups go through `AGS_ENTITY_TABLE` with faction mapping for variants.

**Faction map** (`helpers/ags_blueprints.scar` ~L153):
```lua
AGS_CIV_FACTION_MAP = {
    abbasid_ha_01  = "abbasid",
    french_ha_01   = "french",
    chinese_ha_01  = "chinese",
    hre_ha_01      = "hre",
    japanese_ha_sen = "japanese",
    mongol_ha_gol  = "mongol",
    sultanate_ha_tug = "sultanate",
    lancaster      = "english",
    byzantine_ha_mac = "byzantine",
    templar        = "sultanate",
}
```

**Lookup chain:**
```lua
local player_civ = Player_GetRaceName(player.id)
local branch_civ = AGS_CIV_FACTION_MAP[player_civ] or player_civ

-- Entity table lookup: logical name → civ-specific EBP string
local ebp_name = AGS_ENTITY_TABLE[branch_civ]["spearman"]
-- e.g., "unit_spearman_1_eng" for English

-- Resolve to blueprint
local sbp = BP_GetSquadBlueprint(ebp_name)
```

**Important:** Use `AGS_CIV_FACTION_MAP` (not deprecated `AGS_CIV_PARENT_MAP`) for
all faction branching. Use raw `player_civ` for variant-specific EBP selection.

---

## 4. Rule & Timer Patterns

Three rule types handle game events and timed actions.

### Global Event (reacts to game state changes)
```lua
-- Register
Rule_AddGlobalEvent(MyModule_OnEntityKilled, GE_EntityKilled)

-- Callback receives context table
function MyModule_OnEntityKilled(context)
    local victim = context.victim    -- entity
    local killer = context.killer    -- entity (may be nil)
    local player = context.player    -- player owning entity
end

-- Cleanup
Rule_RemoveGlobalEvent(MyModule_OnEntityKilled)
```

### Interval (recurring timer)
```lua
Rule_AddInterval(MyModule_PeriodicCheck, 5.0)  -- every 5 seconds

function MyModule_PeriodicCheck()
    -- runs every interval until removed
end

Rule_Remove(MyModule_PeriodicCheck)  -- stop
```

### OneShot (delayed single execution)
```lua
-- With payload data
Rule_AddOneShot(MyModule_DelayedAction, 12, {text = 11183992, sfx = "alert"})

function MyModule_DelayedAction(context, data)
    -- data.text, data.sfx available
end
```

### Common game events
| Event | Fires when |
|-------|-----------|
| `GE_EntityKilled` | Any entity dies |
| `GE_EntityLandmarkDestroyed` | Landmark destroyed |
| `GE_ConstructionComplete` | Building finishes construction |
| `GE_DamageReceived` | Entity takes damage |
| `GE_StrategicPointChanged` | Sacred site captured/neutralized |
| `GE_UpgradeComplete` | Research finishes |
| `GE_PlayerBeingAttacked` | Player structures under attack |

---

## 5. Player Iteration

Standard pattern for looping over all players.

```lua
-- Ordered iteration (most common)
for i, player in ipairs(PLAYERS) do
    if player == nil then break end
    local civ = Player_GetRaceName(player.id)
    local score = Onslaught_GetPlayerScore(player)
end

-- Lookup by ID
local entry = Core_GetPlayersTableEntry(player_id)

-- Common player fields
-- player.id      — numeric ID for all Player_ API calls
-- player.index   — 1-based position in PLAYERS array
```

**Filter to alive players only:**
```lua
for i, player in ipairs(PLAYERS) do
    if player == nil then break end
    if not Core_IsPlayerEliminated(player.id) then
        -- active player logic
    end
end
```

---

## 6. Entity/Squad Query Patterns

### Get & filter player entities
```lua
local eg = Player_GetEntities(player.id)
EGroup_Filter(eg, "military", FILTER_KEEP)    -- keep only military
local count = EGroup_CountSpawned(eg)
local first = EGroup_GetEntityAt(eg, 1)       -- 1-indexed
```

### Type checking
```lua
if Entity_IsOfType(entity, "building") then ... end
if Entity_IsEBPOfType(entity, "wonder") then ... end
if Squad_IsOfType(squad, "cavalry") then ... end
if Squad_IsSBPOfType(squad, "siege") then ... end
```

### World entity search
```lua
local eg = EGroup_Create("temp_neutrals")
World_GetAllNeutralEntities(eg)
EGroup_Filter(eg, "strategic_point", FILTER_KEEP)
```

### Blueprint name check
```lua
local bp = Entity_GetBlueprint(entity)
local name = BP_GetName(bp)
if string.find(name, "town_center") then ... end
```

---

## 7. Reward Definition

Rewards are per-civ tables keyed by kill threshold.

**File:** `rewards/cba_rewards_onslaught.scar`

```lua
-- Initialize all civ tables
_CBA.rewards["english"] = {}

-- Starter reinforcement (threshold 0 = start of game)
_CBA.rewards["english"][0] = {
    unit_upgrade = BP_GetSquadBlueprint("unit_manatarms_3_eng"),
    num_upgrade = 40,
}

-- Upgrade reward
_CBA.rewards["english"][100] = {
    title = Loc_FormatText("$42764", "$1000893"),   -- "Upgrade: Siege Engineering"
    upgrade = AGS_UP_SIEGE_ENGINEERS,                -- global BP constant
}

-- Named upgrade (string-based)
_CBA.rewards["english"][175] = {
    title = Loc_FormatText("$42764", "$11245756"),
    upgradeBP = "upgrade_longbow_make_camp_eng",     -- resolved at runtime
}

-- Unit spawn reward
_CBA.rewards["english"][1500] = {
    title = "2x Bombards",
    unit = BP_GetSquadBlueprint("unit_bombard_4_eng"),
    num = 2,
}

-- Conditional age reward
if AGS_GLOBAL_SETTINGS.Option_Reward_Age then
    _CBA.rewards["english"][500] = {
        title = "$11149424",
        age = 2,
    }
end
```

**Reward entry fields:**
| Field | Type | Purpose |
|-------|------|---------|
| `title` | string/LocID | Display text |
| `upgrade` | BP handle | Global upgrade constant (e.g., `AGS_UP_SIEGE_ENGINEERS`) |
| `upgradeBP` | string | Upgrade blueprint name (resolved at runtime) |
| `unit` | SBP handle | Squad blueprint for spawning |
| `num` | number | Count to spawn |
| `unit_upgrade` | SBP handle | Reinforcement squad (replaces existing) |
| `num_upgrade` | number | Reinforcement count |
| `age` | number | Age-up reward (gates on `Option_Reward_Age`) |

---

## 8. UI DataContext Binding

UI state flows through a single `PlayerUiDataContext` table pushed to XAML each update cycle.

**Initialization** (`playerui/playerui_datacontext.scar`):
```lua
PlayerUiDataContext = {}

PlayerUiDataContext.TeamSummaryLeft = {
    WorkerPopulation = 0,
    MilitaryPopulation = 0,
    KillScore = 0,
    KillScorePulseActive = false,
}

PlayerUiDataContext.limits = {
    siege_visible = false, siege_current = 0, siege_max = 1,
    siege_counter = "0 / 0", siege_fg = "#FFFFFF",
}

PlayerUiDataContext.rewardProgressText = "0 / 0"
PlayerUiDataContext.rewardIcons = {}
```

**Update cycle** (`playerui/playerui_updateui.scar`):
```lua
-- Modify fields directly
PlayerUiDataContext.limits.siege_current = current_count
PlayerUiDataContext.limits.siege_counter = tostring(current_count) .. " / " .. tostring(max_count)

-- Push all changes to XAML in one batch (guarded)
pcall(UI_SetDataContext, "PlayerUIHud", PlayerUiDataContext)
```

**XAML safety constraints** — these binding types crash on Toggle UI:
- No `Width`/`Height`/`Opacity`/`RenderTransform` bound via DataContext
- Static values for these properties (no binding) are safe
- Always use `pcall()` wrapping `UI_SetDataContext` for post-teardown safety

---

## 9. Debug Suite Structure

Debug suites follow a consistent pattern with module registration.

```lua
-- Local state and constants (prefixed with module abbreviation)
local _MY_DELAY = 0.5
local _my_state = { pass = 0, fail = 0, total = 0 }

-- Assertion helper
local function _MY_Assert(test_name, condition, detail)
    _my_state.total = _my_state.total + 1
    if condition then
        _my_state.pass = _my_state.pass + 1
        AGS_Print("[PASS] " .. test_name)
    else
        _my_state.fail = _my_state.fail + 1
        AGS_Print("[FAIL] " .. test_name .. " — " .. tostring(detail))
    end
end

-- Main entry point (registered with debug dispatcher)
function Debug_MyFeatureTest()
    _my_state = { pass = 0, fail = 0, total = 0 }
    AGS_Print("=== My Feature Test Suite ===")

    _MY_Assert("basic check", some_value ~= nil, "value was nil")
    _MY_Assert("count check", count > 0, "count=" .. tostring(count))

    AGS_Print(string.format("Results: %d/%d passed", _my_state.pass, _my_state.total))
end
```

**Tag-based dispatch:** `debug.run("myfeature")` calls registered handler.

---

## 10. Civ-Specific Branching

When behavior varies by civilization, branch on `Player_GetRaceName`.

```lua
local civ = Player_GetRaceName(player.id)
local faction = AGS_CIV_FACTION_MAP[civ] or civ  -- normalize variants

-- Faction-level branching (same behavior for all variants of a civ)
if faction == "english" then
    -- English + Lancaster share this path
elseif faction == "chinese" then
    -- Chinese + Zhu Xi share this path
end

-- Variant-specific branching (when variants differ)
if civ == "lancaster" then
    -- Lancaster-specific EBP
    local sbp = BP_GetSquadBlueprint("unit_longbow_2_lan")
elseif civ == "english" then
    local sbp = BP_GetSquadBlueprint("unit_longbow_2_eng")
end
```

---

## Quick Reference: Common API Functions (Top 20 in Onslaught)

| Function | Calls | Usage |
|----------|-------|-------|
| `Loc_FormatText(fmt, ...)` | 769 | Localization string formatting |
| `BP_GetSquadBlueprint(name)` | 354 | Resolve squad blueprint by name |
| `Entity_IsOfType(entity, type)` | 210 | Entity type check |
| `AGS_Print(msg)` | 148 | Debug/diagnostic logging |
| `Squad_IsOfType(squad, type)` | 135 | Squad type check |
| `Player_GetRaceName(id)` | 121 | Get civilization string |
| `Rule_AddOneShot(fn, delay, data)` | 117 | Delayed one-time execution |
| `Player_SetEntityProductionAvailability(...)` | 88 | Enable/disable production |
| `World_GetGameTime()` | 87 | Current game clock |
| `Entity_IsEBPOfType(entity, type)` | 85 | Entity blueprint type check |
| `Loc_Empty()` | 75 | Empty localized string |
| `World_Pos(x, y, z)` | 61 | Create world position |
| `Core_GetPlayersTableEntry(id)` | 55 | Player ID → table entry |
| `Rule_AddGlobalEvent(fn, event)` | 53 | Register event handler |
| `Squad_IsSBPOfType(squad, type)` | 52 | Squad blueprint type check |
| `Player_ObserveRelationship(p1, p2, r)` | 48 | Set diplomacy |
| `Player_GetEntities(id)` | 46 | Get all player entities |
| `UI_CreateEventCueClickable(...)` | 44 | In-game notification |
| `Player_SetResource(id, res, amt)` | 43 | Set resource amount |
| `Core_RegisterModule(name)` | 43 | Module registration |
