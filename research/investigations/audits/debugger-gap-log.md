# Debugger Gap Log

Tracks areas where no existing `Debug_*` function covers a validated change, requiring a workaround command.

When a Testing section emits a `<!-- GAP: ... -->` marker, append a row here. When a new debug helper is added to cover the gap, update status to `resolved`.

## Log

| Date | Area | Gap Description | Workaround Used | Status |
|------|------|-----------------|-----------------|--------|
| 2026-03-27 | playerui-elimination-snapshot | Snapshot output lacked opacity/fence/seed/strikethrough/progress fields required to validate C1-C3 cadence behavior. | `PlayerUI_Animate_Debug_PrintEliminationDiag()` plus scarlog trigger/complete lines. | resolved |
| 2026-03-27 | playerui-elimination-retrigger | No animation-only retrigger command existed for repeated fade tuning on already-eliminated rows. | `Debug_ForceEliminatePlayer(n)` with full scenario reset between attempts. | resolved |
| 2026-03-27 | playerui-command-catalog | PlayerUI elimination diagnostics were console-callable but not represented in SKILL.md command catalog. | Manual command recall from source files. | resolved |
| — | — | _No gaps logged yet._ | — | — |
