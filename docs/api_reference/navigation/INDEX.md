# Reference Directory Index

> **Older copy.** Canonical version: [../INDEX.md](../INDEX.md).

> Quick navigation for all 28+ reference files. Organized by workflow and data type.

**Last Updated:** February 23, 2026 | **Coverage:** 8,989 functions, 14,158 globals, 3,214 groups

---

## 🔧 Scripting & API Reference

| File | Purpose | Type | Use Case | Depth |
|------|---------|------|----------|-------|
| [scar-api-functions.md](../api/scar-api-functions.md) | All 4,435 SCAR functions organized by category (Squad_, Entity_, Player_, UI_, AI_, etc.) | Markdown | Find function signatures, understand API namespaces | Deep Dive |
| [commands-reference.md](../api/commands-reference.md) | Entity, Squad, and Player command type constants with descriptions | Markdown | Look up CMD_* constant values and meanings | Quick Ref |
| [constants-and-enums.md](../api/constants-and-enums.md) | 700+ typed constants and enums (Resource Types, Player States, etc.) | Markdown | Find constant/enum definitions and numeric IDs | Quick Ref |
| [game-events.md](../api/game-events.md) | 175 game events (GE_*) with usage patterns and context data | Markdown | Hook game events with `Rule_AddGlobalEvent()` | Deep Dive |

---

## 📊 Data & Code Analysis (CSV + Markdown)

| File | Purpose | Type | Use Case | Depth |
|------|---------|------|----------|-------|
| [function-index.md](../indexes/function-index.md) | All 8,989 functions indexed by source file (campaign + gameplay) | Markdown | Browse functions by script file and campaign | Deep Dive |
| [function-index.csv](../indexes/function-index.csv) | Machine-readable function index (function name, params, visibility) | CSV | Parse/filter functions programmatically | Deep Dive |
| [globals-index.csv](../indexes/globals-index.csv) | 14,158 global variable assignments with line numbers and values | CSV | Find where globals are declared, track variable flow | Deep Dive |
| [groups-index.csv](../indexes/groups-index.csv) | 3,214 SGroup/EGroup declarations (squad vs. entity groups) | CSV | Locate group creation patterns across scripts | Deep Dive |
| [imports-index.csv](../indexes/imports-index.csv) | 1,283 import statements (modules and dependencies) | CSV | Understand module dependencies, trace imports | Quick Ref |
| [objectives-index.csv](../indexes/objectives-index.csv) | 835 unique OBJ_/SOBJ_ constants with definition/usage locations | CSV | Find objective definitions and usages | Quick Ref |

### CSV Schema Legend

| File | Columns | Notes |
|------|---------|-------|
| [function-index.csv](../indexes/function-index.csv) | Category, File, FileName, Function, Params, Line, Visibility, FileRole | Find functions by name, signature, and script role |
| [globals-index.csv](../indexes/globals-index.csv) | Category, File, Variable, Line, Value | Track global declarations with assignment values |
| [groups-index.csv](../indexes/groups-index.csv) | Category, File, GroupType, GroupName, Line | Locate SGroup/EGroup creation patterns |
| [imports-index.csv](../indexes/imports-index.csv) | Category, File, Import, Line | Map module dependencies and includes |
| [objectives-index.csv](../indexes/objectives-index.csv) | Category, File, Objective, Context, Line | Find objective definitions vs. usages |

---

## 🗺️ Indexes & Navigation

| File | Purpose | Type | Use Case | Depth |
|------|---------|------|----------|-------|
| [master-index.md](master-index.md) | Central hub with 65 campaign summaries, 11 gameplay systems, 6 indexes | Markdown | Start here for guided navigation | Quick Ref |
| [data-index.md](data-index.md) | SCAR dependency summary: imports, objectives, groups, globals (auto-generated Feb 23, 2026) | Markdown | High-level overview of codebase metrics | Quick Ref |
| [aoe4world-data-index.md](aoe4world-data-index.md) | Cross-reference guide for game data (units, buildings, technologies, civilizations in `game_data/extracted/aoe4/data/` folder) | Markdown | Navigate structured game balance data | Quick Ref |

---

## 🔄 Extraction & Automation

| File | Purpose | Type | Use Case | Depth |
|------|---------|------|----------|-------|
| [extraction-workflow.md](../workflows/extraction-workflow.md) | Complete pipeline: 532 .scar files → organized reference material (4 phases) | Markdown | Understand how reference data is generated | Deep Dive |
| [deterministic-workflow-guidelines.md](../workflows/deterministic-workflow-guidelines.md) | System consolidation prompt for Copilot (reads Phase 3 summaries, generates final indexes) | Markdown | Re-run extraction pipeline with AI assistance | Deep Dive |
| [../.github/copilot-instructions.md](../../.github/copilot-instructions.md) | Repo-specific Copilot usage, skill link, and Phase 4 constraints | Markdown | Align Copilot usage with workspace rules | Quick Ref |

