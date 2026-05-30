# Workspace Reorganization Audit Log

**Executed:** 2026-03-18
**Reversibility:** All moves are reversible via the reverse commands below.

---

## Move Log

| # | Operation | Source | Destination |
|---|-----------|--------|-------------|
| 1 | MOVE | `mods/Arabia/` | `Scenarios/Arabia/` |
| 2 | MOVE | `mods/Japan/` | `Scenarios/Japan/` |
| 3 | MOVE | `mods/cba-mod-summary.md` | `Gamemodes/Onslaught/cba-mod-summary.md` |
| 4 | MOVE | `mods/testing-template3v.md` | `docs/development_guides/community/testing-template3v.md` |
| 5 | DELETE | `mods/` (empty) | — |
| 6 | MOVE | `guides/` | `docs/development_guides/community/` |
| 7 | MOVE | `official-guides/` | `docs/development_guides/official/` |
| 8 | MOVE | `data/` | `reference/data/` (before rename) |
| 9 | RENAME | `reference/` | `references/` |
| 10 | RENAME | `gamemodes/` | `Gamemodes/` |

## Cross-Reference Updates

Files updated after directory moves:

| File | Changes |
|------|---------|
| `.github/copilot-instructions.md` | `mods/` → `Scenarios/`, `gamemodes/` → `Gamemodes/`, `reference/` → `references/`, `data/` → `game_data/extracted/aoe4/data/` |
| `.github/instructions/mods-scope.instructions.md` | applyTo `mods/**` → `Scenarios/**`, path refs |
| `.github/instructions/mod-context.instructions.md` | applyTo updated, `mods/` → `Scenarios/`, `reference/` → `references/` |
| `.github/instructions/gamemode-scope.instructions.md` | applyTo `gamemodes/**` → `Gamemodes/**`, path refs |
| `.github/instructions/scar-coding.instructions.md` | `reference/` → `references/`, `data/` → `game_data/extracted/aoe4/data/` |
| `.github/instructions/QUICKSTART.md` | `mods/` → `Scenarios/`, `gamemodes/` → `Gamemodes/`, `reference/` → `references/` |
| `README.md` | `guides/` → `docs/development_guides/community/`, `official-guides/` → `docs/development_guides/official/`, `reference/` → `references/` |
| `docs/api_reference/navigation/INDEX.md` | `../data/` → `data/` (data now sibling) |
| `docs/api_reference/navigation/aoe4world-data-index.md` | `../data/` → `data/` (data now sibling) |
| `docs/game_systems/mods/MOD-INDEX.md` | `../../data/` → `../data/`, `../../official-guides/` → `../../docs/development_guides/official/`, `../../mods/` → `../../Scenarios/`, `reference/` → `references/` |
| `docs/game_systems/mods/arabia-mod-index.md` | `official-guides/` → `docs/development_guides/official/` |
| `.skills/_dev/cache-manager/SKILL-GUIDE.md` | `../../data/` → `../data/` |
| `.skills/_dev/cache-manager/README.md` | `../../data/` → `../data/` |
| `.skills/_dev/cache-manager/MANIFEST.md` | `../../data/` → `../data/` |
| `docs/project_overview/changelog/QUICKSTART.md` | `mods/*` → `Scenarios/*`, `data/` → `game_data/extracted/aoe4/data/`, `guides/` → `docs/development_guides/community/` |
| `docs/project_overview/changelog/README.md` | `mods/` → `Scenarios/` in routing rules, `data/` → `game_data/extracted/aoe4/data/`, `guides/` → `docs/development_guides/community/` |
| `docs/project_overview/changelog/USAGE.md` | `mods/` → `Scenarios/` in routing references |
| `docs/project_overview/changelog/migrate-to-scopes.ps1` | `^mods/` → `^Scenarios/` pattern |
| `Scenarios/Arabia/README.md` | `../../official-guides/` → `../../docs/development_guides/official/`, `../../guides/` → `../../docs/development_guides/community/`, tree `mods/Arabia/` → `Scenarios/Arabia/`, CBA link → `../../Gamemodes/Onslaught/` |
| `Scenarios/Arabia/IMPLEMENTATION-PLAN.md` | `mods/Arabia/` → `Scenarios/Arabia/`, `reference/mods/` → `docs/game_systems/mods/` |
| `Scenarios/Japan/MOD-INDEX.md` | `reference/` → `references/`, `data/` → `game_data/extracted/aoe4/data/`, `workspace/reference/` → `references/`, `workspace/guides/` → `docs/development_guides/community/` |
| `Gamemodes/Dependencies/Advanced Game Settings/README.md` | `gamemodes/` → `Gamemodes/` |
| `Gamemodes/Dependencies/Advanced Game Settings/ai/architecture.md` | `gamemodes/` → `Gamemodes/` |
| `Gamemodes/Dependencies/Advanced Game Settings/ai/settings_schema.yaml` | `gamemodes/` → `Gamemodes/` |
| `.github/copilot/REFERENCE_GENERATION_STRATEGY.md` | `gamemodes/` → `Gamemodes/` |
| `.github/instructions/ai-reference.instructions.md` | `gamemodes/` → `Gamemodes/` |
| `.skills/readme-to-ai-reference/ai/AI_INDEX.md` | `reference/` → `references/` |
| `docs/game_systems/mods/japan_reference/japan-stage4-restriction.md` | `reference/mods/` → `docs/game_systems/mods/` |
| `README.md` | Display text `reference/` → `references/` in link table |

## Reverse Commands (Full Rollback)

```powershell
cd c:\Users\Jordan\Documents\AoE4-Workspace

# Reverse step 10: Gamemodes/ → gamemodes/
Rename-Item -Path "Gamemodes" -NewName "_gamemodes_tmp"
Rename-Item -Path "_gamemodes_tmp" -NewName "gamemodes"

# Reverse step 9: references/ → reference/
Rename-Item -Path "references" -NewName "reference"

# Reverse step 8: reference/data/ → data/
Move-Item -Path "reference\data" -Destination "data"

# Reverse step 7: docs/development_guides/official/ → official-guides/
Move-Item -Path "user_references\official-guides" -Destination "official-guides"

# Reverse step 6: docs/development_guides/community/ (minus testing-template3v.md) → guides/
Move-Item -Path "user_references\guides\testing-template3v.md" -Destination ".\testing-template3v-temp.md"
Move-Item -Path "user_references\guides" -Destination "guides"
Move-Item -Path ".\testing-template3v-temp.md" -Destination "guides\testing-template3v-temp.md"
Remove-Item -Path "user_references" -Force

# Reverse steps 1-4: Recreate mods/
New-Item -ItemType Directory -Path "mods" -Force
Move-Item -Path "Scenarios\Arabia" -Destination "mods\Arabia"
Move-Item -Path "Scenarios\Japan" -Destination "mods\Japan"
Move-Item -Path "gamemodes\Onslaught\cba-mod-summary.md" -Destination "mods\cba-mod-summary.md"
# Move testing-template3v back
Move-Item -Path "guides\testing-template3v-temp.md" -Destination "mods\testing-template3v.md"
Remove-Item -Path "Scenarios" -Force

# NOTE: Cross-reference file edits must be reverted via git:
# git checkout -- .github/ README.md references/ docs/project_overview/changelog/ Scenarios/
```
