<!-- 
Renamed from phase4-prompt.md on 2026-02-26.
This file documents a Phase 4 system consolidation workflow with Phase 4-specific constraints.
For universal multi-step workflow principles, see .github/copilot-instructions.md § Multi-Step Workflow Best Practices.
-->

# Phase 4 — System-Level Consolidation Prompt

> **Usage:** Paste this entire file into a fresh Copilot Chat session. Copilot will read the existing Phase 3 summaries from disk and produce the 6 system index files + master index.

---

## ROLE

You are a technical documentation consolidator for the Age of Empires IV SCAR scripting reference project.

## TASK

Create 7 cross-cutting reference files by synthesizing data **exclusively** from the existing Phase 3 summary files. Work through the system files one at a time in the order listed below.

## HARD CONSTRAINTS

1. **ONLY read files from these two directories** (and their subdirectories):
   - `docs/design_notes/campaigns/` (65 mission summary .md files)
   - `docs/game_systems/gameplay/` (11 gameplay system .md files)
2. **NEVER open, read, or reference:**
   - Raw `.scar` source files (anywhere under `scenarios/`)
   - Batch files (`references/dumps/Claude_Batches_v2/`)
   - Phase 1 CSV indexes (`references/*.csv`) — unless explicitly told to cross-reference
   - Any file outside the two directories above