---

## 📁 Advanced: Subdirectories

| Folder | Contents | Use Case |
|--------|----------|----------|
| [blueprints/](../blueprints/) | Campaign scenario blueprints (65 files) | Understand scenario structure and layout |
| [campaigns/](../campaigns/) | Campaign-level documentation summaries | Reference campaign-specific systems |
| [gameplay/](../gameplay/) | Gameplay system indexes (AI, armies, objectives, win conditions) | Deep dive into game mode logic |
| [systems/](../systems/) | System-level consolidation (Cardinal, MissionOMatic, etc.) | Architecture and cross-system patterns |
| [scar_dump/](../../game_data/extracted/aoe4/scar_dump/) | Raw extraction outputs (Lua, CSV, JSON interim) | Data source verification and debugging |
| [ui/](../ui/) | PlayerUI architecture, field discovery, and quick reference docs | XamlPresenter HUD panels, SetPlayerDataContext bindings |
| [audits/](../audits/) | Reference folder audit reports | Track structural issues and validation history |
| [ai_sessions/](../ai_sessions/) | AI session summaries (changes, patterns, gaps per session) | Review past session outcomes and decisions |
| [workspace/](../workspace/) | Workspace maintenance docs (audit logs, reorg prompts, optimization plans) | Repo hygiene and reorganization history |

---

## ✨ Quick Start by Task

### "I need to call SCAR functions"
→ Start: [scar-api-functions.md](../api/scar-api-functions.md) | Then: [commands-reference.md](../api/commands-reference.md)

### "I need to hook game events"
→ Start: [game-events.md](../api/game-events.md) | Reference: [constants-and-enums.md](../api/constants-and-enums.md)

### "I need to find where a variable is used"
→ Start: [globals-index.csv](../indexes/globals-index.csv) | Context: [function-index.md](../indexes/function-index.md)

### "I need to understand campaign structure"
→ Start: [master-index.md](master-index.md) | Then: [blueprints/](../blueprints/) or [campaigns/](../campaigns/)

### "I need to understand dependencies"
→ Start: [imports-index.csv](../indexes/imports-index.csv) | Context: [data-index.md](data-index.md) | Deep: [extraction-workflow.md](../workflows/extraction-workflow.md)

### "I need game balance data"
→ Start: [aoe4world-data-index.md](aoe4world-data-index.md) | Then: navigate `../../game_data/extracted/aoe4/data/` subfolder

---

## 🎯 Mod-Specific Resources

**Rule:** Always use the reference copy (`docs/gamemodes/MOD-INDEX.md`) for Copilot lookups. Never read `Scenarios/Japan/MOD-INDEX.md` directly (Scenarios Folder Scope restriction).

For mod development in `Scenarios/Japan/`, use these reference documents instead of reading files directly in the scenario folder:

| Document | Primary Use | Content |
|----------|------------|----------|
| [mods/MOD-INDEX.md](../mods/MOD-INDEX.md) | **Start here for Japan scenario work** | File structure, DLC civs, restriction profiles, data tables |
| [mods/japan_reference/japan-archive-refactor-log.md](../mods/japan_reference/japan-archive-refactor-log.md) | Refactor log | Track design decisions and refactor history |
| [mods/japan_reference/japan-guide-api-reference.md](../mods/japan_reference/japan-guide-api-reference.md) | API reference | Helper functions, resolver functions, restriction table signatures |
| [mods/japan_reference/japan-checkpoint-index.md](../mods/japan_reference/japan-checkpoint-index.md) | Navigation hub | Links to all Stage 1-4 documentation |
| [mods/japan_reference/japan-stage4-restriction.md](../mods/japan_reference/japan-stage4-restriction.md) | Restriction deep-dive | Complete audit of all 22 restriction points + how to add new ones |
| [mods/japan_reference/japan-stage1-summary.md](../mods/japan_reference/japan-stage1-summary.md) | Stage 1 reference | DLC civ resolver, composition maps, AGS wrapper architecture |
| [mods/japan_reference/japan-stage2-summary.md](../mods/japan_reference/japan-stage2-summary.md) | Stage 2 reference | Helper functions, data-driven restrictions, regression audit |

---

## 📈 Statistics

- **Total functions indexed**: 8,989
- **SCAR API functions**: 4,435
- **Global variables**: 14,158
- **Squad/Entity groups**: 3,214
- **Unique objectives**: 835
- **Module imports**: 453 distinct modules
- **Campaign scenarios**: 394 files
- **Gameplay scripts**: 138 files
- **Last updated**: February 23, 2026

