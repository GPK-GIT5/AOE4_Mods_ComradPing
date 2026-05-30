# Gameplay: Start Conditions

## OVERVIEW

The start conditions system handles the initial game state setup for standard Age of Empires IV matches, including age-based upgrade application, fog-of-war reveal around starting positions, and Nomad mode support. It is implemented in a single file (`classic_start.scar`) that registers as a Core module and hooks into the `PostInit` phase to read win-condition options, apply the selected starting age's upgrades to all players, reveal fog of war around each player's starting position, and optionally remove wolves for Nomad starts. An Expert-difficulty AI cheat grants AI players a larger reveal radius when the default radius is under 100.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| classic_start.scar | core | Configures player starting state — age upgrades, FOW reveal, Nomad wolf removal |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `ClassicStart_OnInit` | classic_start.scar | Empty init hook registered via Core module |
| `ClassicStart_PostInit` | classic_start.scar | Applies starting age upgrades, FOW reveal, Nomad logic |
| `ClassicStart_NomadRemoveAllWolves` | classic_start.scar | Removes all wolf entities for Nomad starts |

## KEY SYSTEMS

### Objectives

No objectives (`OBJ_` / `SOBJ_` constants) are defined in this file. Start conditions are a setup-phase system only, with no mission objective logic.

### Difficulty

| Parameter | What It Scales |
|-----------|---------------|
| `Game_GetSPDifficulty() == GD_EXPERT` | AI players receive a larger FOW reveal radius (100 instead of the default 70) when the configured `FOWRevealRadius` is less than 100 — gives Expert AI better initial map awareness |

### Spawns

No wave or spawn systems. The file does not create units; it only applies upgrades and reveals fog of war. In Nomad mode (`_match.is_nomad_start`), it skips per-player FOW/TC logic and instead removes all neutral wolves from the map via `ClassicStart_NomadRemoveAllWolves`.

### AI

- No `AI_Enable` or encounter/plan logic.
- Expert-difficulty AI cheat: when `difficulty == GD_EXPERT` and `FOWRevealRadius < 100`, AI players receive `FOW_PlayerRevealArea` with radius 100 (vs. the default 70 for human players). This is explicitly marked in the source as an "INTEGRATION WARNING" / temporary cheat.

### Timers

No `Rule_AddInterval` or `Rule_AddOneShot` calls. All logic runs synchronously during `PostInit`.

### Starting Age System

The `_classicStart.ages` table maps win-condition option keys to cumulative upgrade chains:

| Option Key | Age | Upgrades Applied |
|------------|-----|-----------------|
| `option_start_age_1` | Dark Age | `dark_age` |
| `option_start_age_2` | Feudal Age | `dark_age`, `feudal_age` |
| `option_start_age_3` | Castle Age | `dark_age`, `feudal_age`, `castle_age` |
| `option_start_age_4` | Imperial Age | `dark_age`, `feudal_age`, `castle_age`, `imperial_age` |

Upgrades are applied in **reverse chronological order** to prevent audio cue overlap (iterates `#initialUpgrades` down to 1). Each upgrade is checked with `Player_HasUpgrade` before being granted via `Player_CompleteUpgrade`.

### FOW Reveal

- Default reveal radius: **70** units around `player.startingPos`
- Reveal duration: **0.25** seconds (brief flash reveal)
- Skipped entirely for Nomad starts

### Data Lifecycle

The `_classicStart` data table is set to `nil` at the end of `ClassicStart_PostInit`, freeing memory after setup is complete. The module uses `Core_RegisterModule("ClassicStart")` for lifecycle hook registration.

## CROSS-REFERENCES

### Imports & Dependencies

| Dependency | Usage |
|------------|-------|
| Core module system (`Core_RegisterModule`) | Registers `ClassicStart` for `OnInit` / `PostInit` callbacks |
| `BP_GetUpgradeBlueprint` | Resolves age upgrade names to blueprint handles |
| `Setup_GetWinConditionOptions` | Reads lobby win-condition settings to determine starting age |
| `FOW_PlayerRevealArea` | Reveals fog of war at player start positions |
| `Player_HasUpgrade` / `Player_CompleteUpgrade` | Checks and applies age upgrades per player |
| `World_GetAllNeutralEntities` | Used in Nomad wolf cleanup |
| `EGroup_Filter` / `EGroup_DestroyAllEntities` | Filters for wolves and removes them |
| `Game_GetSPDifficulty` / `GD_EXPERT` | Difficulty check for AI FOW cheat |

### Shared Globals

| Global | Source | Usage |
|--------|--------|-------|
| `PLAYERS` | core.scar | Iterated to apply upgrades and FOW reveal to all players |
| `_match.is_nomad_start` | game mode setup | Controls Nomad-specific behavior (skip TC logic, remove wolves) |

### Inter-File Calls

- Called **by** `core.scar` via the module lifecycle (`OnInit` → `PostInit` sequence).
- No outbound calls to other mission or gameplay module functions beyond the standard SCAR API.
