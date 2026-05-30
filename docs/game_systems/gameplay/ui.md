# Gameplay: UI

## OVERVIEW

The UI gameplay system consists of a single file (`vizierui.scar`) that supports the Ottoman civilization's Vizier / Imperial Council mechanic. It registers as a core module via `Core_RegisterModule`, runs a per-frame update rule to track the local player's Vizier Points (stored as the `RT_Command` resource type), and plays an audio notification (`sfx_ui_vizier_point_notification`) whenever the point total increases. The system handles observer and replay mode gracefully by detecting local player ID changes. It is a lightweight, self-contained UI feedback layer with no objectives, difficulty scaling, or AI logic.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| vizierui.scar | core | Tracks Ottoman Vizier Points for the local player and plays a sound notification on point gain |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `VizierUI_OnInit` | vizierui.scar | Adds per-frame VizierUI_Update rule on init |
| `VizierUI_OnGameOver` | vizierui.scar | Removes update rule on game over |
| `VizierUI_Update` | vizierui.scar | Polls Vizier Points, plays sound on increase |

## KEY SYSTEMS

### Objectives

None. This file defines no `OBJ_` or `SOBJ_` constants.

### Difficulty

None. No `Util_DifVar` calls or difficulty-based scaling.

### Spawns

None. No wave/spawn logic or unit compositions.

### AI

None. No `AI_Enable`, encounter plans, or patrol logic.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Rule_Add(VizierUI_Update)` | Every frame | Polls `RT_Command` resource for local Ottoman player; fires sound on point increase |

### Vizier Point Tracking

- **Resource type**: `RT_Command` — Vizier Points are mapped to the engine's Command resource slot.
- **Persistent state**: `vizierData` table stores `localPlayerVizierPoints` (last known total) and `localPlayerID` (to detect player switches in replay/observer).
- **Race gate**: Update logic early-returns for non-Ottoman players, storing only the player ID.
- **Sound cue**: `sfx_ui_vizier_point_notification` plays via `Sound_Play2D` when points increase and the local player ID has not changed (prevents false triggers on observer player switch).

## CROSS-REFERENCES

### Module Registration

- Registers with `Core_RegisterModule("VizierUI")` — hooks into the core lifecycle callbacks `OnInit_PartB()` and `OnGameOver()` defined in `core.scar`.

### Engine API Calls

| Function | Purpose |
|----------|---------|
| `Game_GetLocalPlayer()` | Retrieves the local (viewing) player |
| `Player_GetRaceName()` | Checks if local player is Ottoman |
| `Player_GetID()` | Gets numeric player ID for replay/observer tracking |
| `Player_GetResource(player, RT_Command)` | Reads current Vizier Point total |
| `Sound_Play2D()` | Plays non-positional UI sound effect |
| `Rule_Add()` / `Rule_Remove()` | Manages per-frame update rule lifecycle |

### Imports / Shared Globals

- No explicit `import()` calls; relies on the core module system for lifecycle hooks.
- `vizierData` is the only global table; no inter-file function calls or shared state with other scripts.
