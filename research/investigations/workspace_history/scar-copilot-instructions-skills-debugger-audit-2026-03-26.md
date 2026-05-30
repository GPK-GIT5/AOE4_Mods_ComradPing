# SCAR Copilot Portable System Brief (2026-03-26)

Purpose: single-file, workspace-independent briefing for ChatGPT analysis of AoE4 .scar workflows.

This file is self-contained. It includes the execution rules, console command contract, debugger and logging model, map/reference structure, and risk/remediation summary without requiring access to any other file.

## 1) Execution Rules (Inlined)

### 1.1 Rule priority
Use this precedence order when generating or reviewing SCAR work:
1. Version compatibility and known runtime behavior.
2. Source-of-truth indexes and verified references.
3. Existing codebase patterns (prefer proven local patterns over generic best practices).
4. Architectural consistency.
5. Code quality/style.

### 1.2 SCAR language/runtime constraints
- Lua 5.x style used by SCAR.
- Use `import()`, not `require()`.
- No metatable-heavy patterns.
- Prefer minimal, evidence-backed fixes over speculative rewrites.
- Mark uncertain runtime behavior explicitly; do not ship assumptions silently.

### 1.3 Mission/system coding constraints
- Use narrowest event scope possible:
- Global event only when truly global.
- Player/entity/squad scoped events when feasible.
- Always guard stale entity handles before operations.
- Ownership transfer caveat: changing entity owner does not trigger construction lifecycle events; counter systems must recount explicitly.

### 1.4 Siege/limit pipeline invariants
Central enforcement flow must stay:
1. Recount
2. Apply threshold
3. Field-construct gate last

Critical invariants:
- Threshold handlers must lock and unlock (bidirectional behavior).
- Do not bypass pipeline with inline production lock/unlock calls in event handlers.
- Use full revalidation when a change affects multiple limit systems.

### 1.5 XamlPresenter safety model (current effective interpretation)
Severity tiers used in practice:
- FATAL: block and auto-fix
- WARN-HIGH: flag and prefer alternative
- WARN-LOW: flag only when initialization guarantees are missing
- SAFE: default allowed

Current high-value rules:
- FATAL: Width/Height DataContext bindings in XamlPresenter.
- WARN-HIGH: Opacity DataContext binding, MergedDictionaries + local Effect resource combinations, ToolTip on non-interactive elements, XAML Storyboard/DataTrigger pathways lacking validation.
- SAFE/common: Text, Foreground, Fill, Visibility (with converter), Source, Command.

Runtime UI lifecycle requirements:
1. Add child panel.
2. Set initial data context immediately.
3. Set creation flag.
4. Guard all update calls by creation state.
5. Recreate panel for layout-class changes when required.

## 2) Console Command Contract (Inlined)

Console is treated as stateless single-entry execution surface.

Hard constraints:
- One command per block.
- Each command is one single-line raw Lua statement/expression.
- No `local`.
- No control-flow blocks (`if/for/while/repeat` blocks).
- No cross-command state assumptions.
- No comment/prose inside code blocks.
- Prefer <= 3 commands; never exceed 5.

Preferred patterns:
- Direct function call: `Debug_RunSmokeTests()`
- Single print expression: `print(Debug_Validator().ok)`
- Single global assignment when needed: `DLC_DEBUG = true`

Fallback rule:
- If logic requires iteration/control-flow/state, implement a named function in SCAR and call only that function from console.

## 3) Testing Output Contract (Inlined)

When code changes require validation, response should end with testing commands section.

Testing section rules:
1. Short validation checklist (1-3 bullets).
2. Console commands as separate Lua blocks.
3. One single-line command per block.
4. Commands must be independent.
5. Keep command count minimal and non-overlapping in coverage.

## 4) Skill Layer Summary (Inlined)

### 4.1 Console-commands skill role
- Enforces strict command syntax for Content Editor console.
- Primary reliability gate against malformed multiline/stateful command output.

### 4.2 SCAR-debug skill role
- Structured diagnosis flow for nil/entity/event/counter/UI failures.
- Provides debug command catalog and post-edit test surfacing behavior.

