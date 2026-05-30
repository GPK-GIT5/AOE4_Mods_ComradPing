# AoE4 Game Configuration Reference

> **Source**: `C:\Program Files (x86)\Steam\steamapps\common\Age of Empires IV\` (v15.4.8719.0)  
> **User data**: `%USERPROFILE%\Documents\My Games\Age of Empires IV\`  
> **Workspace copy**: `game_data/extracted/aoe4/sysconfig.lua`, `game_data/extracted/aoe4/mods_meta_data.lua`  
> **Last Updated**: 2026-03-18

---

## Overview

AoE4 uses Lua-based configuration files for game settings and mod management. This reference documents the key files an AoE4 modder or SCAR scripter should understand.

---

## 1. sysconfig.lua — Game Settings Template

**Location**: `<install>/cardinal/sysconfig.lua` → workspace: `game_data/extracted/aoe4/sysconfig.lua`  
**Size**: ~5,700 lines, 255 unique settings, version `3666938`

### Format

Each setting is a table entry inside a top-level `configuration` array:

```lua
{
    setting = "windowmode",      -- unique setting key
    variantUInt = 0,             -- default value (typed: variantBool, variantInt, variantUInt, variantFloat, variantString, variantKey)
    canOverrideDefault = true,   -- can autodetect override?
    valueStore = valueStoreSystem, -- 1=system, 2=user (cloud-synced)
    nameLocID = 11149474,        -- localization string ID
    descLocID = 11149475,        -- description loc ID
    dataTemplate = DT_ComboBox,  -- UI widget type
    uiType = UT_List,            -- UI control type (see below)
    uiAvailability = UA_Both,    -- where setting appears
    telemetryName = "Window Mode", -- analytics label (max 64 chars)
    canPreview = false,          -- live preview in options?
    canChangeInGame = true,      -- can change during match?
    persistent = true,           -- saved to cloud?
}
```

### UI Type Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `UT_Bool` | 0 | Checkbox / toggle |
| `UT_Range` | 1 | Slider / ranged float (uses `rangeMin`, `rangeMax`, `tickFrequency`) |
| `UT_List` | 2 | Dropdown / combobox (uses `list = { {locNameID=..., key=...}, ... }`) |
| `UT_Custom` | 3 | Custom UI widget |

### Availability Enums

| Constant | Value | Scope |
|----------|-------|-------|
| `UA_Both` | 0 | Frontend + in-game |
| `UA_FE` | 1 | Frontend only |
| `UA_InGame` | 2 | In-game only |
| `PA_All` | 0 | All platforms |
| `PA_Steam` | 1 | Steam only |
| `PA_Xbox` | 2 | Xbox / MS Store only |
| `PA_PS5` | 3 | PS5 only |
| `HA_PC` | 1 | PC hardware |
| `HA_Xbox` | 2 | Xbox hardware |
| `HA_PS5` | 4 | PS5 hardware |
| `HA_Console` | 6 | Xbox + PS5 (bitmask) |
| `HA_All` | 7 | All hardware (bitmask) |

### Data Templates

| Constant | UI Widget |
|----------|-----------|
| `DT_ToggleCheckBox` | Checkbox toggle |
| `DT_ComboBox` | Dropdown list |
| `DT_Slider` | Range slider |
| `DT_HDR` | HDR-specific slider (rounded display) |
| `DT_Resolution` | Resolution picker |
| `DT_AudioInputDevice` | Audio input device picker |
| `DT_AudioOutputDevice` | Audio output device picker |
| `DT_Button` | Xbox button control |

### Value Store

| Constant | Value | Description |
|----------|-------|-------------|
| `valueStoreSystem` | 1 | Available immediately at startup |
| `valueStoreUser` | 2 | Requires cloud storage load; not available during early startup |

### Setting Categories (255 total)

Settings are organized into the `configuration` array without explicit categories, but can be grouped by domain:

| Domain | Example Settings | Count (approx) |
|--------|-----------------|-----------------|
| **Graphics** | `GraphicsQuality`, `Shadows`, `AntiAliasing`, `ModelDetail`, `TextureDetail`, `Reflections`, `VolumetricLighting`, `AmbientOcclusion` | ~50 |
| **Display** | `windowmode`, `resolution`, `VerticalSync`, `DynamicResolution*`, `HDR`, `FrameRateLimit`, `DynamicVerticalSync` | ~20 |
| **Audio** | `masterVolume`, `musicVolume`, `sfxVolume`, `speechVolume`, `tauntsVolume`, `AudioOutput*`, `VoiceChat*` | ~15 |
| **Camera** | `CameraMode`, `CameraRotation`, `CameraSnapIsActive`, `ScrollWheelZoom`, `DynamicCamera`, `FocusSelectedFollow` | ~15 |
| **Controls** | `Controls`, `InputDeviceType`, `MouseCursorSpeed`, `KeyboardPanSpeedFactor`, `EdgePan*`, `AnalogPanSpeed` | ~40 |
| **Controller** | `Controller*`, `LeftThumbstickDeadzone`, `RightThumbstickDeadzone`, `RumbleStrength`, `RadialHoldToggle` | ~15 |
| **HUD/UI** | `UIScale`, `HealthBarVisibilityMode`, `ShowPlayerScores`, `ShowGameTimer`, `MinimapZoomLevel`, `ShowHUD*` | ~30 |
| **Gameplay** | `DynamicTraining`, `AttackMoveBehaviour`, `ControlGroupCycleBehaviour`, `StickySelection`, `RightClickGarrison` | ~20 |
| **Accessibility** | `CaptionScale`, `SubtitleVisibility`, `StrongHighContrast`, `ReduceFlashes`, `SpeechToText`, `TextToSpeech*` | ~15 |
| **Social** | `AllowFriendRequests`, `AllowMessages`, `CrossNetwork`, `FilterChat`, `BlockUGC`, `EnableTaunts` | ~10 |
| **Events** | `event*` (notification toggles: `eventAgeUp`, `eventBuildingComplete`, `eventUnderAttack`, etc.) | ~10 |
| **Texture Streaming** | `TextureStreaming*` (advanced: max memory, mip counts, concurrent streams) | ~8 |
| **Campaign** | `CampaignAutoSave`, `CampaignDifficulty`, `RogueModeDifficulty`, `RogueModePerks` | ~5 |

### Modding Relevance

- Settings cannot be added by mods — the `configuration` table is engine-defined
- Mods can **read** current values via `Game_GetSettingAsString()` / `Game_GetSettingAsFloat()` etc.
- Useful for adapting mod behavior to player preferences (e.g., checking `UIScale` for HUD positioning)
- The `xboxOverride` field means some settings have platform-specific defaults

---

## 2. mods_meta_data.lua — Mod Load Order

**Location**: `%USERPROFILE%\Documents\My Games\Age of Empires IV\mods_meta_data.lua`  
**Workspace copy**: `game_data/extracted/aoe4/mods_meta_data.lua`

### Format

```lua
items = {
    {
        modKey = "CBA Custom v1f",  -- local mod: folder name under mods/local/
        priority = 1,               -- load order (lower = loaded first)
        enabled = true,
    },
    {
        modKey = "108834",          -- workshop mod: numeric Steam Workshop ID
        priority = 2,
        enabled = true,
    },
    -- ...
}
```

### Key Points

- **Local mods** use the mod folder name as `modKey` (e.g., `"CBA Custom v1f"`)
- **Workshop mods** use the numeric Steam Workshop ID as `modKey`
- `priority` determines load order — **lower number = loaded first** (overrides later mods)
- `enabled = true/false` toggles mod without removing it from the list
- File is rewritten by the game when mod list changes in the UI
- Mods are stored in:
  - Local: `%USERPROFILE%\Documents\My Games\Age of Empires IV\mods\local\<modKey>\`
  - Workshop: `%USERPROFILE%\Documents\My Games\Age of Empires IV\mods\<modKey>\`

---

## 3. User Data Directory

**Location**: `%USERPROFILE%\Documents\My Games\Age of Empires IV\`

| Path | Purpose |
|------|---------|
| `configuration_system.lua` | Active user settings (saved values from sysconfig template) |
| `mods_meta_data.lua` | Mod load order (see §2) |
| `local.ini` | Low-level engine config |
| `mods/` | Downloaded and local mod files |
| `mods/local/` | Local development mods |
| `LogFiles/` | Runtime logs (see §4) |
| `playback/` | Match replays |
| `screenshots/` | Screenshots |
| `matchhistory/` | Local match history cache |
| `keyBindingProfiles/` | Custom key binding profiles |
| `warnings.log` | Accumulated engine warnings |
| `flipchart.log` | UI/rendering log |
| `session_data.txt` | Current session metadata |
| `EssenceEditorLog.txt` | Content Editor (mod tools) output |

---

## 4. LogFiles — Debugging

**Location**: `%USERPROFILE%\Documents\My Games\Age of Empires IV\LogFiles\`

### Log Types

| Pattern | Content | Typical Size |
|---------|---------|-------------|
| `unhandled.YYYY-MM-DD.HH-MM-SS.txt` | Uncaught errors: network timeouts, SCAR runtime errors, asset load failures | 0.5–3 KB |
| `DataCRC###.txt` | Data integrity checksums (used for desync detection) | ~140 KB |
| `SyncError_OutOfSyncFrame_*.txt` | Desync dump — frame data when OOS detected | ~43 KB |
| `SyncError_PreviousFrame_*.txt` | Frame before desync — comparison data | ~43 KB |

