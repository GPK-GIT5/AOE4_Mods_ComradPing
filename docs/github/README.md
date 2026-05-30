# .github — Workspace Automation and AI Customization

The `.github/` folder from the private workspace is not present in this public repository.

## Purpose

In the private workspace, `.github/` holds all CI/CD workflows, Copilot agent definitions, coding instructions, and PowerShell tooling scripts. See the private workspace for the full development tooling.

## Structure

```
.github/
├── agents/                  # Agent mode definitions
├── data/
│   └── aoe4/                # Local Relic IP snapshots — not redistributable
├── instructions/
│   ├── coding/
│   ├── context/
│   └── core/
├── prompts/
├── scripts/
│   ├── auditing/
│   ├── build/
│   ├── extraction/
│   ├── regression/
│   └── validation/
├── workflows/
└── copilot-instructions.md
```

## Why excluded

Contains development tooling, internal automation configuration, and local snapshots of Relic IP (`data/aoe4/`) that are not appropriate for public distribution.

## Integration points

| Consumer | Uses |
|---|---|
| VS Code Copilot | Instructions, agents, and prompts in the private workspace |
| GitHub Actions | Workflows run on the private repository |
| PowerShell tooling | Scripts invoked locally or via CI |

## Related docs

- [docs/skills/README.md](../skills/README.md)
- [docs/game_data/README.md](../game_data/README.md)
