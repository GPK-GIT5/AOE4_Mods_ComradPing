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
| Raw game data | Lua runtime dump, blueprint data, and SCAR script dumps from the live game |
| Automation scripts | PowerShell tools for data extraction, auditing, and CI regression |
| AI integration | Copilot custom instructions, skills, and agents tuned for this codebase |

---

## Folder Structure

Every folder below links to its navigation entry point. The `Gamemodes/` and `Scenarios/` runtime folders cannot hold README files (AoE4 packaging constraint), so their navigation lives under `docs/gamemodes/` and `docs/scenarios/`.

| Folder | Navigation entry | Purpose |
|---|---|---|
| `Gamemodes/` | [docs/gamemodes/README.md](docs/gamemodes/README.md) | Mod source — Onslaught (CBA, our mod) and `Dependencies/` (AGS third-party dependency) |
| `Scenarios/` | [docs/scenarios/README.md](docs/scenarios/README.md) | Scenario SCAR scripts for custom coop maps |
| [`docs/`](docs/README.md) | [docs/README.md](docs/README.md) | All reference and design documentation: `api_reference/`, `game_systems/`, `development_guides/`, `design_notes/`, `project_overview/` |
| [`game_data/`](game_data/README.md) | [game_data/README.md](game_data/README.md) | Extracted and generated game data: `extracted/aoe4/`, `extracted/blueprints/`, `generated/canonical|derived|schema/`, `game_versions/` |
| [`research/`](research/README.md) | [research/README.md](research/README.md) | Investigations, audits, AI session notes, experiments, design assumptions |
| [`.github/`](.github/index.md) | [.github/index.md](.github/index.md) | Copilot instructions, custom agents, automation scripts (`scripts/extraction\|validation\|auditing\|regression\|build/`), CI workflows, prompt templates |
| [`.skills/`](.skills/index.md) | [.skills/index.md](.skills/index.md) | VS Code Copilot skill files (SCAR debug, data extraction, console commands, cache manager) |
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
| [docs/development_guides/community/scar-scripting-basics.md](docs/development_guides/community/scar-scripting-basics.md) | Common SCAR patterns and scripting fundamentals |
| [docs/development_guides/community/common-patterns.md](docs/development_guides/community/common-patterns.md) | Reusable code patterns extracted from official scripts |
| [.github/instructions/coding/known-issues.instructions.md](.github/instructions/coding/known-issues.instructions.md) | Known crash patterns and instability bugs (KI-* registry) |
| [docs/api_reference/navigation/INDEX.md](docs/api_reference/navigation/INDEX.md) | Full index of all 25 reference files, organized by workflow |

---

## How to Use This Workspace

1. **Open** `AoE4-Workspace.code-workspace` in VS Code — all folders load as roots.
2. **Write mod code** in `Gamemodes/Onslaught/assets/scar/`. Do not edit `Gamemodes/Dependencies/Advanced Game Settings/` — it is a read-only third-party dependency.
3. **Look up APIs** in `docs/api_reference/api/` while coding. `.scar` files use Lua syntax highlighting.
4. **Run automation** from `.github/scripts/` using PowerShell — buckets: `extraction/`, `validation/`, `auditing/`, `regression/`, `build/`.
5. **Check AI guidance** in `.github/copilot-instructions.md` before asking Copilot for help.

---

## File Conventions

| Convention | Pattern | Example |
|---|---|---|
| Script files | `.scar` = Lua | `cba.scar`, `cardinal.scar` |
| Function names | `Category_ActionName` | `Squad_GetHealth()`, `Player_SetResource()` |
| Constants | `UPPER_CASE` with type prefix | `RT_Food`, `GE_EntityKilled`, `CMD_Move` |
| Game event hooks | `Rule_AddGlobalEvent(fn, GE_*)` | `Rule_AddGlobalEvent(OnAgeUp, GE_PlayerAgeUp)` |
| Named callbacks only | `Rule_Add*` rejects anonymous functions | Use named globals + queue pattern for deferred calls |
