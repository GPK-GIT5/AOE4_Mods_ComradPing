# Onslaught Debug Reference

> **Canonical spec:** `.github/instructions/core/debugger-architecture.instructions.md`
>
> The full module table, namespace hierarchy, branch naming, state tables, and known audit findings are defined there.
> This file retains the quick-start guide, command reference, scenario stages, and related references below.

---

## Quick Start

The debug system has two paths: **structured** (tag-based, safe-by-default) and **expert** (direct global calls).

### Structured Path — `debug.run(tag)`

```lua
debug.run("smoke")       -- Quick 7-test smoke check
debug.run("siege")       -- Full siege pipeline (~60s)
debug.run("playerui")    -- Full PlayerUI diagnostics + animation
debug.run("data")        -- Blueprint audit + civ overview + data extraction
debug.run("players")     -- Full player system validation (safety-gated)
debug.run("all")         -- Run all master suites (case-insensitive)
```

### Discovery

```lua
debug.list()             -- Show all 22 tags with tier and description
debug.list("siege")      -- Filter tags by substring
debug.status()           -- Show sub-tables and function counts
```

### Subsystem Runners

| Runner | Suites Chained | Pattern |
|--------|---------------|---------|
| `debug.playerUI.run()` | Init/Data/UI/Ranking → Animation | Async sub-orchestrator |
| `debug.siege.run()` | Quick → Field → Pending → Workshop | Async sub-orchestrator |
| `debug.data.run()` | Blueprint Audit → Civ Overview → Data Summary | Sync sequential |
| `debug.players.run(idx)` | Full system validation (safety-gated) | Delegated async |

### Safety

```lua
debug._safety.include_human()        -- Unlock human player as target
debug._safety.exclude_human_reset()  -- Re-enable protection (default)
```

### Limitations

- Only one sub-orchestrator (`debug.*.run()`) can be active at a time.
- Async callback crashes (inside `Rule_AddOneShot`) stall the sub-orchestrator. Setup-phase crashes auto-recover.

---

## Command Reference

### Quick Diagnostics

```lua
debug.run("smoke")                     -- Preferred: tag dispatch
Debug_RunSmokeTests()                  -- 7-test smoke check
Debug_SetBaseline(500)             -- Set all resources to N
Debug_GetPopCap(1)                 -- Pop/cap/max for player
Debug_GetKillScore(1)              -- Kills and next reward requirement
Debug_KeepDiagnostic()             -- All keep HP/alive status
Debug_PrecacheStatus()             -- AGS_ENTITY_TABLE castle BP check
Debug_Spawn("unit_name", 1, 3)    -- Spawn N units at player's keep
```

### Read-Only Inspectors

```lua
Debug_GetBuildingLimitState()      -- Per-player building counts vs limits
Debug_GetSiegeLimitState()         -- Per-player siege counts vs limits
Debug_GetKeepOwnershipMap()        -- Keep alive/owner for all players
Debug_GetVillagerState()           -- Villager count per player
Debug_GetOptionParseResults()      -- Parsed AGS_GLOBAL_SETTINGS
Debug_GetPostDefeatState()         -- Per-player eliminated/entity count
Debug_GetReligiousState()          -- Sacred site progress
Debug_GetWonderState()             -- Wonder timer state
Debug_GetAutoAgeState()            -- Auto-age module state
Debug_RamSiegeTowerLimitState()    -- Ram/siege tower detailed state
Debug_GetStarterKeepState()        -- English starter keep tracking
Debug_GetLeaverBalanceState()      -- Team balance after disconnects
```

### Validation Suites

