# Cross-Cutting Systems — Architecture Overview

Cross-mission system patterns extracted from Onslaught and official AoE4 campaign analysis. This folder contains original architectural documentation only — no engine API catalogs or internal identifier references.

## Module Lifecycle Pattern

All behavior modules (TownLife, Defend, Attack, RovingArmy, UnitSpawner) share a consistent lifecycle that allows the mission framework to manage them generically:

1. **Init** — Spawn units, create encounter, register in the global module table and type-specific list
2. **Monitor** — Interval rule for reinforcement checks and state transitions (intervals vary: 1 s for Defend/RovingArmy, 5 s for TownLife/Attack)
3. **Unit management** — Add/Remove squad interfaces shared across all types
4. **Disband** — Full teardown; units returned to caller or destroyed
5. **IsDefeated** — Boolean health-check used by objectives and win conditions
6. **Unit provider interface** — ProvideEstimate and Start callbacks for the reinforcement pipeline

## Wave and Spawn Pipeline

Waves flow through a two-stage pipeline: preparation (units created with simulated build-time delays) then launch (transfer to assault army or target module).

Simulated build times approximate realistic production costs without requiring actual queued production: light infantry ~15 s, medium infantry/cavalry ~22–35 s, siege ~30–45 s. This creates a natural escalation curve within a wave before the first units arrive.

The unit request pipeline handles AI reinforcements between modules: a combat module signals need via the framework, the framework solicits estimates from provider modules, and the best-fit provider begins production. This decouples AI production logic from AI combat logic.

Auto-launch modes allow waves to launch immediately after preparation completes, or after a fixed delay, reducing the need for manual wave timing in mission scripts.

## Objective Methodology

Official AoE4 campaign objectives follow consistent structural patterns:

- **Primary objectives** track the main win condition; completing all active primaries triggers victory.
- **Sub-objectives** are children of a primary; their completion feeds the parent's counter or state.
- **Information objectives** track implicit fail conditions (hero survival, building survival) — they complete on failure rather than success, immediately triggering mission failure.
- **Battle objectives** are short-duration combat tasks that unlock or reward rather than driving the win condition directly.
- **Optional/Bonus objectives** operate independently; their completion grants rewards or unlocks but does not affect the main win/lose path.

Win and lose conditions are always defined as explicit objective completions or failures — there is no implicit game-over from unit death except when an Information objective tracking that unit is active.

## Difficulty Scaling Methodology

Standard campaign missions use a four-tier system (Easy / Normal / Hard / Expert). Rogue mode uses a seven-to-eight tier system with a polynomial coefficient set.

Three mechanisms apply difficulty scaling independently:

1. **Value selection** — A scaling function picks one value from a per-difficulty array; used for timing, unit counts, resource amounts, and thresholds
2. **Wave unit filtering** — Per-unit tags remove units that do not match the current difficulty tier from wave compositions
3. **Module conditional init** — Entire behavior modules are skipped on lower difficulty tiers, reducing overall AI complexity rather than just scaling numbers

These three mechanisms can be combined: a mission may reduce unit counts (mechanism 1), strip elite units from waves (mechanism 2), and disable one flanking army entirely on Easy (mechanism 3).

## See also

- [../gameplay/README.md](../gameplay/README.md) — gameplay framework (MissionOMatic, modules, Rogue, prefabs)
- [../ui/README.md](../ui/README.md) — Onslaught custom PlayerUI
- [../../design_notes/campaigns/](../../design_notes/campaigns/) — per-campaign difficulty and spawn analysis
