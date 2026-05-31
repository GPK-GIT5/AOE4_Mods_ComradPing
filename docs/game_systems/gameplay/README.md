# Gameplay Systems — Architecture Overview

Custom project gameplay systems used across Onslaught, custom scenarios, and official AoE4 campaign patterns. This folder contains original analysis and architectural documentation only — no Relic engine API catalogs or internal identifier references.

## MissionOMatic Framework

MissionOMatic is the core mission runtime used by all official AoE4 campaign missions. It consumes a declarative recipe (a Lua table returned by `GetRecipe()`) and initializes all locations, AI behavior modules, objectives, and metrics from that single data structure.

The recipe architecture separates **what** a mission does (the recipe) from **how** the framework executes it (the engine). Key recipe fields define players, locations, behavior modules, objective conditions and actions, intro/outro NIS events, and per-mission audio settings.

The framework initializes in four ordered stages: global setup, recipe processing (modules and objectives), pre-start actions, then mission start and objective activation. All campaign-level and Onslaught mission logic sits inside this pipeline.

**Conditions** evaluate boolean game state; **Actions** execute game logic (spawn units, start objectives, trigger events); **Playbills** sequence condition→action blocks with parallel-branch support. This three-layer structure is what allows complex mission scripting to remain data-driven rather than requiring per-mission imperative code.

## AI Behavior Modules

The module system provides the building blocks for AI unit behavior in both campaign missions and custom scenarios. Five module types cover the major AI behavioral patterns:

- **TownLife** — AI economy: villager gathering, building construction, unit production via skirmish homebase
- **Defend** — Hold-position encounters with optional withdraw conditions triggered by sightlines, engagement, or health thresholds
- **Attack** — Assault-target encounters with dynamic retargeting as the mission progresses
- **RovingArmy** — Mobile patrol cycling through waypoints with six targeting modes (Discard, Cycle, Reverse, Proximity, Random, RandomMeandering)
- **UnitSpawner** — Simple on-map or off-map unit provider for scripted reinforcements

All modules share a common lifecycle (Init → Monitor → unit management → Disband → IsDefeated) and participate in the unit request/reinforcement pipeline, where combat modules signal need and provider modules respond with production.

## Army and Encounter System

The Army system manages groups of AI-controlled units at a higher abstraction level than individual units. An Army has a target sequence (attack, then defend, then complete), manages its own encounter lifecycle, handles split sub-encounter families for large groups, and fires callbacks on death, completion, or path-blocked events.

Encounter Plans (Attack, Defend, Move, TownLife, DoNothing) are registered plan types that configure the underlying AI state machine for a specific behavioral mode. The encounter framework handles phase transitions, plan registration, and AI notification routing.

WaveGenerator provides timed unit production with simulated build-time delays — infantry take ~15–22 seconds, cavalry 35 seconds, siege 30–45 seconds. It is the primary spawn mechanism for campaign AI waves.

## Rogue Mode Survival Framework

Rogue mode is a Wonder-defense survival game mode with procedurally-scheduled enemy waves. Its architecture is documented in detail in [../../design_notes/campaigns/rogue/README.md](../../design_notes/campaigns/rogue/README.md).

Key architectural components:
- **Lane system:** 2–4 named lanes with 3 sublanes each, defining physical paths from enemy spawn to Wonder
- **Combinatorial wave templates:** Auto-generated from unit type combinatorics rather than hand-authored; selected by age, lane, and resource budget
- **Event scheduler:** Time-ordered event queue drives round arrival, age-ups, lane unlocks, and roamer spawns
- **Polynomial difficulty:** A multi-coefficient polynomial equation generates 7–8 tier difficulty values for resource budgets, unit counts, and timing

## Prefab / WorldBuilder Trigger System

The prefab system provides schema-driven WorldBuilder components for placing gameplay logic directly in the map editor. Each prefab has a schema file defining editor-exposed parameters and an implementation file with `_Init`, `_Activate`, `_Trigger`, and `_Stop` lifecycle functions.

Available prefab types: CanSeeTrigger (visibility check), ExclusionArea (AI no-path zone), HealthTrigger (health threshold watcher), PlayerTrigger (proximity zone), VillagerLife (ambient villager AI with resource gathering and flee/attack responses), and MOMObjective (Mission-o-Matic objective placement). Prefabs communicate via action dispatch and an external-interest registration pattern for cross-prefab triggering.

## See also

- [../systems/README.md](../systems/README.md) — cross-cutting system indexes (waves, spawns, objectives, difficulty)
- [../ui/README.md](../ui/README.md) — Onslaught custom PlayerUI architecture
- [../../design_notes/campaigns/](../../design_notes/campaigns/) — campaign pattern analysis per folder
