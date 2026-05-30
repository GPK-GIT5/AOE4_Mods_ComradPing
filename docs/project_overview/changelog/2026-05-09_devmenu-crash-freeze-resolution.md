# 2026-05-09 - DevMenu Startup/Click Crash Resolution

## Status
- Resolved in user validation: startup freeze/crash and DEV submenu click crash no longer reproduce.
- Scope-complete for this session: startup hardening, click-path XAML escaping, and full Q&A prototype decommissioning.

## Executive Summary
This session addressed two distinct crash paths in the Onslaught DevMenu flow:

1. Startup freeze/crash risk during early UI creation.
2. Click-time crash when opening DEV submenu content containing unescaped XML-special characters.

The final implementation deferred and guarded initial UI creation, introduced lazy submenu presenter creation, and added XML escaping for dynamic XAML text interpolation. In addition, the unfinished Q&A debugger prototype was fully removed from active menu wiring and debug module registration to prevent accidental runtime activation.

## Root Causes
### RC-1: Startup UI creation pressure and timing coupling
- DevMenu UI presenters were created in an eager startup path.
- Early-stage UI initialization had higher contention/risk in the observed startup window.
- Mitigation: deferred creation, one-shot scheduling guard, and phased creation path.

### RC-2: Unescaped dynamic text inserted into XAML attributes
- DEV submenu title/subtitle strings were interpolated directly into XAML attribute values.
- Category strings containing characters like `&` (for example, Q&A-style labels) can produce invalid XAML and parser faults.
- Mitigation: strict XML escaping before interpolation.

## Implementation Changes
### 1. Startup lifecycle hardening and lazy submenu creation
File: `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar`
- Added deferred creation entrypoint and startup scheduling flow:
  - `DevMenu_CreateUIDeferred`
  - `DevMenu_OnPlay` defers via one-shot rule instead of eager immediate creation.
- Added idempotence/scheduling guards to avoid duplicate creation requests.
- Consolidated phased creation in `_devmenu_create_ui_now(source)` for explicit startup sequencing and easier diagnosis.
- Added lazy submenu presenter creation:
  - `_devmenu_ensure_submenu_presenter(key)` creates submenu presenters on first access.
  - Category handlers are bound at panel creation, while submenu payloads are instantiated only when opened.

### 2. Dynamic XAML escaping for click path safety
File: `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_xaml.scar`
- Added `_DEVMENU_XML_ESCAPE(value)`.
- Escaped dynamic title/subtitle in `_DEVMENU_BUILD_DEV_SUBMENU_XAML(...)` before attribute interpolation.
- Escaping covers at least `&`, `"`, `<`, `>`, and `'` to prevent malformed XAML attributes.

### 3. Full Q&A debugger prototype decommissioning
File: `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_categories.scar`
- Removed Q&A category exposure from the DEV category list.

File: `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_actions.scar`
- Removed `DevMenu_RunQAChecks` wrapper/action.

File: `Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_data.scar`
- Removed flat "Q&A Checks" command entry.
- Kept "Prompts" command path active.

File: `Gamemodes/Onslaught/assets/scar/debug/cba_debug.scar`
- Removed import of `debug/cba_debug_qa_runner.scar`.

File: `Gamemodes/Onslaught/assets/scar/debug/cba_debug_core.scar`
- Removed/cleaned Q&A runner references from active module registry wiring and stale manual-run comments.

Deleted file:
- `Gamemodes/Onslaught/assets/scar/debug/cba_debug_qa_runner.scar`

## Validation Performed
- Runtime validation (user-confirmed):
  - Startup freeze/crash resolved.
  - DEV toggle/menu click crash resolved.
- Static validation during the session:
  - Diagnostics checks on edited SCAR files reported clean for modified targets.
- Reference hygiene checks during the session:
  - Removed Q&A runner symbols were swept from active loader/registry paths.
  - Prompts category/action remained present and wired.

## Scope Boundaries
### In Scope
- DevMenu startup stabilization.
- DEV submenu click-path XAML safety.
- Q&A prototype disable/remove in active runtime paths.

### Out of Scope
- Unrelated generated-data and staging artifacts modified elsewhere in the workspace.
- Broader gameplay/AI behavior changes not required for this incident.

## Residual Risk and Follow-up
- Residual risk is low for the original repro paths, but no full UI regression matrix was executed in this session.
- Recommended follow-up:
  1. Add a small shared utility/policy note: all dynamic strings inserted into XAML attributes must be escaped.
  2. Run a quick smoke pass across remaining DEV categories/submenus to confirm no other unescaped interpolation paths exist.
  3. Keep unfinished debug prototypes disconnected from both menu exposure and debug module registries until release-ready.
