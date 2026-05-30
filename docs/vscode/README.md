# .vscode — Workspace Editor Configuration

The `.vscode/` folder from the private workspace is not present in this public repository.

## Purpose

In the private workspace, `.vscode/` stores per-workspace Visual Studio Code settings, launch configurations, and task definitions.

## Typical contents

```
.vscode/
├── settings.json       # .scar → Lua, cache/ excluded from search
├── launch.json         # TypeScript debug profiles
├── tasks.json          # PowerShell scripts wired as VS Code tasks
└── extensions.json     # Recommended: Lua LSP, Copilot, PowerShell, GitLens
```

## Why excluded

Developer-machine-local configuration. Contributors should create their own `.vscode/` from the extension recommendations and build task patterns documented in [docs/github/README.md](../github/README.md).

## Integration points

| File | Effect |
|---|---|
| `settings.json` | `.scar` treated as Lua; `cache/` excluded from search |
| `tasks.json` | Surfaces `.github/scripts/` tooling as runnable tasks |
| `extensions.json` | Extension recommendations for AoE4 mod development |