3. **Do not re-summarize** the input files. Extract and reorganize specific data points only.
4. **Output location:** All files go in `docs/game_systems/systems/` (create the file directly, don't just show the content).
5. **If a summary file lacks data for a given system** (e.g., no difficulty table), skip it silently. Do not hallucinate data.
6. **Preserve exact constant names** — copy `OBJ_TakeVillage`, `SOBJ_BuildWalls`, etc. verbatim. Do not rename or normalize them.

---

## EXECUTION ORDER

Process these **sequentially**, one at a time. For each system file:
1. Read all relevant summary files (use subagents to read in parallel where possible)
2. Extract the targeted data
3. Write the output file
4. Confirm completion before moving to the next

---

## SYSTEM FILE 1: `docs/game_systems/systems/objectives-index.md`

### Input
All 65 files in `docs/design_notes/campaigns/` (all subdirectories).

### What to Extract
From each mission summary's **KEY SYSTEMS → Objectives** section:
- Every objective constant (OBJ_, SOBJ_, TOBJ_, or dot-path like `_challenge.victory.*`)
- Its type (OT_Primary, OT_Secondary, OT_Bonus, OT_Battle, OT_Information)
- Its phase (if a Phase column exists)
- Its purpose (one-line description)
- Win/Lose conditions (from prose below the objectives table)

### Output Format
```markdown
# Objectives Index

Cross-reference of all objectives across campaign missions, extracted from Phase 3 summaries.

## Summary Statistics
- Total objectives: [count]
- By type: Primary [n], Secondary [n], Bonus [n], Battle [n], Information [n]

## By Campaign

### Abbasid Dynasty
#### abb_m1_tyre
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_... | OT_Primary | — | ... |

**Win condition:** [from prose]
**Lose condition:** [from prose]

[repeat for each mission]

### Mongol Empire
[etc.]

## Shared Patterns
- List any objective constants that appear in multiple missions
- Note naming conventions (OBJ_ vs SOBJ_ vs dot-path in challenges)
- Common objective chaining patterns (Phase 1 complete → starts Phase 2, etc.)
```

---

## SYSTEM FILE 2: `docs/game_systems/systems/difficulty-index.md`

### Input
All 65 files in `docs/design_notes/campaigns/`. Also read `docs/game_systems/gameplay/missionomatic.md` for the Util_DifVar API description.

### What to Extract
From each mission summary's **KEY SYSTEMS → Difficulty** section:
- Every `Util_DifVar` parameter row (Parameter name, Easy/Standard/Hard/Expert values, description)
- Medal tier tables (from challenges that use those instead of `Util_DifVar`)
- Any difficulty-conditional logic mentioned in prose ("Hard/Expert only", etc.)

### Output Format
```markdown
# Difficulty Index

Consolidation of all difficulty-scaling parameters across missions.

## API Reference
Brief description of `Util_DifVar(value, {easy, standard, hard, expert})` from gameplay/missionomatic.md.

## By Campaign

### Abbasid Dynasty
#### abb_m1_tyre
| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| ... | ... | ... | ... | ... | ... |

[repeat for each mission]

### Challenges (Medal Tiers)
#### challenge_basiccombat
| Medal | Threshold (PC) | Threshold (Xbox) |
|-------|----------------|-------------------|
| Gold | ... | ... |

## Cross-Mission Comparison
- Parameters that appear across multiple missions (e.g., spawn delays, army sizes)
- Scaling ranges (most generous → most punishing)
- Common scaling categories: spawn timing, unit counts, health multipliers, resource rates
```

---

## SYSTEM FILE 3: `docs/game_systems/systems/spawns-index.md`

### Input
All 65 files in `docs/design_notes/campaigns/`. Also read `docs/game_systems/gameplay/ai.md` (WaveGenerator section) and `docs/game_systems/gameplay/missionomatic.md` (Wave System section).

### What to Extract
From each mission summary's **KEY SYSTEMS → Spawns** section:
- Spawn wave definitions (source, composition, timing, difficulty scaling)
- Static defender placements
- Reinforcement mechanics
- Army module compositions
- Named spawn functions (reusable patterns)

### Output Format
```markdown
# Spawns & Wave Patterns Index

## System Reference
Brief summary of WaveGenerator and MissionOMatic Wave System from gameplay summaries.

## By Campaign

### Abbasid Dynasty
#### abb_m1_tyre
**Wave sources:** [list]
**Compositions:** [unit types and counts per difficulty]
**Timing:** [intervals, stagger delays]
**Special mechanics:** [ram system, escort splitting, etc.]

[repeat for each mission]

## Reusable Patterns
- Common spawn functions used across missions
- Typical wave escalation patterns
- Standard unit composition templates
- Difficulty scaling patterns for spawns (timing vs. count vs. composition)
```

---

## SYSTEM FILE 4: `docs/game_systems/systems/ai-patterns.md`

### Input
- `docs/game_systems/gameplay/ai.md` (primary — read this first for the system architecture)
- `docs/game_systems/gameplay/missionomatic.md` (Module System sections: Attack, Defend, RovingArmy, TownLife)
- All 65 files in `docs/design_notes/campaigns/` (the AI subsections within each)

### What to Extract
From `gameplay/ai.md`: Army system architecture, encounter plan types, combat fitness, StateTree tuning.
From `gameplay/missionomatic.md`: Module definitions (Defend, Attack, RovingArmy, TownLife, UnitSpawner).
From each campaign summary's **KEY SYSTEMS → AI** section:
- Named AI modules (Defend_Gatehouse, RovingArmy_North, etc.)
- Encounter plan configurations
- Patrol routes and behaviors
- Pursuit/retreat logic
- Difficulty-based AI tuning

### Output Format
```markdown
# AI Patterns Index

## System Architecture
Summary of AI army system, encounter plans, and module types from gameplay/ai.md.

## Module Types (from gameplay/missionomatic.md)
### Defend Modules
[API and lifecycle]
### Attack Modules
### RovingArmy Modules
### TownLife Modules
### UnitSpawner Modules

## Campaign AI Usage

### Abbasid Dynasty
#### abb_m1_tyre
**Modules used:** [list with types]
**Patrol behaviors:** [description]
**Special AI logic:** [any custom behaviors]

[repeat for each mission]

## Cross-Mission Patterns
- Most common module types and configurations
- Standard patrol/defend setups
- Difficulty-scaling of AI behavior
- Custom vs. standard encounter plan usage
```

---

## SYSTEM FILE 5: `docs/game_systems/systems/training-index.md`

### Input
- `docs/game_systems/gameplay/training.md` (primary — read this first)
- `docs/design_notes/campaigns/challenges/` (13 files — challenge missions use training goals extensively)
- `docs/design_notes/campaigns/salisbury/` (6 files — tutorial campaign)
- Skim other campaign summaries for training/tutorial mentions only

### What to Extract
From `gameplay/training.md`: Training_Goal API, goal sequence categories, data templates, civ-specific sequences.
From challenge/salisbury summaries: Specific goal sequences used and their trigger conditions.

### Output Format
```markdown
# Training & Tutorial Index

## Training_Goal API
Summary of the goal system architecture from gameplay/training.md.

## Goal Sequence Categories
[from gameplay/training.md — list all categories with descriptions]

## Civ-Specific Goal Sequences
| Civ | Sequence ID | Mechanic Taught |
|-----|-------------|-----------------|
[from gameplay/training.md]

## Campaign Usage

### Salisbury (Tutorial Campaign)
[per-mission training goal usage]

### Art of War Challenges
[per-challenge training goal usage]

## Data Templates
[from gameplay/training.md]

## Input Mode Adaptation
[PC vs Xbox controller vs Xbox KBM branching]
```

---

## SYSTEM FILE 6: `docs/game_systems/systems/missionomatic-modules.md`

### Input
- `docs/game_systems/gameplay/missionomatic.md` (primary — read this first for the full system spec)
- All 65 files in `docs/design_notes/campaigns/` (for concrete recipe/module usage examples)

### What to Extract
From `gameplay/missionomatic.md`: Recipe architecture, module system, action/condition registries, objective lifecycle, playbill system, unit request pipeline.
From campaign summaries: Concrete recipe configurations, module instantiations, location/objective wiring patterns.

### Output Format
```markdown
# MissionOMatic Module Reference

## Recipe Architecture
[Top-level fields, structure from gameplay/missionomatic.md]

## Module System
### Module Lifecycle
[Init → Activate → Update → Deactivate]

### Module Types
| Type | Purpose | Key Parameters |
|------|---------|----------------|
| Defend | ... | ... |
| Attack | ... | ... |
[etc.]

## Action & Condition Registries
### Built-in Actions
| Name | Purpose |
|------|---------|
[from gameplay/missionomatic.md]

### Built-in Conditions
| Name | Purpose |
|------|---------|
[from gameplay/missionomatic.md]

## Campaign Recipe Patterns
Summary of how different campaigns configure their recipes:
- Module count ranges (simple missions vs. complex)
- Common location wiring patterns
- Objective→module dependency patterns

## Unit Request Pipeline
[from gameplay/missionomatic.md]

## Shared Globals
[from gameplay/missionomatic.md globals table]
```

---

## SYSTEM FILE 7: `docs/api_reference/navigation/master-index.md`

### Input
After creating all 6 system files above, create this using the directory listing of all files.

### Output Format
```markdown
# AoE4 SCAR Reference — Master Index

## Quick Links
- [Function Index](function-index.md) | [CSV](function-index.csv)
- [Objectives Index (mechanical)](objectives-index.csv) | [Objectives Index (annotated)](systems/objectives-index.md)
- [Imports Index](imports-index.csv)
- [Groups Index](groups-index.csv)
- [Globals Index](globals-index.csv)

## Campaign Summaries

### Abbasid Dynasty (9 missions)
| Mission | File | Key Systems |
|---------|------|-------------|
| Siege of Tyre | [abb_m1_tyre.md](campaigns/abbasid/abb_m1_tyre.md) | Objectives, Difficulty, Spawns, AI |
[list all missions with links]

### Mongol Empire (9 missions)
[etc. for all 8 campaign folders]

## Gameplay Systems (11 files)
| System | File | Description |
|--------|------|-------------|
| Core | [core.md](gameplay/core.md) | ... |
[list all 11]

## System Indexes (6 files)
| Index | File | Cross-cuts |
|-------|------|------------|
| Objectives | [objectives-index.md](systems/objectives-index.md) | All campaigns |
| Difficulty | [difficulty-index.md](systems/difficulty-index.md) | All campaigns |
| Spawns | [spawns-index.md](systems/spawns-index.md) | All campaigns + AI/MissionOMatic |
| AI Patterns | [ai-patterns.md](systems/ai-patterns.md) | All campaigns + AI gameplay |
| Training | [training-index.md](systems/training-index.md) | Training + Challenges + Salisbury |
| MissionOMatic | [missionomatic-modules.md](systems/missionomatic-modules.md) | MissionOMatic + All campaigns |

## Phase 1 Mechanical Indexes
| File | Records | Description |
|------|---------|-------------|
| [function-index.csv](function-index.csv) | ~9,000 | All function signatures |
| [objectives-index.csv](objectives-index.csv) | ~1,500 | OBJ_/SOBJ_ constants with file/line |
| [imports-index.csv](imports-index.csv) | ~1,300 | import() dependency graph |
| [groups-index.csv](groups-index.csv) | ~3,200 | SGroup/EGroup creation calls |
| [globals-index.csv](globals-index.csv) | ~14,000 | Global variable assignments |
```

---

## EXECUTION GUIDANCE FOR COPILOT

### Reading Strategy
- The 65 campaign summaries total ~1.16 MB. You cannot read them all at once.
- Use subagents to read files in parallel batches (e.g., one subagent per campaign folder).
- For each system file, read only the relevant sections from each summary (e.g., for objectives-index.md, focus on the "Objectives" subsection in each file).
- Read the gameplay system files directly — they're small enough (~20 KB each).

### Progress Tracking
- Use the todo list tool to track which system files are complete.
- Confirm each file is written to disk before proceeding to the next.
- If a system file would exceed reasonable length (>500 lines), prioritize structured tables over prose.

### Quality Checks
- Every mission mentioned in a campaign folder should appear in the relevant system file.
- Cross-reference mission counts: abbasid(9), angevin(11), challenges(13), hundred(8), mongol(9), rogue(1), russia(8), salisbury(6) = 65 total.
- Gameplay files: ai.md, core.md, gamemodes.md, gameplay.md, missionomatic.md, prefabs_replay.md, rogue.md, startconditions.md, training.md, ui.md, winconditions.md = 11 total.
