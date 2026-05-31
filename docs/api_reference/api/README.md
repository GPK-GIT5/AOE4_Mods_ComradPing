# SCAR Scripting System — Overview

This folder previously contained five Relic/Microsoft engine API catalog files. Those files have been removed to comply with the [Xbox Game Content Usage Rules](https://www.xbox.com/en-US/developers/rules).

*Age of Empires IV © Microsoft Corporation. This workspace was created under Microsoft's "Game Content Usage Rules" using assets from Age of Empires IV, and it is not endorsed by or affiliated with Microsoft.*

## What was here

The five removed files covered the following areas of the AoE4 SCAR (Scripting at Relic) Lua scripting surface:

**Scripting function surface** — The callable Lua API is organized into namespaces by target object type: `Squad_*`, `Entity_*`, `SGroup_*`, `EGroup_*`, `Player_*`, `UI_*`, `World_*`, `AI_*`, `Rule_*`, `Misc_*`, `Util_*`, and others. Functions covered creation, destruction, state queries, movement commands, combat commands, ability activation, production control, resource management, diplomacy, and objective/event integration.

**Typed engine signatures** — A subset of the function surface (sourced from the official `Essence_ScarFunctions.api` scardocs) included full parameter and return-type annotations across 89 namespaces.

**Command constants** — Enumerated integer constants for entity commands (`CMD_*`), squad commands (`SCMD_*`), player commands (`PCMD_*`), and AI task types (`TASK_*`), used as arguments to command-dispatch functions.

**Game constants and enumerations** — Named constants for resource types (`RT_*`), age tiers (`AGE_*`), unit stances, diplomatic relationships, win-condition reasons, objective states, and other engine-defined enumerations.

**Game event system** — The `GE_*` event catalog, used with `Rule_AddGlobalEvent()` to hook into engine lifecycle events: entity killed/created/garrisoned, construction complete, upgrade complete, ability triggered, player resource change, game state transitions, and others.

## See also

- [../README.md](../README.md) — api_reference index
- [../indexes/README.md](../indexes/README.md) — Onslaught symbol and module indexes (original project content)
