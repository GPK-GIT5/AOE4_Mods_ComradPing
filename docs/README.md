# Documentation Index

Top-level entry point for all reference and design documentation in this workspace.

## TL;DR

Six top-level documentation trees plus two runtime-folder mirrors. Start here if you are unsure where to look.

## Documentation trees

| Tree | Purpose | Entry point |
|---|---|---|
| `api_reference/` | SCAR API, constants, events, and lookup indexes | [api_reference/README.md](api_reference/README.md) |
| `game_systems/` | Engine/system-level references (gameplay, systems, UI) | [game_systems/README.md](game_systems/README.md) |
| `development_guides/` | How-to guides: community, official, third-party, workflows | [development_guides/README.md](development_guides/README.md) |
| `design_notes/` | Architecture decisions, campaign-script summaries | [design_notes/README.md](design_notes/README.md) |
| `project_overview/` | Changelog and project-level docs | [project_overview/changelog/README.md](project_overview/changelog/README.md) |
| `archive/` | Historical/superseded docs moved out of active navigation | [archive/README.md](archive/README.md) |
| **`gamemodes/`** *(mirror)* | Navigation mirror for [`Gamemodes/`](../Gamemodes/) runtime tree | [gamemodes/README.md](gamemodes/README.md) |
| **`scenarios/`** *(mirror)* | Navigation mirror for [`Scenarios/`](../Scenarios/) runtime tree | [scenarios/README.md](scenarios/README.md) |

## Why mirrors?

`Gamemodes/` and `Scenarios/` are AoE4 runtime packages and cannot contain README/metadata files (structure_lint Rule 9). Their navigation lives under `docs/gamemodes/` and `docs/scenarios/` and links into the runtime tree.

## Cross-workspace navigation

- [Root README](../README.md) — workspace overview
- [github/README.md](github/README.md) — public summary of private GitHub/automation materials
- [skills/README.md](skills/README.md) — public summary of private Copilot skills
- [game_data/README.md](game_data/README.md) — data-reference documentation and extraction notes
