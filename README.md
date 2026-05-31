# Age of Empires 4 — Modding Workspace

A development and reference workspace for AoE4 SCAR scripting, custom game modes, scenarios, and mod tooling.
Contains live mod source, extracted game data, reference documentation, and Copilot AI integration.

---

## Workspace Overview

| What it is | What it's for |
|---|---|
| Active mod source | One published mod under active development (`Gamemodes/Onslaught/`), plus a third-party dependency (`Gamemodes/Dependencies/Advanced Game Settings/`) |
| Custom scenarios | Coop map scripts for Arabia, Japanese, Taiga, and Woodland maps (`Scenarios/`) |
| SCAR reference | Extracted API, constants, events, and script indexes for lookup while coding |
| Data reference docs | Public summaries of extraction models, schema notes, and data workflow guidance |
| Automation references | Documentation for validation and release workflows used in development |
| AI integration docs | Public-safe Copilot workflow notes and capability boundaries |

---

## Folder Structure

Every folder below links to its navigation entry point. The `Gamemodes/` and `Scenarios/` runtime folders cannot hold README files (AoE4 packaging constraint), so their navigation lives under `docs/gamemodes/` and `docs/scenarios/`.

| Folder | Navigation entry | Purpose |
|---|---|---|
| `Gamemodes/` | [docs/gamemodes/README.md](docs/gamemodes/README.md) | Mod source — Onslaught (CBA, our mod) and `Dependencies/` (AGS third-party dependency) |
| `Scenarios/` | [docs/scenarios/README.md](docs/scenarios/README.md) | Scenario SCAR scripts for custom coop maps |
| `docs/` | [docs/README.md](docs/README.md) | All reference and design documentation: `api_reference/`, `game_systems/`, `development_guides/`, `design_notes/`, `game_data/` |
| [`docs/game_data/`](docs/game_data/README.md) | [docs/game_data/README.md](docs/game_data/README.md) | Public data-reference docs and extraction workflow notes |
| `Temporary/` | — | Untracked scratch space — AI processing, raw extractions, debug outputs, discarded runs (gitignored) |

---

## Mods in This Workspace

| Mod | Folder | Ownership | Description |
|---|---|---|---|
| **Onslaught (CBA Custom)** | `Gamemodes/Onslaught/` | **Ours** | Full CBA game mode with auto-age, boon selection, player UI, leaver handling |
| **Advanced Game Settings** | `Gamemodes/Dependencies/Advanced Game Settings/` | Third-party dependency | Lobby option framework (population, team balance, siege limits). Included because Onslaught's scripts depend on its files — we do not own or maintain this mod. |

---

## Key Reference Files

| File | What it covers |
|---|---|
| [docs/api_reference/api/scar-api-functions.md](docs/api_reference/api/scar-api-functions.md) | 4,435 SCAR API functions across 157 categories |
| [docs/api_reference/api/constants-and-enums.md](docs/api_reference/api/constants-and-enums.md) | 700+ constants and enums with type prefixes |
| [docs/api_reference/api/game-events.md](docs/api_reference/api/game-events.md) | 175 game events (`GE_*`) with numeric IDs |
| [docs/development_guides/community/boonui-community/README.md](docs/development_guides/community/boonui-community/README.md) | End-to-end BoonUI integration guide with MP-safe mutation pattern |
| [docs/api_reference/INDEX.md](docs/api_reference/INDEX.md) | Primary API reference index and navigation hub |

---

## How to Use This Workspace

1. **Open** `AoE4-Workspace.code-workspace` in VS Code — all folders load as roots.
2. **Write mod code** in `Gamemodes/Onslaught/assets/scar/`. Do not edit `Gamemodes/Dependencies/Advanced Game Settings/` — it is a read-only third-party dependency.
3. **Look up APIs** in `docs/api_reference/api/` while coding. `.scar` files use Lua syntax highlighting.
4. **Follow workflow docs** in [docs/development_guides/README.md](docs/development_guides/README.md) for data source authority and extraction pipeline context.
5. **Review docs** at [docs/README.md](docs/README.md) for documentation boundaries, private workspace notes, and the Game Content Usage notice.

---

## File Conventions

| Convention | Pattern | Example |
|---|---|---|
| Script files | `.scar` = Lua | `cba.scar`, `cardinal.scar` |
| Function names | `Category_ActionName` | `Squad_GetHealth()`, `Player_SetResource()` |
| Constants | `UPPER_CASE` with type prefix | `RT_Food`, `GE_EntityKilled`, `CMD_Move` |
| Game event hooks | `Rule_AddGlobalEvent(fn, GE_*)` | `Rule_AddGlobalEvent(OnAgeUp, GE_PlayerAgeUp)` |
| Named callbacks only | `Rule_Add*` rejects anonymous functions | Use named globals + queue pattern for deferred calls |