```lua
debug.run("validation")                -- Preferred: 6-phase validation via tag
debug.run("stress")                    -- 8-stage stress via tag
debug.run("coverage")                  -- 10-batch API coverage via tag
debug.run("siege")                     -- Full siege pipeline via tag (~60s)
debug.run("playerui")                  -- Full PlayerUI diagnostics via tag
debug.run("data")                      -- Data pipeline via tag
debug.run("players")                   -- Player system validation via tag (safety-gated)
Debug_FullValidation()                 -- 6-phase validation (~12s)
Debug_LimitEnforcementValidator()  -- Phase 5 (Limits) only
Debug_StressTest()                 -- 8-stage stress test (~25s)
Debug_SiegeLimitStressTest()       -- Dedicated siege/ram/tower stress test
Debug_StressStage(3)               -- Individual stress stage (1-8)
Debug_CoverageTest()               -- 10-batch API coverage (~40s)
Debug_CoverageBatch(5)             -- Individual coverage batch (1-10)
Debug_EventProbes()                -- Mock-context handler resilience
Debug_Scenario()                   -- Full 7-stage orchestrated run
Debug_ScenarioStatus()             -- Check scenario progress
Debug_ScenarioStop()               -- Abort running scenario
```

### Destructive (safety-gated on structured path)

```lua
debug.run("destructive")               -- Prints command reference (no execution)
debug.players.forceKeepDestroy(idx)    -- Kill player's keep (safety-gated)
debug.players.forceEliminate(idx)      -- Trigger elimination path (safety-gated)
debug.players.forceSurrender(idx)      -- Trigger surrender path (safety-gated)
debug.players.forceTransfer(src, dst)  -- Transfer buildings src→dst (safety-gated)
debug.players.validateAnchors()        -- Check spawn positions (read-only)
-- Expert path (no safety gate):
Debug_ForceKeepDestroy(1)              -- Kill player's keep
Debug_ForceEliminatePlayer(2)          -- Trigger elimination path
Debug_ForceSurrender(1)                -- Trigger surrender path
Debug_ForceTransferTest(1, 2)          -- Transfer buildings src→dst
Debug_ValidateSpawnAnchors()           -- Check spawn positions
```

### Limits UI

```lua
Debug_GetLimitsUIState()           -- Building/siege limit summary
Debug_ConstructionTrace(1)         -- Entity type breakdown for player
Debug_LimitsUIStress()             -- Counter consistency (desync detection)
```

### Leaver

```lua
debug.run("leaver")                    -- Preferred: leaver pipeline via tag
debug.run("players")                   -- Full player system validation via tag
debug.players.forceDisconnect(idx)     -- Simulate disconnect (safety-gated)
debug.players.forceAnnihilation(idx)   -- Kill all entities/squads (safety-gated)
-- Expert path:
Debug_ForceDisconnect(1)               -- Simulate player disconnect
Debug_ForceAnnihilation(1)             -- Kill all player entities/squads
```

### Logging

```lua
DebugLog("area", "msg")            -- Filtered structured log
DebugLog_SetFilter("stress", "coverage")  -- Show only matching areas
DebugLog_SetFilter()               -- Clear filter (show all)
```

---

## Known Audit Findings

### 1. Building-Limit Counter Desync After Ownership Transfer

`Entity_SetPlayerOwner` does not fire construction events, so `obj_buildingLimit_count`,
`obj_buildingLimit_workshop_count`, and `siegeLimit_count` desync for the recipient.
**Fix:** Call `CBA_Options_BuildingLimit_RecountPlayer` + `CBA_Options_SiegeLimit_Recount/ApplyThreshold` after transfer.

### 2. English Keeps Dual-Classified in Production Counting

English keep entities have both `military_only_production` and `military_production_building` classes.
Startup reconciliation in `cba_options.scar` counts them unless skipped before incrementing.

### 3. Player_SetMaximumAge Cannot Uncap

`Player_SetMaximumAge` returns early when `maximumAge >= 4` (Imperial). Calling it to "remove"
a previously applied cap does not re-enable age menus/upgrades. Reliable uncapping requires
`Player_SetConstructionMenuAvailability` and/or `Player_SetUpgradeAvailability`.

### 4. Siege-Limit Disable Uses Multi-Step Cascade

`SiegeLimit_Disable` (cba.scar) has 4 tiers of civ-specific EGroup filter and production checks.
Chinese/Abbasid variants are intentionally separate because they have different siege BPs.

---

## Scenario Stages

`Debug_Scenario()` runs 7 stages with 5s gaps between each:

