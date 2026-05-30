# Data Sync Workflow

How to keep `game_data/extracted/aoe4/` synchronized with AoE4 game patches and DLC releases.

## Source authority

| Tier | Source | Role | Win on conflict? |
|---|---|---|---|
| 1 truth | EBP XML dump (`Gameplay_data_duplicate/.../ebps/races/`) + `game_data/extracted/aoe4/scar_dump/` | Game-file ground truth | ✅ Always |
| 2 cache | `https://data.aoe4world.com/` JSON | Convenience layer; mirrored under `game_data/extracted/aoe4/data/{units,buildings,technologies}/*-optimized.json` | Only when Tier 1 unavailable |
| 3 UI | `https://aoe4world.com/` | "Something changed" signal | No (advisory) |
| 4 advisory | aoe4labs, support.ageofempires, fandom | Formulas, patch notes, narrative tooltips | No (advisory) |

## Tooling map

| Script | Role |
|---|---|
| [.github/.github/scripts/build/_stats/fetch_aoe4world.ps1](../../.github/.github/scripts/build/_stats/fetch_aoe4world.ps1) | Pull Tier-2 cache → `Temporary/raw_extractions/staging/aoe4world/` |
| [.github/.github/scripts/build/_stats/check_patch_signal.ps1](../../.github/.github/scripts/build/_stats/check_patch_signal.ps1) | Detect new patches via support.ageofempires.com |
| [.github/.github/scripts/build/_stats/diff_data_sources.ps1](../../.github/.github/scripts/build/_stats/diff_data_sources.ps1) | Cache freshness: workspace cache vs live aoe4world |
| [.github/.github/scripts/build/_stats/verify_canonical_vs_cache.ps1](../../.github/.github/scripts/build/_stats/verify_canonical_vs_cache.ps1) | Tier-1 vs Tier-2 consistency (hp + costs today; weapons once EBP stat extract exists) |
| [.github/scripts/extraction/generate_all_data.ps1](../../.github/scripts/extraction/generate_all_data.ps1) | Re-extract canonical from local EBP XML dump (manual EBP refresh prerequisite) |
| [.github/.github/scripts/build/_stats/sync_all.ps1](../../.github/.github/scripts/build/_stats/sync_all.ps1) | One-command wrapper |
| [game_data/generated/schema/SCHEMA_VERSION.md](../../game_data/generated/schema/SCHEMA_VERSION.md) | Pinned schema; bump procedure |
| [.github/scripts/auditing/diff_ignore.psd1](../../.github/scripts/auditing/diff_ignore.psd1) | Ignore list + numeric tolerance |

## Standard workflow (post-patch)

1. **Notice / detect a patch.**
   - Automatic signal: `pwsh .github/.github/scripts/build/_stats/check_patch_signal.ps1` (exit code `10` = new patch detected). Schedule weekly or run on demand.
   - Manual signal: aoe4world.com homepage banner, AoE4 client launcher.

2. **Wait 24–72h.** aoe4world typically lags game patches by 1–3 days while Robert van Hoesel re-runs his parser.

