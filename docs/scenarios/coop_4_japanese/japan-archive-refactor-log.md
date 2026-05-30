# Japan Refactor Log

## 2026-02-25: Reinforcements_Player Consolidation

**Summary:** Replace four player-specific reinforcement functions with one data-driven function and add special-unit respawn tracking.

**Key Changes:**
- Use a single `players` config table in `Start_Setup_Players` to register reinforcement rules.
- Deploy special units into per-player `sg_unique` groups for death tracking and respawn.
- Resolve reinforcement unit types via `REINFORCE_MELEE_MAP` / `REINFORCE_RANGED_MAP` instead of per-function civ branches.
- Preserve all spawn marker names (`mkr_spawn_1`-`mkr_spawn_4`) by passing through config.

**Decisions:**
- Respawn special units on the same 5-second reinforcement interval rather than a separate timer.
- Keep Town Centers protected as-is; no dummy TC needed for Mongol Khan.

**Test Checklist:**
- Verify reinforcements trigger at <30% unit threshold.
- Verify special units respawn when dead.
- Verify civ-specific reinforcements (Malian, Rus/French cavalry, English/HRE infantry, etc.).
- Verify village capture still triggers final reinforcements.

