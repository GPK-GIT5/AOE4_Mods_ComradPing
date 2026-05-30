# Quick Start — Adding Your First Changelog Entry

Add changes to the AoE4 workspace changelog in 5 minutes. This guide covers the essential workflow.

## 1. Identify Your Scope (1 minute)

Determine which category your change belongs to:

| File Path | Scope | Example: Changed `reference/commands-reference.md` |
|-----------|-------|------|
| `Scenarios/*` or `Gamemodes/*` | **mods** | Changes to mod/scenario/gamemode files |
| `docs/project_overview/changelog/*` (scripts, configs, JSON schemas) | **system** | Updated `validate-entry.ps1` script |
| Everything else: `references/`, `user_references/`, `game_data/extracted/aoe4/`, root configs | **workspace** | ✅ Use **workspace** scope |

## 2. Create Your Entry (2 minutes)

A changelog entry is a single line of valid JSON. Create it using this template:

```json
{
  "timestamp": "2026-02-24T15:30:00Z",
  "file": "reference/commands-reference.md",
  "status": "added",
  "type": "markdown",
  "change": "Added 5 new game events (OnPlayerDefeat, OnGameEnd, OnResourceTransfer, OnUnitKilled, OnBuildingCompleted)",
  "impact": "documentation",
  "category": "reference",
  "audience": "scripters",
  "tags": ["api", "events", "scar"],
  "notes": "Resolves GitHub issue #42, enables event-driven mod logic"
}
```

**Field Quick Reference:**
- **timestamp**: `ISO 8601` format with Z suffix (e.g., `2026-02-24T15:30:00Z`). All changes in same prompt get same timestamp.
- **file**: Relative path from workspace root (e.g., `reference/commands-reference.md`)
- **status**: `added`, `modified`, or `removed`
- **type**: File type such as `markdown`, `json`, `typescript`, `powershell`, `config`
- **change**: What changed (1-2 sentences)
- **impact**: `critical`, `major`, `minor`, `bugfix`, `documentation`, `refactor`, `internal`, `other`
- **category**: Topic area (`reference`, `data`, `scripts`, `mods`, `guides`, `systems`)
- **audience**: Who cares (`scripters`, `modders`, `testers`, `users`, `api-tools`)
- **tags**: Array of searchable keywords
- **notes**: Optional additional context (GitHub issues, related tasks, etc.)

**Required vs Optional:** 9 fields are required; `notes` is optional.

## 3. Validate Before Appending (1 minute)

Always validate your entry before adding it to the log:

```powershell
cd changelog
# Copy your entry object (the entire JSON) and run:
.\scripts\validate-entry.ps1 -Entry '{"timestamp":"2026-02-24T15:30:00Z","file":"reference/commands-reference.md",...}'
```

**Expected output if valid:**
```
✓ Valid entry - ready to append
```

**If invalid,** you'll see a clear error message showing which field failed. Fix it and try again.

## 4. Append to Daily Log (1 minute)

Once validated, append to the appropriate scope's daily file:

```powershell
# Append to workspace scope (most common)
Add-Content changelog\output\workspace\2026-02\2026-02-24.jsonl '{"timestamp":"2026-02-24T15:30:00Z","file":"reference/commands-reference.md",...}'

# Or mods scope:
Add-Content changelog\output\mods\2026-02\2026-02-24.jsonl '{"timestamp":"2026-02-24T15:30:00Z",...}'

# Or system scope:
Add-Content changelog\output\system\2026-02\2026-02-24.jsonl '{"timestamp":"2026-02-24T15:30:00Z",...}'
```

**Tip:** Copy the validated entry string exactly (including outer braces), then paste it in the `Add-Content` command.

## 5. Auto-Generate Summary (Optional, 1 minute)

After adding entries, generate an updated overview:

```powershell
cd changelog
.\scripts\generate-overview.ps1 -Scope workspace -Month 2026-02
.\scripts\generate-detailed-entries.ps1 -Scope workspace -Month 2026-02
```

This creates `output/workspace/2026-02/INDEX.md` with a dashboard + detailed entries.

## Next Steps

- **View all entries for a file:** `Get-Content output\workspace\2026-02\*.jsonl | ConvertFrom-Json | Where-Object { $_.file -eq 'reference/commands-reference.md' }`
- **Export for release notes:** Copy from `output/workspace/2026-02/INDEX.md`
- **Query by impact:** `Get-ChildItem output -Recurse -Filter *.jsonl | Get-Content | ConvertFrom-Json | Where-Object { $_.impact -eq 'critical' }`
- **See all options:** Check [README.md — Quick Reference](README.md#quick-reference)

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Validation fails with "timestamp" error | Ensure format is `YYYY-MM-DDTHH:MM:SSZ` with Z suffix |
| Validation fails with missing field | Every entry needs all 10 fields (`timestamp`, `file`, `status`, `type`, `change`, `impact`, `category`, `audience`, `tags`, `notes`) |
| Path errors when running scripts | Make sure you're in the `docs/project_overview/changelog/` directory before running `.ps1` scripts |
| Can't find my change in overview | Verify you used the correct scope (`mods/`, `system/`, or `workspace/`) and correct file path prefix (`Scenarios/`, `Gamemodes/`, `references/`) |

---

**Questions?** See [README.md — Scope Definitions](README.md#scope-definitions) or [README.md — Schema Consistency Rules](README.md#schema-consistency-rules).
