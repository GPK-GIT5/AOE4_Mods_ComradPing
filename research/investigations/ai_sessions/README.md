# AI Session Summaries

Post-session records of changes, patterns, failures, and gaps from AI-assisted development sessions.

## Naming Convention

- **File name:** `session_YYYY-MM-DD_NN.md` (zero-padded sequence per day; `NNb` for sub-sessions)
- **SESSION_ID field:** `YYYY-MM-DD_NN` (bare ID, no `session_` prefix)

## Required Sections

Every session file should include these fields (leave empty if not applicable):

| Field | Purpose |
|-------|---------|
| SESSION_ID | Unique identifier matching the filename date/sequence |
| CHANGES | What was added or modified |
| FIXES | Bugs or regressions resolved |
| NEW PATTERNS | Reusable rules or conventions discovered |
| FAILURES | What didn't work or wasn't validated |
| NEW/UPDATED FILES | File paths touched during the session |
| GAPS | Known issues or incomplete work carried forward |

Optional fields: `CRITICAL DECISIONS`, `NEXT ACTIONS`.

## Current Sessions

| File | Date | Key Topics |
|------|------|------------|
| session_2026-03-21_01.md | 2026-03-21 | (first session of the day) |
| session_2026-03-21_02.md | 2026-03-21 | Reward import switch, locdb placeholder fix |
| session_2026-03-21_02b.md | 2026-03-21 | Sub-session continuation |
| session_2026-03-21_03.md | 2026-03-21 | (session 3) |
| session_2026-03-21_06.md | 2026-03-21 | Debug UI prompts, XamlPresenter overlay, InteractiveChecks |
| session_2026-03-21_07.md | 2026-03-21 | (session 7) |
