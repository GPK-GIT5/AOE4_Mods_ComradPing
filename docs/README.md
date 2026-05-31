# Documentation Index

Top-level entry point for all reference and design documentation in this workspace.

## TL;DR

Five active documentation trees plus two runtime-folder mirrors. Start here if you are unsure where to look.

## Documentation trees

| Tree | Purpose | Entry point |
|---|---|---|
| `api_reference/` *(private-maintained reference; retained)* | SCAR API, constants, events, and lookup indexes curated for this workspace | [api_reference/README.md](api_reference/README.md) |
| `game_systems/` | Custom project systems: Onslaught gameplay, MissionOMatic, Rogue mode, and UI architecture | [game_systems/README.md](game_systems/README.md) |
| `development_guides/` | How-to guides: community, official, third-party, workflows | [development_guides/README.md](development_guides/README.md) |
| `design_notes/` | Official AoE4 campaign pattern analysis — one summary README per campaign | [design_notes/README.md](design_notes/README.md) |
| `game_data/` | Data-reference documentation and extraction workflow notes | [game_data/README.md](game_data/README.md) |
| **`gamemodes/`** *(mirror)* | Navigation mirror for [`Gamemodes/`](../Gamemodes/) runtime tree | [gamemodes/README.md](gamemodes/README.md) |
| **`scenarios/`** *(mirror)* | Navigation mirror for [`Scenarios/`](../Scenarios/) runtime tree | [scenarios/README.md](scenarios/README.md) |

## Why mirrors?

`Gamemodes/` and `Scenarios/` are AoE4 runtime packages and cannot contain README/metadata files (structure_lint Rule 9). Their navigation lives under `docs/gamemodes/` and `docs/scenarios/` and links into the runtime tree.

## Cross-workspace navigation

- [Root README](../README.md) — workspace overview
- [api_reference/README.md](api_reference/README.md) — API reference root
- [game_data/README.md](game_data/README.md) — data-reference documentation and extraction notes

## Changelog and project history

The project change log was previously maintained under `docs/project_overview/changelog/` as an automated dual-format (JSONL + Markdown) system driven by four PowerShell scripts: `auto-changelog.ps1`, `generate-overview.ps1`, `generate-detailed-entries.ps1`, and `validate-entry.ps1`. On every VS Code startup, `.vscode/tasks.json` triggered the automation, which gated on a 24-hour interval, scanned committed and uncommitted changes, ran heuristic classification, validated entries, and appended them to scope-separated daily files under `output/mods/`, `output/system/`, and `output/workspace/`. Monthly `INDEX.md` files were regenerated each run. Dated narrative documents (audit summaries, postmortems, determinism fix records) were stored alongside as standalone markdown files. That folder and all its contents have been removed; the tooling and output history were development-cycle artifacts with no ongoing reference value.

## Historical scenario snapshots

The `docs/archive/` tree previously held development-history checkpoint and stage-summary documents for the `coop_4_japanese` scenario (stage 1–3 summaries, checkpoint manifests, and rollback guides). Those were traceability records for completed work phases and have been removed along with the archive tree. Active `coop_4_japanese` documentation remains in [scenarios/coop_4_japanese/README.md](scenarios/coop_4_japanese/README.md).

## Copilot instruction architecture

In the private workspace, Copilot uses a context-pattern instruction system split across six files, each carrying a YAML `applyTo` frontmatter field. Files activate automatically based on what is being edited:

| When editing | Instruction scope |
|---|---|
| `.scar` files | SCAR/Lua naming, API conventions, console constraints |
| `.ps1` files | PowerShell structure, validation patterns |
| Files in `Scenarios/` | File restrictions, index-first rule |
| Files in `Gamemodes/` | Gamemode-specific restrictions |
| `Scenarios/**` or `docs/gamemodes/onslaught/**` | Mod navigation, scenario indexes |
| Everything else | Master workspace guidance |

Each instruction file is kept under 4,000 characters to comply with GitHub Code Review limits. A master fallback file provides general guidance; specialized files layer on top without duplication. When editing a `.scar` file inside `Scenarios/`, both the language-level and folder-scope files activate simultaneously.

## Game Content Usage Notice

