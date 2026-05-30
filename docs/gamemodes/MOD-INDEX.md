# Japan Scenario MOD Index (Reference Copy)

This file is a reference copy for the Japan coop_4_japanese scenario.
Use this copy for Copilot lookups to avoid Scenarios/ scope restrictions.
The authoritative MOD index lives under Scenarios/Japan/ (Scenarios scope).

## Quick Start for Copilot

When working on Japan scenario .scar files:

1. Reference this file (never read `Scenarios/Japan/MOD-INDEX.md` directly per Scenarios Folder Scope)
2. Check Helper Functions section for civ checking and restrictions
3. Review Data Tables section for landmark and House of Wisdom restrictions
4. Use SCAR API Lookup section for function references
5. Debug with console commands in Stage 4 Notes

---

## Scope

- Scenario: coop_4_japanese (4-player co-op)
- Language: SCAR (Lua)
- Primary focus: restriction profiles, objectives, spawns, and data tables

## Key Files

| File | Purpose |
|------|---------|
| Scenarios/Japan/assets/scenarios/multiplayer/coop_4_japanese/coop_4_japanese.scar | Mission entry, imports, mission setup |
| Scenarios/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_data.scar | Data tables, restriction profiles, DLC resolver, validators |
| Scenarios/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_objectives.scar | Objective callbacks and phase transitions |
| Scenarios/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_spawns.scar | Spawn helpers and starting army setup |

## Workflow Constraints

**Scope:** When working on files in `Scenarios/Japan/` (the authoritative scenario code):

- **ONLY file types allowed:** `.scar` and `.md`
- **DO NOT attempt:** Editing `.json`, `.xml`, or other file types in `Scenarios/`
- **External lookups permitted:** `docs/api_reference/`, `docs/development_guides/official/`, and `game_data/` for supporting context

**Full constraints:** See [.github/copilot-instructions.md](../../.github/copilot-instructions.md) § Scenarios Folder Scope

This file is a **read-only reference copy**; the authoritative index lives at [Scenarios/Japan/MOD-INDEX.md](../../Scenarios/Japan/MOD-INDEX.md).

## Helper Functions

Civ checking (Stage 2+):
- `IsCivFamily(player_id, family)` — Family-wide checks (includes DLC variants)
- `IsCivExact(player_id, civ_name)` — Variant-specific checks (exact match only)
- `IsCivFamilyAny(player_id, families)` — Multi-family roster checks

Restriction application (Stage 2+):
- `ApplyLandmarkRestrictions(player_id, table, state)` — Landmark restrictions
- `ApplyHouseOfWisdomRestrictions(player_id, state)` — HoW Age 4 upgrades
- `ApplyRestrictionProfile(player_id, profile_name)` — Stage 4 profile application

Full API reference: See [japan-guide-api-reference.md](japan_reference/japan-guide-api-reference.md) for signatures and examples.

## Data Tables

Core restriction tables in `coop_4_japanese_data.scar`:

| Table | Purpose | Used In |
|-------|---------|----------|
| `LANDMARK_KEEP_RESTRICTIONS` | Early-game keep restrictions | `ApplyLandmarkRestrictions()` |
| `LANDMARK_AGE4_RESTRICTIONS` | Age 4 landmark restrictions | `ApplyLandmarkRestrictions()` |
| `HOUSE_OF_WISDOM_AGE4_RESTRICTIONS` | HoW Age 4 upgrade restrictions | `ApplyHouseOfWisdomRestrictions()` |
| `BALANCE_LOCKS` | Intentional permanent locks (Stage 3+) | `Validator_RestrictionParity()` |
| `CIV_CAPABILITIES` | Civ capability model (Stage 3+) | `Simulate_PlayerProgression()` |
| `Restriction_Profile` | Profile definitions (Stage 3+) | `ApplyRestrictionProfile()` |

How to add restrictions: See [japan-stage4-restriction.md](japan_reference/japan-stage4-restriction.md) section Adding New Restrictions

## Stage 4 Notes

- All restriction points flow through ApplyRestrictionProfile().
- Profile state tracked via PLAYER_RESTRICTION_STATE and PLAYER_PROFILE_APPLIED.
- Simulate_PlayerProgression is a dry-run validator (no SCAR C++ API calls).

Console validators (Stage 4):
```lua
print(Validator_RestrictionState())
-- Output: {PASS|FAIL, ...} for all 6 players

Simulate_PlayerProgression("english", 4)
-- Dry-run validator: checks civ resolution, table presence, profile chain
```

## Related References

**Governance & Constraints:**
- [.github/copilot-instructions.md](../../.github/copilot-instructions.md) — Mods Folder Scope rules, Rule Precedence, Multi-Step Workflow Best Practices

**Scenario Structure & Data:**
- [Scenarios/Japan/MOD-INDEX.md](../../Scenarios/Japan/MOD-INDEX.md) — **Authoritative** full index (function catalogs, data tables, objective system) — *Do not read directly per Scenarios Folder Scope rules*
- [docs/scenarios/coop_4_japanese/japan-guide-api-reference.md](../scenarios/coop_4_japanese/japan-guide-api-reference.md) — Complete API reference for all helper, resolver, and restriction functions
- [docs/scenarios/coop_4_japanese/japan-checkpoint-index.md](../scenarios/coop_4_japanese/japan-checkpoint-index.md) — Stage status snapshots and checksums
- [docs/scenarios/coop_4_japanese/japan-stage4-restriction.md](../scenarios/coop_4_japanese/japan-stage4-restriction.md) — Profile audit + all restriction points

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