### 4.3 Data-extraction skill role
- Regenerates index surfaces used for deterministic SCAR lookup and navigation.

### 4.4 README-to-AI-reference skill role
- Converts narrative docs into deterministic, non-invented AI reference material.

## 5) Debugger + Logging Architecture Snapshot (Current)

Observed live topology:
- Entry debug importer currently pulls 28 debug modules.
- Architecture has expanded beyond legacy 12-file/14-file documentation states.

Core primitives:
- `DebugLog(area, msg)` for structured tagged output.
- `DebugLog_SetFilter(...)` for area filtering.
- `_Debug_EndMarker(...)` emits parseable suite completion marker:
- Format includes suite name, pass/total, elapsed, and status.
- Writes persistent run-line to debug log file channel.
- Triggers completion cue for in-game feedback.

Suite orchestration:
- `Debug_RunAll(step)` queues multiple suites and aggregates final pass/fail.
- Step mode controls (`Debug_StepMode`, `Debug_Continue`, `Debug_Skip`, `Debug_StepStatus`) support gated phase progression.
- Scheduler abstraction preserves normal behavior when step mode is off.

Reliability implication:
- The completion marker protocol (`[CBA_DEBUG_END] ...`) is the most machine-parseable signal for automated log verification.

## 6) Reference/Map Structure (Conceptual, Inlined)

Navigation planes used by workflow:
1. Top-level reference index plane (human task-based entry).
2. Navigation plane (master index + data index).
3. API plane (SCAR functions, events, constants/signatures).
4. Mechanical index plane (functions/globals/groups/imports/objectives).
5. Mod-specific index plane (mod entry and scenario-specific guides).
6. Workflow plane (extraction + deterministic consolidation playbooks).

Why this matters:
- SCAR workflow reliability depends on index-first navigation and deterministic lookup before source edits.

## 7) Overlaps, Gaps, Inconsistencies (Actionable)

### P0 - Reliability risks
1. Debug architecture drift:
- Legacy docs describe smaller debugger splits (12/14) while live importer reflects 28 modules.
- Effect: command and suite assumptions can be stale.

2. Branch naming drift in debug docs:
- Older branch naming notes conflict with current headers/import assumptions.
- Effect: wrong source expectations during fixes/migrations.

3. XAML severity mismatch across control surfaces:
- One control surface treats Opacity/MergedDictionaries+Effects as WARN-HIGH; another labels as FATAL.
- Effect: inconsistent generation/review behavior and false blocking.

### P1 - Efficiency risks
1. Directory map drift:
- Documentation map references context files no longer present.
- Effect: onboarding and navigation friction.

2. Path namespace drift:
- Some workflow docs use `reference/...` while repository uses `references/...`.
- Effect: avoidable command/path failures.

### P2 - Maintainability risks
1. Redundant console rule copies across layers.
- Effect: drift risk and update overhead.

2. Stats/timestamps across references not always synchronized.
- Effect: lower trust in quick audits (non-fatal).

## 8) What Is Working Well (Keep)

1. Three-layer console reliability guard (syntax + response format + debug-command fallback).
2. Parseable suite completion marker for log-based verification.
3. Step mode support reducing sequencing errors in long validation runs.
4. Index-first lookup model improving deterministic SCAR edits.

## 9) Fast Remediation Plan

1. Re-baseline debugger documentation to current 28-module live topology.
2. Normalize branch naming notes to one active profile.
3. Unify XAML severity statements across all control surfaces.
4. Fix `reference/` vs `references/` path drift in workflow docs.
5. Collapse console rules into one canonical source and keep other layers as pointers.

## 10) Portable Minimal Checklist

Use this checklist even without repository access:
1. Enforce single-line stateless console command grammar.
2. Use event scope minimization and stale-entity guards.
3. Recount after ownership transfer for any limit/counter system.
4. Keep siege pipeline order: Recount -> Apply -> Field gate last.
5. Treat Width/Height DataContext binding in XamlPresenter as blocked.
6. Validate via debug suites and parse completion markers, not only ad-hoc prints.
7. Resolve doc-vs-runtime mismatches before trusting any command catalog.
