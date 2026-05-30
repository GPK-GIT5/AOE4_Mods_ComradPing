# Credits and Acknowledgements

This repository — the Onslaught game mode and its companion co-op scenarios for **Age of Empires IV** — exists because of the work of many people. This document gathers all the attributions we can verify, plus general acknowledgements where specific attribution is not available.

If you are an author listed here and want your entry corrected, expanded, removed, or linked to your preferred handle/site, please open an issue.

---

## Project Maintainer

| Role | Handle | Scope |
|---|---|---|
| Mod author, maintainer, primary developer | **Comrad Ping** | Onslaught (`Gamemodes/Onslaught/`), the four co-op scenarios under `Scenarios/`, all original SCAR code (including the `cba_ai/` modular AI), all original documentation under `docs/`, and the tooling/workflows in the source workspace. |

The attribution "Edit by Comrad Ping" appears at the top of [Gamemodes/Onslaught/assets/scar/cba.scar](Gamemodes/Onslaught/assets/scar/cba.scar) and is the authoritative source for the entries below.

---

## Upstream Mods, Scripts, and Frameworks (Verified)

These authors and projects are credited directly in the Onslaught source header. Onslaught either depends on them at runtime or vendors a subset of their code for local development.

| Contributor | Project | Used for |
|---|---|---|
| **Kzoacn** | *Castle Blood Automatic* (CBA) for Age of Empires IV | The base CBA gamemode that Onslaught forks and extends.|
| **Woprock** | *Advanced Game Settings* (AGS) | Game-setting framework, win-condition plumbing, balance helpers, and several gameplay subsystems consumed by Onslaught. A subset of AGS is vendored locally under `Gamemodes/Onslaught/assets/scar/AGS/`. The full mod must be obtained separately for local builds — see [docs/gamemodes/dependencies/advanced-game-settings/README.md](docs/gamemodes/dependencies/advanced-game-settings/README.md). |
| **Tommy** | *Day & Night Cycle* | Day/night cycle behaviour integrated into Onslaught. |
| **Skirp** and **Hank** | *Automatic Population* | Used by Onslaught's automatic population module (`gameplay/ags_population_auto.scar`). |

---

## Data Sources and Reference Material (Acknowledgement)

This repository does not redistribute the data sources below, but Onslaught's development and the published documentation rely on them. They deserve acknowledgement.

| Source | Owner / Maintainer | Usage |
|---|---|---|
| **Age of Empires IV** game data, SCAR API, EBP blueprints, `cardinal.ucs` | © Microsoft / World's Edge / Relic Entertainment | Reference target for every blueprint name, upgrade ID, and engine call used by Onslaught and the scenarios. Extracted locally from the official Content Editor; not redistributed. See [docs/game_data/README.md](docs/game_data/README.md). |
| **Official AoE IV Mod Tools documentation** | © Microsoft / World's Edge | Foundational modding guidance. Verbatim copies removed from this repo; see [docs/development_guides/official/README.md](docs/development_guides/official/README.md). |
| **AoE4World data dumps** (`data.aoe4world.com`) | AoE4World community | Per-civilization JSON used as a cross-reference for canonical unit/building/upgrade data. Not redistributed; see [docs/game_data/README.md](docs/game_data/README.md). |

---

## Tools and Engines (Acknowledgement)

| Tool | Maintainer | Usage |
|---|---|---|
| **Age of Empires IV Content Editor** | Microsoft / World's Edge / Relic | Authoring, packaging, and testing of all mods and scenarios in this repository. |
| **SCAR (Scripting At Relic)** runtime | Relic Entertainment | The Lua-based scripting environment Onslaught and the scenarios run on. |
| **Essence Engine** | Relic Entertainment | The underlying game engine. |

---

## General Acknowledgements

Many things in a modding ecosystem cannot be cleanly attributed because they are folk knowledge passed around between mod authors, refined over years of community streams, Discord servers, and forum threads. In the spirit of credit-where-credit-is-due, this section acknowledges them as a group:

- The **Age of Empires IV modding community** on Discord, for shared SCAR patterns, debugging tips, blueprint sleuthing, and reverse-engineering work that informs almost every gameplay system in this repo.
- All **mod authors** whose published SCAR files served as practical examples of how to use specific engine functions and patterns that are otherwise sparsely documented.
- The **AoE4World** maintainers and contributors for keeping a high-quality, public dataset alive.
- The **streamers, content creators, and balance analysts** who provide the play-testing observations that shape Onslaught's balance.
- **Bug reporters and play-testers** who have contributed feedback on Onslaught and the scenarios.

If you contributed something specific that should be moved out of this general acknowledgement and into the Verified section above, please open an issue with the file/feature it applies to and your preferred attribution.

---

## License and Redistribution Boundary

- Original SCAR, documentation, scenarios, and tooling authored for this project are © Comrad Ping. See the repository's `LICENSE` file (if present) for terms.
- Vendored or derivative third-party code retains the rights of its original authors. The Verified section above is the canonical attribution list for those works.
- Game-owned data (SCAR engine API, EBP blueprints, `cardinal.ucs`, official modding docs) belongs to Microsoft / World's Edge / Relic Entertainment and is not redistributed here.
- The AoE4World JSON dataset is provided under the terms set by AoE4World; see their site for details.
