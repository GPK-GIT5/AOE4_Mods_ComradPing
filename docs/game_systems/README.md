# Game Systems Documentation

Original architectural documentation for custom project systems. Content is scoped to Onslaught, custom scenarios, and original analysis of official AoE4 campaign patterns. No Relic engine API catalogs or internal identifier references.

## TL;DR

Three subtrees covering gameplay frameworks, cross-cutting system patterns, and the Onslaught custom UI. Mod-specific navigation lives under [../gamemodes/](../gamemodes/) and [../scenarios/](../scenarios/).

## Subtrees

| Folder | Covers |
|---|---|
| [gameplay/](gameplay/README.md) | MissionOMatic framework, AI modules, Army/Encounter system, Rogue mode, prefab/trigger system |
| [systems/](systems/README.md) | Module lifecycle pattern, wave/spawn pipeline, objective methodology, difficulty scaling |
| [ui/](ui/README.md) | Onslaught custom PlayerUI — two-layer timing architecture, XAML data flow, tracking modules |

## See also

- [../api_reference/README.md](../api_reference/README.md) — SCAR API reference
- [../design_notes/campaigns/](../design_notes/campaigns/) — per-campaign pattern analysis
- [../gamemodes/README.md](../gamemodes/README.md) — Onslaught mod navigation
- [../scenarios/README.md](../scenarios/README.md) — custom scenario navigation
