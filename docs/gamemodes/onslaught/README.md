# Onslaught — Documentation Mirror

Navigation hub for [`Gamemodes/Onslaught/`](../../../Gamemodes/Onslaught/). The mod itself is `CBA Custom v1f.aoe4mod`, a CBA-derived gamemode with extensive AGS option integration, reward trees, and a custom devmenu.

## TL;DR

Onslaught is built on the **CBA (Cuman Boyars & Arrows)** mod template plus heavy custom modules. The SCAR source lives in [`Gamemodes/Onslaught/assets/scar/`](../../../Gamemodes/Onslaught/assets/scar/) — see the **submodule table** below for navigation.

For deep references, read [MOD-INDEX.md](../MOD-INDEX.md) first, then any specific document below.

## Reference documents (in this folder)

| Document | Purpose |
|---|---|
| [onslaught-api-usage-map.md](onslaught-api-usage-map.md) | Onslaught → SCAR API cross-reference (top callers, per-namespace detail) |
| [onslaught-patterns.md](onslaught-patterns.md) | 10 canonical code patterns used throughout Onslaught |
| [onslaught-event-handler-map.md](onslaught-event-handler-map.md) | Event/rule handler catalog with registration sites |
| [onslaught-options-schema.md](onslaught-options-schema.md) | AGS option keys, types, defaults, enum groups |
| [onslaught-blueprint-audit.md](onslaught-blueprint-audit.md) | Blueprint coverage (FOUND/MISSING status) |
| [onslaught-reward-trees.md](onslaught-reward-trees.md) | Reward tree definitions and selection logic |
| [onslaught-debug-commands.md](onslaught-debug-commands.md) | Console/devmenu debug command registry |
| [onslaught-debug-reference.md](onslaught-debug-reference.md) | Debug system architecture + module reference |
| [onslaught-module-lifecycle.md](onslaught-module-lifecycle.md) | Module init/update/shutdown lifecycle ordering |
| [devmenu/INDEX.md](devmenu/INDEX.md) | DEVMENU subsystem index (routing, tables, verification) |

## SCAR source layout — `Gamemodes/Onslaught/assets/scar/`

### Subsystem folders

| Folder | Purpose |
|---|---|
| [`AGS/`](../../../Gamemodes/Onslaught/assets/scar/AGS/) | Advanced Game Settings integration |
| [`archive/`](../../../Gamemodes/Onslaught/assets/scar/archive/) | Archived/legacy source kept for reference |
| [`boonui/`](../../../Gamemodes/Onslaught/assets/scar/boonui/) | BoonUI integration layer |
| [`cba_ai/`](../../../Gamemodes/Onslaught/assets/scar/cba_ai/) | CBA AI behaviour overrides |
| [`debug/`](../../../Gamemodes/Onslaught/assets/scar/debug/) | Debug/logging modules |
| [`devmenuUI/`](../../../Gamemodes/Onslaught/assets/scar/devmenuUI/) | Custom developer menu UI — see [devmenu/INDEX.md](devmenu/INDEX.md) |
| [`gamemodes/`](../../../Gamemodes/Onslaught/assets/scar/gamemodes/) | Gamemode-specific scripts |
| [`gameplay/`](../../../Gamemodes/Onslaught/assets/scar/gameplay/) | Core gameplay rules (options, spawns, etc.) |
| [`observerui/`](../../../Gamemodes/Onslaught/assets/scar/observerui/) | Observer UI |
| [`playerui/`](../../../Gamemodes/Onslaught/assets/scar/playerui/) | Player-side UI |
| [`rewards/`](../../../Gamemodes/Onslaught/assets/scar/rewards/) | Reward tree implementation |
| [`startconditions/`](../../../Gamemodes/Onslaught/assets/scar/startconditions/) | Start condition scripts |

### Top-level entry scripts

| File | Role |
|---|---|
| `cba.scar` | CBA mod root |
| `cba_annihilation.scar` | CBA annihilation mode |
| `cba_debug.scar` | CBA debug entry |
| `cba_religious.scar` | CBA religious-victory mode |
| `myannihilation.scar` | Onslaught annihilation variant |
| `myreligious.scar` | Onslaught religious variant |
| `onslaught.scar` | Onslaught mod root |
| `onslaught_annihilation_patches.scar` | Patches over annihilation mode |
| `onslaught_religious_patches.scar` | Patches over religious mode |
| `wonder.scar` | Wonder-victory handling |

## In-mod docs (live inside the runtime tree)

- [`Gamemodes/Onslaught/docs/cba-mod-summary.md`](../../../Gamemodes/Onslaught/docs/cba-mod-summary.md)
- [`Gamemodes/Onslaught/docs/kill-event-batch-plan.md`](../../../Gamemodes/Onslaught/docs/kill-event-batch-plan.md)

## See also

- [../MOD-INDEX.md](../MOD-INDEX.md) — cross-mod quick reference
- [../../api_reference/README.md#onslaught-indexes](../../api_reference/README.md#onslaught-indexes) — onslaught function index, globals index, excluded sources
- [../../README.md#private-and-excluded-workspace-components](../../README.md#private-and-excluded-workspace-components) — consolidated notes for private skill tooling context
