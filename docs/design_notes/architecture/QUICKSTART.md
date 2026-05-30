# Copilot Instructions — Quick Start

## TL;DR

**Copilot auto-loads the right instruction file based on what you're editing** — no action needed. Each instruction file uses YAML frontmatter (`applyTo: "pattern"`) to tell Copilot when to activate.

For consistent behavior in new sessions, open the project via [AoE4-Workspace.code-workspace](../../AoE4-Workspace.code-workspace). This guarantees `.github/` is part of the active workspace so [../copilot-instructions.md](../copilot-instructions.md) is discovered every time.

---

## How It Works

### The Instruction Files

This directory contains specialized instruction files that Copilot automatically loads based on **what you're editing**:

| When Editing | File Loaded | Location |
|-------------|-----------|----------|
| `.scar` files | [scar-coding.instructions.md](../instructions/scar-coding.instructions.md) | SCAR/Lua naming, APIs, console constraints |
| `.ps1` files | [ps-coding.instructions.md](../instructions/ps-coding.instructions.md) | PowerShell script structure, patterns, validation |
| Files in `Scenarios/` | [mods-scope.instructions.md](../instructions/mods-scope.instructions.md) | File restrictions, index-first rule |
| Files in `Gamemodes/` | [gamemode-scope.instructions.md](../instructions/gamemode-scope.instructions.md) | Gamemode-specific restrictions |
| Anywhere in `Scenarios/**` or `docs/gamemodes/onslaught/**` | [mod-context.instructions.md](../instructions/mod-context.instructions.md) | Mod navigation, Japan & Arabia indexes |
| Everything else | [`copilot-instructions.md`](../copilot-instructions.md) (master) | General workspace guidance |

### Frontmatter Format

Each file begins with YAML that tells Copilot when to activate:

```markdown
---
applyTo: "**/*.scar"           # Activate for all .scar files
---
```

Supported patterns:
- `"**/*.scar"` — All .scar files recursively
- `"Scenarios/**"` — All files under Scenarios/ folder
- `"**/*.ps1,**/*.csv"` — Multiple patterns (comma-separated)
- `"**/tests/*.spec.ts"` — Nested patterns

### Precedence (Highest Priority Wins)

1. **Path-specific rules** (this directory) — Most specific
2. **Master rules** (`copilot-instructions.md`) — General fallback
3. **GitHub/User defaults** — Least specific

Example: When editing a `.scar` file in `Scenarios/Japan/`, Copilot loads **both** rules:
- `scar-coding.instructions.md` (language-level rules)
- `mods-scope.instructions.md` (folder restrictions)
- Stack them: both apply simultaneously

---

## Architecture Notes

- **Total compliance:** All files <4,000 chars (GitHub Code Review hard limit)
- **Master file:** 3,997 chars (vs. original 26,467)
- **Information preserved:** 100% across 6 files
- **Auto-discovery:** No manual loading needed — Copilot pattern-matches automatically

---

## Further Reference

- **Master strategy:** [../copilot-instructions.md](../copilot-instructions.md)
- **Research & decisions:** [RESEARCH_FINDINGS_2026-03.md](RESEARCH_FINDINGS_2026-03.md)
- **Implementation plan:** [../archive/2026-03/UPDATE_PLAN_2026-03.md](../archive/2026-03/UPDATE_PLAN_2026-03.md) *(archived)*

---

## What Changed

**Before:** Single 26K-char master file (most content invisible to Code Review)  
**After:** Master (3,997 chars) + 5 specialized files (all under 4K limit)  
**Result:** 100% GitHub compliance + better guidance per context