3. **Re-export game files** (manual; requires the AoE4 client). Per [game_data/extracted/aoe4/EXTRACTION_PLAN.md](../../game_data/extracted/aoe4/EXTRACTION_PLAN.md):
   - Use `AOEMods.Essence` to unpack `Attrib.sga` from your installed game folder.
   - Replace contents of `C:\Users\Jordan\Documents\Gameplay_data_duplicate\assets\attrib\instances\ebps\races\` with the new export.

4. **Refresh canonical from new EBP dump:**
   ```pwsh
   cd c:\Users\Jordan\Documents\AoE4-Workspace
   pwsh .github\.github\scripts\extraction\generate_all_data.ps1
   ```

5. **Run the sync wrapper:**
   ```pwsh
   pwsh .github\.github\scripts\build\_stats\sync_all.ps1
   ```
   This pulls the fresh aoe4world cache, runs both diffs, and archives `drift-report.md` to `docs/project_overview/changelog/<today>_data-drift.md`.

6. **Review reports:**
   - `game_data/generated/derived/drift-report.md` — fields that changed in aoe4world since the last fetch.
   - `game_data/generated/derived/canonical-vs-cache-report.md` — fields where game files (Tier 1) disagree with aoe4world (Tier 2).
   - `Temporary/raw_extractions/staging/patch-state.json` — last-seen patch ID.

7. **Triage each finding** into one of:
   - `STALE-CACHE` — wait, no action.
   - `EXTRACTOR-BUG` — fix the relevant `extract_*.ps1` or `verify_*.ps1`.
   - `WIKI-WRONG` — ignore.
   - `NEW-DLC-ENTITY` — re-run `generate_all_data.ps1` (already covered by step 4).
   - `FORMULA-DRIFT` — escalate to balance/formula effort.
   - `CONVENTION-DIFF` — document in `diff_ignore.psd1` if it's a known per-civ modifier (e.g., Golden Horde double-squad time).

8. **Promote staging → workspace cache.** When the cache-freshness diff is clean and nothing else is suspect, copy the staging files over the workspace cache:
   ```pwsh
   Copy-Item -Recurse -Force Temporary\raw_extractions\staging\aoe4world\units\*       game_data\extracted\aoe4\data\units\
   Copy-Item -Recurse -Force Temporary\raw_extractions\staging\aoe4world\buildings\*   game_data\extracted\aoe4\data\buildings\
   Copy-Item -Recurse -Force Temporary\raw_extractions\staging\aoe4world\technologies\* game_data\extracted\aoe4\data\technologies\
   ```

9. **Commit** the refreshed `game_data/extracted/aoe4/data/**`, the updated derived reports, the dated changelog drift entry, and any `diff_ignore.psd1` additions.

## Schema-bump handling

If `__version__` in any fetched file differs from `game_data/generated/schema/SCHEMA_VERSION.md`:

1. The differ raises a `SCHEMA_BUMP` warning at the top of `drift-report.md`.
2. Inspect 1–2 fresh per-civ files in `Temporary/raw_extractions/staging/aoe4world/`.
3. Compare top-level + `data[*]` field names against the previous schema.
4. Update `.github/scripts/auditing/diff_ignore.psd1` if new structural fields appear (e.g., new icon URLs).
5. Bump the value in `SCHEMA_VERSION.md` with the new date.
6. Re-run `.github\.github\scripts\build\_stats\sync_all.ps1` to confirm clean diff under the new schema.

## DLC-release workflow

A new civ DLC is the same workflow, with two extras:

1. **Update the civ list** in `.github/.github/scripts/build/_stats/fetch_aoe4world.ps1` and `.github/.github/scripts/build/_stats/diff_data_sources.ps1` and `.github/.github/scripts/build/_stats/verify_canonical_vs_cache.ps1`. Each holds an explicit 22-civ array.
2. **Update the abbr→slug map** in `verify_canonical_vs_cache.ps1` (the `switch` near the top).
3. The first `sync_all.ps1` after the DLC will show many `MISSING_LOCAL` entries (new entities pulled in from aoe4world); these become real once `generate_all_data.ps1` re-extracts the new EBP dump.

## Cross-source manual spot-check (when needed)

Use this when a `WORTH-MANUAL-CHECK` finding appears or when validating a balance hypothesis:

1. Open `https://aoe4world.com/civilizations/<slug>/units/<unit>` — read the public unit page.
2. Open `https://aoe4labs.com/` combat simulator — verify damage/EHP under standard attackers.
3. If still ambiguous, search `game_data/extracted/aoe4/scar_dump/scar gameplay/cardinal.scar` and `Gameplay_data_duplicate/.../ebps/races/<race>/units/<unit>.xml` for the raw value.
4. Fandom wiki only as a last resort for narrative-only fields (e.g., proximity tooltips).
5. Record any cross-check findings under `research/investigations/audits/source-cross-check-<date>.md`.

## Known limitations (today)

- `verify_canonical_vs_cache.ps1` only checks `hp` and `costs.*` because today's canonical doesn't yet contain damage / armor / range. Building `.github/scripts/stats/extract_ebp_stats.ps1` (per EXTRACTION_PLAN Priority 2) unlocks weapon-level verification.
- `verify_canonical_vs_cache.ps1` resolves variation IDs by `{baseId}-{age}`. Siege, naval, and economy units use other naming conventions and currently report as `MISSING_LIVE`. Fix is enumerating `entity.variations[*].id` instead of synthesizing.
- `check_patch_signal.ps1` parses HTML; if support.ageofempires.com restructures their landing page, regex patterns may need an update.