### Reading Unhandled Logs

Unhandled logs use timestamped lines:

```
18:53:11.462   WorldwideAutomatch2Service::OnHostComplete - we're not polling...
19:26:20.369   BattleServerRelay::Process - 317 ms between calls!
```

**For SCAR modders**: Look for lines containing `SCAR`, `scarload`, `lua`, or `Runtime` to find script errors. The timestamp helps correlate with in-game events.

### SCAR-Specific Errors

When a SCAR script errors at runtime, the unhandled log contains:
- The error message and stack trace
- The script file path and line number
- The function call chain

**Tip**: Use `warnings.log` (182 KB, accumulates across sessions) for persistent error tracking. It captures engine warnings that repeat-fire during gameplay.

---

## 5. attributes.xml — Game Data Tables

**Location**: `<install>/cardinal/attrib/instances/` (extracted via Content Editor)  
**Format**: XML attribute databases defining all game entities

The attributes system is AoE4's core data layer — every unit, building, technology, and ability is defined as attribute instances. This data is not directly accessible from SCAR at runtime beyond blueprint lookups, but understanding it helps when:

- Debugging blueprint names that don't match expected behavior
- Verifying unit stats for mod tuning packs
- Cross-referencing entity types with the workspace `game_data/extracted/aoe4/data/` JSON extracts

The workspace already has extracted JSON versions under `game_data/extracted/aoe4/data/buildings/`, `game_data/extracted/aoe4/data/units/`, `game_data/extracted/aoe4/data/technologies/`, and `game_data/extracted/aoe4/data/civilizations/`.

---

## See Also

- [scar-engine-api-signatures.md](../api/scar-engine-api-signatures.md) — Full engine API with typed signatures
- [scar-api-functions.md](../api/scar-api-functions.md) — Curated API reference by category
- [constants-and-enums.md](../api/constants-and-enums.md) — Constants and enum values
- [game-events.md](../api/game-events.md) — GE_ event reference
