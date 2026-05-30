# .skills — Copilot Custom Skills

The `.skills/` folder from the private workspace is not present in this public repository.

## Purpose

In the private workspace, `.skills/` contains self-contained Copilot skill packages that drive AI-assisted authoring of SCAR scripts, game-data extraction, and AoE4 MCP server queries.

## Structure

```
.skills/
├── index.md
├── aoe4-mcp/
├── console-commands/
├── data-extraction/
├── readme-to-ai-reference/
├── scar-debug/
└── _dev/
    └── cache-manager/     # TypeScript dev sandbox; node_modules/ excluded everywhere
```

## Why excluded

Tightly coupled to the private development environment: local MCP server, private data pipelines, and workspace-specific Copilot configuration that does not apply outside the private workspace.

## Integration points (private workspace)

| Consumer | Uses |
|---|---|
| VS Code Copilot agent mode | All `SKILL.md` files via `index.md` |
| `data-extraction` skill | Drives the `game_data/` extraction pipeline |
| `aoe4-mcp` skill | Live AoE4 MCP server blueprint queries |