| Stage | Suite | Description |
|-------|-------|-------------|
| 1 | FullValidation | 6-phase validation |
| 2 | StressTest | 8-stage stress across 16 civs |
| 3 | CoverageTest | 10-batch API coverage |
| 4 | EventProbes | Mock-context handler resilience |
| 5 | AuditFindings | All 4 known audit finding reproductions |
| 6 | AIDataExport | AGS_GLOBAL_SETTINGS dump |
| 7 | FinalSummary | Pass/fail summary log |

---

## Related References

| Resource | Path |
|----------|------|
| SCAR debug skill | `.skills/scar-debug/SKILL.md` |
| Game events API | `docs/api_reference/api/game-events.md` |
| SCAR API functions | `docs/api_reference/api/scar-api-functions.md` |
| Constants & enums | `docs/api_reference/api/constants-and-enums.md` |
| Blueprint data | `game_data/extracted/blueprints/` |
| SCAR coding rules | `.github/instructions/coding/scar-coding.instructions.md` |
| XAML/UI rules | `.github/instructions/coding/xaml-ui.instructions.md` |
- [.github/copilot-instructions.md](../../.github/copilot-instructions.md) — Mods Folder Scope rules, Rule Precedence, Multi-Step Workflow Best Practices

**Scenario Structure & Data:**
- [Scenarios/Japan/MOD-INDEX.md](../../Scenarios/Japan/MOD-INDEX.md) — **Authoritative** full index (function catalogs, data tables, objective system) — *Do not read directly per Scenarios Folder Scope rules*
- [docs/scenarios/coop_4_japanese/japan-guide-api-reference.md](../../scenarios/coop_4_japanese/japan-guide-api-reference.md) — Complete API reference for all helper, resolver, and restriction functions
- [docs/scenarios/coop_4_japanese/japan-checkpoint-index.md](../../scenarios/coop_4_japanese/japan-checkpoint-index.md) — Stage status snapshots and checksums
- [docs/scenarios/coop_4_japanese/japan-stage4-restriction.md](../../scenarios/coop_4_japanese/japan-stage4-restriction.md) — Profile audit + all restriction points

**SCAR API Lookup (when editing scenario .scar files):**
- [docs/api_reference/api/scar-api-functions.md](../api/scar-api-functions.md) — SCAR functions by namespace
- [docs/api_reference/indexes/function-index.md](../indexes/function-index.md) — Functions indexed by source file
- [docs/api_reference/api/constants-and-enums.md](../api/constants-and-enums.md) — Constants, enums, objective IDs (OBJ_*, SOBJ_*)
- [docs/api_reference/api/game-events.md](../api/game-events.md) — Game event hooks (GE_*)
- [.skills/_dev/cache-manager/SKILL-GUIDE.md](../.skill/SKILL-GUIDE.md) — Blueprint resolution (attribName ↔ pbgid)

## External References (Permitted Lookups)

When working on `.scar` files in `Scenarios/Japan/`, these external folders are accessible:

| Folder | Access | Primary Use |
|--------|--------|-------------|
| `docs/api_reference/` | ✅ Read-only | API docs, function indexes, constants |
| `docs/development_guides/official/` | ✅ Read-only | Editor workflows, modding patterns |
| `game_data/extracted/aoe4/data/` | ✅ Read-only | Game balance data, unit/building stats |
| `Scenarios/Japan/` | ✅ Author | Edit `.scar` and `.md` only |

## Update Guidance

When `Scenarios/Japan/` scenario files change, regenerate this reference copy:

1. **Verify scope:** Changes only to `.scar` or `.md` files?
   (JSON changes → no update needed for MOD-INDEX)
2. **Update line counts & hashes:** Extract from modified `.scar` files; regenerate checksums
3. **Cross-reference authoritative index:** Compare against [Scenarios/Japan/MOD-INDEX.md](../../Scenarios/Japan/MOD-INDEX.md) — if mismatch, run full regeneration
4. **Commit separately:** Sync reference copy only when final state is verified

**Last Updated:** 2026-02-26

