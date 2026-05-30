# AoE4 SCAR Reference Extraction Workflow

## Overview

Pipeline for converting 532 .scar files (394 campaign + 138 gameplay, ~9.3 MB) into organized, searchable reference material.

---

## Phase 1: Automated Extraction (No LLM — Run Once)

**Script:** `.github/scripts/extraction/run_all_extraction.ps1`

```powershell
cd C:\Users\Jordan\Documents\AoE4-Workspace
.\.github\scripts\run_all_extraction.ps1
```

**Produces:**

| File | Contents | Records |
|------|----------|---------|
| `docs/api_reference/indexes/function-index.csv` | All function signatures with file, line, params, visibility | ~9,000 |
| `docs/api_reference/indexes/function-index.md` | Same data as readable markdown tables | ~9,000 |
| `docs/api_reference/indexes/imports-index.csv` | All `import()` statements (dependency graph) | ~1,300 |
| `docs/api_reference/indexes/objectives-index.csv` | All `OBJ_`/`SOBJ_` constants with definition/usage tracking | ~1,500 |
| `docs/api_reference/indexes/groups-index.csv` | All `SGroup_CreateIfNotFound`/`EGroup_CreateIfNotFound` calls | ~3,200 |
| `docs/api_reference/indexes/globals-index.csv` | File-scope global variable assignments | ~14,000 |
| `docs/api_reference/navigation/data-index.md` | Combined summary with objective cross-references and top imports | — |

**Re-runnable.** Safe to re-run anytime if source files change.

---

## Phase 2: Batch Generation (Automated — Included in Phase 1)

The pipeline auto-generates mission-grouped batches in `references/dumps/Claude_Batches_v2/`.

- **185 batches** covering all 532 files
- **80KB max** per batch (~20K tokens input)
- **Mission-grouped**: all files in a mission folder go together
- Each batch includes the standardized summarization prompt
- Full manifest in `Claude_Batches_v2/batch_manifest.md`

---

## Phase 3: Claude Summarization (Manual — ~185 Conversations)

### Workflow Per Batch

1. Open `Claude_Batches_v2/batch_manifest.md` to see the full list
2. Open the batch file (e.g., `Batch_1.txt`)
3. Paste its contents into a new Claude/Copilot Chat conversation
4. Save the output to `docs/design_notes/campaigns/` or `docs/game_systems/gameplay/` (see structure below)

### Output Folder Structure

```
references/
├── campaigns/
│   ├── abbasid/
│   │   ├── abb_bonus.md
│   │   ├── abb_m1_tyre.md       (merge Part 1 + Part 2 outputs)
│   │   ├── abb_m2_egypt.md
│   │   └── ...
│   ├── angevin/
│   ├── hundred/
│   ├── mongol/
│   ├── russia/
│   ├── salisbury/
│   ├── challenges/
│   └── rogue/
├── gameplay/
│   ├── core.md
│   ├── ai.md
│   ├── missionomatic.md
│   ├── gamemodes.md
│   ├── training.md
│   ├── winconditions.md
│   └── ...
```

### Naming Convention for Multi-Part Missions

When a mission has Part 1, Part 2, etc., merge the outputs into one file per mission:
- `Batch_7` (abb_m4_hattin Part 1) + `Batch_8` (Part 2) + `Batch_9` (Part 3) → `abb_m4_hattin.md`

### Tracking Progress

Use the manifest CSV to track completion:
```powershell
# Add a "Done" column to track which batches are summarized
Import-Csv "references\dumps\Claude_Batches_v2\batch_manifest.csv" |
    Select-Object *, @{N='Done'; E={$false}} |
    Export-Csv "references\dumps\Claude_Batches_v2\batch_progress.csv" -NoTypeInformation
```

---

## Phase 4: System-Level Consolidation (After Phase 3)

Once all mission summaries exist, create cross-cutting system indexes.

### 4a. System Index Files

Run one Claude conversation per system, feeding it all relevant summaries:

| System File | Input | Prompt Focus |
|-------------|-------|-------------|
| `docs/game_systems/systems/objectives-index.md` | All mission summaries | Extract every OBJ_/SOBJ_, group by mission, note shared patterns |
| `docs/game_systems/systems/difficulty-index.md` | All `_data.scar` summaries | Consolidate all Util_DifVar parameters, compare scaling across missions |
| `docs/game_systems/systems/spawns-index.md` | All mission summaries | Wave patterns, army compositions, spawn timing, reusable spawn functions |
| `docs/game_systems/systems/ai-patterns.md` | AI + encounter summaries | AI encounter plans, patrol behaviors, pursuit logic, difficulty AI tuning |
| `docs/game_systems/systems/training-index.md` | Training summaries | Goal sequences, predicates, hint patterns |
| `docs/game_systems/systems/missionomatic-modules.md` | MissionOMatic gameplay summaries | Module types, recipe patterns, location/objective wiring |

### 4b. Master Index

Create `docs/api_reference/navigation/master-index.md` linking everything:
- Campaign navigation (by campaign → mission)
- System navigation (by system type)
- Link to function-index.csv for search

---

## Phase 5: Maintenance

### When Source Files Change

```powershell
# Re-run extraction to update indexes
.\.github\scripts\run_all_extraction.ps1

# Only re-summarize affected batches (check manifest for which missions changed)
```

### Searching the Reference

```powershell
# Find which file defines a function
Import-Csv references\function-index.csv | Where-Object Function -like "*SpawnWave*"

# Find all objectives in a mission
Import-Csv reference\objectives-index.csv | Where-Object File -like "*hattin*"

# Find what imports a specific module
Import-Csv reference\imports-index.csv | Where-Object Import -like "*cardinal*"

# Find all SGroups in a mission
Import-Csv reference\groups-index.csv | Where-Object File -like "*redsea*"
```

---

## Token Budget Estimate

| Phase | Method | Token Cost | Conversations |
|-------|--------|-----------|---------------|
| 1. Extraction | PowerShell | **0** | 0 |
| 2. Batching | PowerShell | **0** | 0 |
| 3. Summarization | Claude (~2K output each) | ~600K | ~185 |
| 4. Consolidation | Claude (~3K output each) | ~50K | ~6 |
| **Total** | | **~650K tokens** | **~191** |

### Minimizing Token Usage

1. **Phase 1 eliminates ~40% of what Claude would otherwise extract** — function lists, objective IDs, and import graphs are already indexed mechanically
2. **Mission grouping** keeps related files together, avoiding redundant context in summaries
3. **The embedded prompt** tells Claude to skip trivial patterns (SGroup creation, simple getters)
4. **80KB batch limit** maximizes files per conversation while keeping within context
5. **System consolidation** is done from summaries, not raw code — 6 passes vs. re-reading 532 files
