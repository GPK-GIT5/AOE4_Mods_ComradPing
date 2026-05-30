# Testing template3v.scar — Quick Reference

## 1. Setup

**Enable dev mode** (one-time):
Steam → AoE4 → Properties → Launch Options → `-dev`

**Build the mod**:
Content Editor → Build > Build Mod
Output: `Documents\My Games\Age of Empires IV\mods\extension\local\`

---

## 2. Launch & Play

1. Launch AoE4 (with `-dev`)
2. Skirmish → select your map from the **Map** dropdown
3. Set **2 players**: you (P1) + AI (P2)
4. Start match — intro NIS plays, then Objective 1 appears after ~1s

---

## 3. SCAR Console (in-game)

Open: **Alt + Shift + ~**

### Inspect State
```lua
print(g_obj_captureID)          -- nil = HUD handle not created yet
print(g_obj_destroyID)
print(player1)                  -- verify player handles
print(player2)
print(Obj_GetState(g_obj_captureID))  -- 0=Incomplete, 1=Complete, 2=Failed
```

### Skip Objective 1 (force-complete capture)
```lua
Obj_SetVisible(g_obj_captureID, false)
Obj_SetState(g_obj_captureID, OS_Complete)
Objective_Complete(OBJ_CaptureEnemiesTown, false, false)
```
This chains to Objective 2 via `CaptureTown_OnComplete`.

### Skip Objective 2 (force victory)
```lua
Obj_SetVisible(g_obj_destroyID, false)
Obj_SetState(g_obj_destroyID, OS_Complete)
Objective_Complete(OBJ_DestroyBuildings, false, false)
```

### Useful debug commands
```lua
FOW_PlayerRevealAll(player1)              -- reveal map
Player_SetResource(player1, RT_Food, 99999)
Misc_DoString("print('hello')")          -- eval arbitrary code
```

---

## 4. Editor Debugger

1. Open Content Editor alongside running game
2. Click **Attach** (ScriptEditor.Debugging toolbar)
3. Set breakpoints by clicking line gutters in template3v.scar:
   - **CaptureTown_OnStart** — verify HUD creation
   - **CaptureTown_OnComplete** — verify hide-before-complete
   - **DefeatBuildings_OnEntityKilled** — verify counter increment
   - **DestroyBuildings_OnComplete** — verify victory trigger
4. Start match → game freezes at breakpoint
5. Use **Locals/Globals** panels to inspect variables
6. Step through: **Step Over** (line-by-line), **Step Into** (enter functions), **Run** (continue)

---

## 5. Test Checklist

### Objective 1: Capture
| Check | How to verify |
|-------|---------------|
| HUD appears top-left | Visual — "Capture Enemy Town" with icon |
| Minimap ping visible | Yellow ping at mkr_enemy01_city |
| Capture zone active | Move units to FrenchCity, capture bar appears |
| No blank popup on complete | Capture the town — should show Obj 2 popup only |
| HUD element disappears | Top-left capture entry gone after complete |

### Objective 2: Destroy
| Check | How to verify |
|-------|---------------|
| HUD appears top-left | "Destroy the French city" with counter "0/N" |
| Counter increments | Destroy a barracks/archery range/TC → counter +1 |
| Ground reticule visible | Glowing ring at mkr_enemy03_city |
| Low-level counter syncs | Console: `print(Obj_GetCounterCount(g_obj_destroyID))` |
| No blank popup on complete | Destroy all targets — victory screen after 3s |

### General
| Check | How to verify |
|-------|---------------|
| Intro NIS plays | Match start — cinematic plays before gameplay |
| Victory triggers | After Obj 2 complete, player wins after 3s |
| No script errors | Check SCAR console for red text / check scarlog.txt |
| Icons not black circles | Both popups show objective icon (not blank/black) |

---

## 6. Log Files

Path: `Documents\My Games\Age of Empires IV\Logfiles\[timestamp]\`

Key file: **scarlog.txt** — contains all `print()` output and SCAR errors.

**Add temporary logging** to debug flow:
```lua
function CaptureTown_OnComplete()
    print(">>> CaptureTown_OnComplete fired")
    -- ...existing code...
end
```
Rebuild mod, restart match, check scarlog.txt.

---

## 7. Multiplayer Testing

1. Both players need `-dev` in Steam launch options
2. Host creates Custom lobby, selects the mod map
3. Second player joins — verify both see objectives
4. Test: only P1 (host) should see objective HUD (objectives are created for `player1`)
5. Verify `GE_EntityKilled` fires for buildings owned by P2 regardless of who destroys them

**Key concern**: `player1 = World_GetPlayerAt(1)` — in MP, player slot order may differ. If P1 must always be the human, verify slot assignment in lobby.

---

## 8. Common Errors

| Symptom | Cause | Fix |
|---------|-------|-----|
| Game freezes on load | `Mission_SetupPlayers` missing/crashed | Check SCAR console error |
| Objective never appears | `Objective_Start` not called or `LOCATION("FrenchCity")` is nil | Verify marker names in editor match `GetRecipe()` |
| Counter stuck at 0 | `eg_destroy_targets` empty — filter found no matching buildings | Console: `print(EGroup_CountSpawned(eg_destroy_targets))` |
| Blank popup appears | `showTitle` not suppressed or `Obj_SetVisible` not called before `OS_Complete` | Verify `CompleteHUDObjective` is called first |
| Black circle icon | Icon path wrong or asset not available | Use `"icons/objectives/objectives_generic_small"` (forward slashes) |
| "Tried to call global ??? (nil)" | Function name typo or missing `import()` | Match name exactly, check imports |

---

## 9. Hot-Reload Workflow

1. Edit template3v.scar in Content Editor or external editor
2. Build > Build Mod (Ctrl+Shift+B)
3. In running match, SCAR console: `dofile("data:scenarios/template3v/multiplayer/template3v.scar")`
4. **Caveat**: hot-reload re-runs file but does NOT reset state — globals keep old values. Restart match for clean test.

Preferred workflow: edit → build → restart match (fastest with `-dev` skirmish).
