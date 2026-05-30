# Onslaught SCAR Archive

The `Gamemodes/Onslaught/assets/scar/archive/` folder from the private workspace is not present in this public repository.

## Purpose

In the private workspace, `archive/` holds superseded legacy SCAR files retained for historical reference. Nothing in it is imported by any active entry point.

## Contents (private workspace)

| File / folder | Origin | Superseded by |
|---|---|---|
| `cba_debug_monolith.scar.bak` | Pre-modularisation CBA AI monolith | [`cba_ai/`](../../../../Gamemodes/Onslaught/assets/scar/cba_ai/) module chain |
| `day night cycle.scar` | Tommy's Day & Night Cycle (third-party copy) | Current day/night integration |
| `rewards.scar` | Legacy reward system | Active `gameplay/` and `rewards/` subtrees |
| `debug/`, `gameplay/` | Legacy helper stubs | Current `devmenuUI/` and active gameplay tree |

## Why excluded

No file in `archive/` is imported by the current active codebase. Publishing them alongside the active source would create confusion about what code is actually running.

## Integration points

None.