Age of Empires IV © Microsoft Corporation. This workspace was created under Microsoft's "Game Content Usage Rules" using assets from Age of Empires IV, and it is not endorsed by or affiliated with Microsoft.

Rules: [https://www.xbox.com/en-US/developers/rules](https://www.xbox.com/en-US/developers/rules)

## Private and excluded workspace components

Private workspace stubs that previously lived in separate README-only folders are consolidated here to keep navigation stable while avoiding top-level clutter.

### `.github/` (private workspace automation and AI customization)

#### Purpose

In the private workspace, `.github/` contains CI/CD workflows, Copilot agent definitions, coding instructions, and PowerShell tooling scripts.

#### Typical structure

```
.github/
├── agents/
├── data/
│   └── aoe4/
├── instructions/
│   ├── coding/
│   ├── context/
│   └── core/
├── prompts/
├── scripts/
│   ├── auditing/
│   ├── build/
│   ├── extraction/
│   ├── regression/
│   └── validation/
├── workflows/
└── copilot-instructions.md
```

#### Why excluded

Contains internal automation configuration and local snapshots of Relic IP (`data/aoe4/`) that are not appropriate for public distribution.

#### Integration points

| Consumer | Uses |
|---|---|
| VS Code Copilot | Instructions, agents, and prompts in the private workspace |
| GitHub Actions | Workflows run on the private repository |
| PowerShell tooling | Scripts invoked locally or via CI |

#### Public replacements and related docs

- [development_guides/README.md](development_guides/README.md) — data source authority and extraction pipeline context
- [api_reference/README.md](api_reference/README.md) — API lookup navigation
- [game_data/README.md](game_data/README.md) — data extraction context

### `.skills/` (private Copilot custom skills)

#### Purpose

In the private workspace, `.skills/` contains Copilot skill packages for SCAR authoring, data extraction, and MCP-driven queries.

#### Typical structure

```
.skills/
├── index.md
├── aoe4-mcp/
├── console-commands/
├── data-extraction/
├── readme-to-ai-reference/
├── scar-debug/
└── _dev/
	└── cache-manager/
```

#### Why excluded

Skills are tightly coupled to private MCP servers, private data pipelines, and workspace-specific Copilot configuration.

#### Integration points (private workspace)

| Consumer | Uses |
|---|---|
| VS Code Copilot agent mode | All `SKILL.md` files via `index.md` |
| `data-extraction` skill | Drives `game_data/` extraction pipeline |
| `aoe4-mcp` skill | Live AoE4 MCP server blueprint queries |

#### Public replacements and related docs

- [api_reference/INDEX.md](api_reference/INDEX.md) — deep API/index lookup
- [game_systems/README.md](game_systems/README.md) — system patterns and architecture
- [development_guides/README.md](development_guides/README.md) — workflow context and data pipeline overview
- [gamemodes/README.md](gamemodes/README.md) and [scenarios/README.md](scenarios/README.md) — runtime tree navigation

### `.vscode/` (private workspace editor configuration)

#### Purpose

In the private workspace, `.vscode/` stores per-workspace settings, launch configurations, and task definitions.

#### Typical contents

```
.vscode/
├── settings.json
├── launch.json
├── tasks.json
└── extensions.json
```

#### Why excluded

Configuration is developer-machine-local and intentionally not committed to this public repository.

#### Integration points

| File | Effect |
|---|---|
| `settings.json` | `.scar` treated as Lua; cache directories excluded from search |
| `tasks.json` | Surfaces private automation scripts as runnable tasks |
| `extensions.json` | Extension recommendations for AoE4 mod development |

#### Public replacements and related docs

- [development_guides/README.md](development_guides/README.md) — portable process documentation
- [README.md](../README.md) — workspace-level orientation

### `.tmp/` and `Temporary/` (workspace ephemeral folders)

#### Purpose

Scratch directories for transient pipeline outputs and in-progress staging work.

#### Typical usage

| Folder | Use |
|---|---|
| `.tmp/` | Short-lived pipeline outputs and intermediate extraction files |
| `Temporary/` | Manual staging area for in-progress experiments |

#### Why excluded

Transient working state with no persistent reference value. Both are ignored by source control.

#### Integration points

None. These folders are intentionally not referenced by published scripts, workflows, or mod source.
