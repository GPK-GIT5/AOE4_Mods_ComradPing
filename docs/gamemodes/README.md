# Gamemodes — Documentation Mirror

Navigation hub for the [`Gamemodes/`](../../Gamemodes/) runtime tree.
The runtime folders cannot hold README/metadata files (AoE4 `.aoe4mod` packaging constraint), so all navigation for that subtree lives here in `docs/`.

## TL;DR

- **[Onslaught](onslaught/README.md)** — the primary CBA-derived gamemode mod (`Gamemodes/Onslaught/`)
- **[Dependencies](dependencies/README.md)** — third-party dependency notes (full upstream trees are external; vendored subset lives under `Gamemodes/Onslaught/assets/scar/AGS/`)
- **[MOD-INDEX.md](MOD-INDEX.md)** — cross-mod quick reference (Onslaught-heavy; Japan + Arabia sections)

## Layout mirror

| Runtime folder | Documentation entry point |
|---|---|
| `Gamemodes/Onslaught/` | [onslaught/README.md](onslaught/README.md) |
| External AGS upstream + vendored subset in `Gamemodes/Onslaught/assets/scar/AGS/` | [dependencies/advanced-game-settings/README.md](dependencies/advanced-game-settings/README.md) |

## In-mod docs (Rule-9 compliant `docs/` subfolders inside each mod)

These live inside the runtime tree and are linked from the mirror READMEs:

- [`Gamemodes/Onslaught/docs/cba-mod-summary.md`](../../Gamemodes/Onslaught/docs/cba-mod-summary.md)
- [`Gamemodes/Onslaught/docs/kill-event-batch-plan.md`](../../Gamemodes/Onslaught/docs/kill-event-batch-plan.md)

## See also

- [docs/README.md](../README.md) — top-level docs navigation
- [docs/scenarios/README.md](../scenarios/README.md) — coop scenario mirror
- [docs/game_systems/](../game_systems/) — engine/system-level references (not mod-specific)
