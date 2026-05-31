# Onslaught PlayerUI — Architecture Overview

Custom observer/player HUD for the Onslaught gamemode. Original project code; not derived from official Relic UI systems. Source lives in `Gamemodes/Onslaught/assets/scar/playerui/`.

## Purpose

The PlayerUI provides a real-time per-player data panel showing scores, population composition, resource rates, relic positions, age-up progress, and reward state for all players in the lobby. It supports up to 8 players across two teams, with observer mode and replay compatibility.

## Two-layer timing architecture

The HUD operates on two independent timing layers:

| Layer | Interval | Responsibility |
|---|---|---|
| Data layer | 1.0 s | Read all game state; populate the internal data context; trigger animation targets |
| Animation layer | 0.1 s | Lerp displayed values toward targets; apply FLIP transitions, decay effects, score pulses; write display values to XAML data context |

The data layer drives what values are *targeted*; the animation layer drives how those values are *displayed*. The 0.1 s animation tick self-pauses when no animations are in progress and unpauses automatically when a new target is set.

## Data flow

Game state is read once per second and written into per-player slot tables in the root data context. The animation layer interpolates raw values toward display values over multiple 0.1 s ticks, providing smooth visual transitions even though underlying game data changes discretely. Final display values are pushed to XAML in batches after each animation tick.

## Ranking system

Player rank is tracked with hysteresis to prevent visual noise from rapid rank changes. Rank transitions trigger FLIP animations (position-swap animations that animate from old position to new position using CSS-style transforms in XAML). The ranking module is initialized once at startup and updated on each 1.0 s data cycle.

## Tracking modules

Six tracking modules collect specialized data per player:

- **PopulationComposition** — worker / military / siege breakdown
- **GameObjectRepository** — age tracking, landmark detection
- **OwnedSquads** — squad inventory by blueprint
- **QueuedStuff** — production queue snapshots
- **RelicLocations** — carried vs. deposited relic counts
- **AgingUpProgress** — age-up state, ETA, and progress percentage

Each tracking module is initialized as part of the lifecycle framework and updated on the 1.0 s data cycle.

## Debug system

Two diagnostic scripts (`cba_debug_playerui.scar`, `cba_debug_playerui_anim.scar`) provide a 4-phase and 6-phase diagnostic sequence respectively, covering init validation, data context verification, UI creation, ranking, animation monitoring, and stress testing. These live in a separate `debug/` directory and are not loaded in production builds.

## XAML binding model

All data is surfaced to XAML through a root `PlayerUiDataContext` table. Per-player slots are initialized with default values at startup; the data layer overwrites slot values each second; the animation layer overwrites display values each 0.1 s. XAML binds directly to display values, never to raw game-state values.

## See also

- [../gameplay/README.md](../gameplay/README.md) — gameplay framework context
- [../systems/README.md](../systems/README.md) — cross-cutting system patterns
