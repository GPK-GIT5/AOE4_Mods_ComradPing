# BoonUI — Beginner's Guide

A friendly, no-jargon guide to **BoonUI**: a small, drop-in pop-up menu for
SCAR-based Age of Empires IV mods. It lets a player choose between 2–4
"cards" (a title, an icon, a description, and a Select button) and runs
whatever code you want when they pick one.

> **Who this is for:** Modders and curious players with **no programming
> background**. You only need a text editor (Notepad, Notepad++, VS Code…)
> and a mod project to drop the files into.

---

## 1. What is BoonUI?

BoonUI is a small "menu in a box." You give it a question and a few
choices; it shows them on screen with nice cards; when the player clicks
one, you decide what happens next.

It looks roughly like this:

```
        ┌──────────────────────────────────┐
        │     Welcome — Pick a Bonus       │
        │     Choose one. The other is     │
        │             lost.                │
        │                                  │
        │   [icon]        [icon]           │
        │  +500 Wood    +500 Food          │
        │  Lumberjack    Farmer            │
        │  Receive…      Receive…          │
        │  [Select]      [Select]          │
        │                                  │
        │      Auto-selects in 30s         │
        └──────────────────────────────────┘
```

**Three things to know:**

1. It supports **1 to 4 cards** at a time.
2. It can **auto-pick** a default card after a timer (or wait forever).
3. When the player clicks, **one function you wrote gets called**. That
   function should *only* record what the player picked and ask the game
   to apply it through a network event — see **Section 4.5** below for
   why, and **Section 11** for the exact pattern you must follow if you
   want your mod to work in multiplayer.

> ⚠ **Multiplayer warning:**
> BoonUI runs **only on the player who clicks**. If your `on_select`
> calls `Player_AddResource`, `Player_CompleteUpgrade`, `Modify_*`,
> `World_*`, etc. directly, **only that one machine will change** and
> the other players will get a **Sync Error** within seconds. The full
> safe pattern is in [Section 11](#11-multiplayer-safety-the-only-pattern-that-works).
> If your mod is single-player only, you can ignore this and pretend
> Section 11 doesn't exist.

---

## 2. The Ready-to-Use Folder

The starter pack lives next to this guide:

[boonui-starter/](boonui-starter/)

It contains three files:

| File | What it does | Do you edit it? |
|---|---|---|
| `boon_selection.scar` | The "engine" that opens, closes, and times the menu. | **No.** Drop in as-is. |
| `boon_selection_xaml.scar` | The visual look (colors, layout, fonts). | Optional — only if you want to restyle. |
| `boon_examples.scar` | Three or four ready-made example menus. **This is your starting point.** | **Yes — copy and modify.** |

---

## 3. Installing the Starter Pack (one-time setup)

1. Copy the **entire `boonui-starter/` folder** into your mod's SCAR
   scripts directory. A common location is something like:
   `<your-mod>/assets/scar/boonui/`.
2. In your mod's **main script** (often `<your-mod>.scar` or whichever file
   already has `import(...)` lines at the top), add:

   ```lua
   import("boonui/boon_selection.scar")
   import("boonui/boon_examples.scar")
   ```

   Adjust the path so it matches where you placed the folder.
3. Save and reload the mod. That's it — BoonUI is now installed.

> If your mod uses a different folder structure, the only rule is:
> `boon_selection.scar` must be **import**ed before any code that calls
> `BoonSelection_Show(...)`.

---

## 4. The 30-Second API

You only need to know **one function**:

```lua
BoonSelection_Show({
    title          = "Header text",
    subtitle       = "Smaller text under the title (optional)",
    timeout        = 30,        -- seconds; use 0 to wait forever
    default_choice = 1,         -- which card auto-picks if the timer ends

    choices = {
        { title = "Card 1", unit = "Tag", desc = "Short description", icon = "" },
        { title = "Card 2", unit = "Tag", desc = "Short description", icon = "" },
        -- up to 4 cards total
    },

    on_select = function(index)
        -- index is 1, 2, 3, or 4 — whichever card the player clicked.
    end,
})
```

That's the **whole** API for everyday use.

---

## 5. Step-by-Step — Your First Custom Menu

Goal: show a 2-card menu that gives the player **+500 wood** or **+500 food**.

### Step 1 — Open the examples file
Open `boonui-starter/boon_examples.scar` in your text editor.

### Step 2 — Find `Example_WelcomeBonus`
Use **Ctrl + F** and search for `Example_WelcomeBonus`. It's already a
2-card wood/food menu — you can use it as your blueprint.

### Step 3 — Copy the function
Select the whole `function Example_WelcomeBonus() ... end` block, copy it,
and paste it back in the file under a new name, e.g.
`function MyMod_StartingChoice()`.

### Step 4 — Edit the cards
Change the `title`, `unit`, `desc`, and the action inside `on_select`.
For example, change `+500 Wood` to `+1000 Wood`.

> If your mod is multiplayer, do **not** put `Player_AddResource` directly
> inside `on_select`. Instead, follow the pattern in
> [Section 11](#11-multiplayer-safety-the-only-pattern-that-works) — the
> `on_select` records the choice and a network handler does the actual
> resource grant on every player's machine. The single-player examples
> shipped in `boon_examples.scar` skip this for brevity; that's fine for
> testing but **not** safe for an MP release.

### Step 5 — Trigger the menu
In your mod's startup script, add:

```lua
Rule_AddOneShot(MyMod_StartingChoice, 5.0)
```

This shows the menu **5 seconds after the match begins**. Save, reload the
mod, and start a match.

That's it — you have your own boon menu.

---

## 6. Copy-Paste Templates

### Template A — Minimal 2-card menu

```lua
function MyMenu_Simple()
    BoonSelection_Show({
        title   = "<Your Question>",
        timeout = 0,                 -- wait forever
        choices = {
            { title = "<Option A>", desc = "<What it does>" },
            { title = "<Option B>", desc = "<What it does>" },
        },
        on_select = function(index)
            -- Put your code here. index is 1 or 2.
        end,
    })
end
```

### Template B — 4-card menu with timer + default

```lua
function MyMenu_Full()
    BoonSelection_Show({
        title          = "<Header>",
        subtitle       = "<Smaller text under the header>",
        timeout        = 45,
        default_choice = 1,
        choices = {
            { title = "<A>", unit = "<tag>", desc = "<...>", icon = "" },
            { title = "<B>", unit = "<tag>", desc = "<...>", icon = "" },
            { title = "<C>", unit = "<tag>", desc = "<...>", icon = "" },
            { title = "<D>", unit = "<tag>", desc = "<...>", icon = "" },
        },
        on_select = function(index)
            print("[MYMOD] Picked option " .. tostring(index))
        end,
    })
end
```

### Template C — Trigger your menu from another script

```lua
-- Show the menu 60 seconds into the game:
Rule_AddOneShot(MyMenu_Simple, 60.0)

-- Or show it once a player reaches a certain age:
-- (See SCAR docs for Rule_AddGlobalEvent and GE_PlayerAgeUp.)
```

---

## 7. Customizing the Cards

Every card in `choices` can have these fields. All are optional — leave a
field out and BoonUI will use a sensible default.

| Field | What it does | Notes |
|---|---|---|
| `title` | Big white text on the card | Keep short — 1–3 words |
| `unit` | Smaller blue tag under the title | Use it for a category like "Economy" or leave blank |
| `desc` | Small gray description | One short sentence is best |
| `icon` | Picture shown at the top of the card | Use `""` for no icon, or a `pack://` path (see Section 9) |

### Example — change a card's wording

Find this card in `boon_examples.scar`:

```lua
{ title = "+500 Wood", unit = "Lumberjack's Gift", desc = "Receive 500 wood immediately.", icon = "" },
```

Change it to:

```lua
{ title = "+1000 Wood", unit = "Royal Grant", desc = "A massive wood shipment arrives.", icon = "" },
```

Save and reload. Done.

---

## 8. Troubleshooting — Common Problems

**The menu doesn't appear.**
- Make sure `import("boonui/boon_selection.scar")` is in your main script
  and that the path matches where you put the folder.
- Make sure something actually calls `BoonSelection_Show(...)` — for
  example via `Rule_AddOneShot`.
- Open the in-game console (if available) and look for `[BOON_SELECTION]`
  log lines.

**The menu appears but cards are missing.**
- Check that you have **at least 1 and at most 4** entries in `choices`.
- Each card line must end with a comma `,` and the curly braces `{ ... }`
  must be balanced.

**Clicking a card does nothing.**
- Your `on_select` function probably has a typo. Check the `[BOON_SELECTION][ERROR]`
  line in the console — it will print the Lua error.

**My description shows weird symbols (`â€™` etc.).**
- You pasted "smart quotes" from Word or Google Docs. Replace them with
  plain straight quotes: `"like this"`, never `“like this”`.

**The mod won't load after my edit.**
- Almost always one of:
  - A missing comma at the end of a line.
  - A missing or extra `}` (curly brace).
  - A missing closing quote on a `title =` or `desc =`.
- Open the file again and compare each entry to the others. If in doubt,
  undo (`Ctrl + Z`) and try smaller changes.

---

## 9. Advanced — For Experienced Modders

Skip this section if you're just getting started.

### 9.1 Custom icons

`icon` accepts any WPF `pack://` path that the AoE4 client can resolve.
Most built-in icons live under `WPFGUI` and use this shape:

```lua
icon = "pack://application:,,,/WPFGUI;component/icons/<sub-path>/<file>.png"
```

If you want the engine to look up an upgrade's official icon
automatically, the starter pack also ships a helper inside
`boon_selection_data.scar` (in the source mod). The relevant snippet is:

```lua
local ubp = BP_GetUpgradeBlueprint(upg_name)
local uiinfo = BP_GetUpgradeUIInfo(ubp)
local icon = string.format(
    "pack://application:,,,/WPFGUI;component/%s.png",
    string.gsub(uiinfo.iconName, "\\", "/"))
```

Both `BP_GetUpgradeBlueprint` and `BP_GetUpgradeUIInfo` are documented in
the official SCAR API reference.

### 9.2 Hiding or canceling the menu manually

```lua
BoonSelection_Hide()                -- visually hide the panel (no callback fires)
BoonSelection_IsActive()            -- returns true if a menu is open
BoonSelection_ForceSelect(2)        -- programmatically click card 2
BoonSelection_Cleanup()             -- fully remove panel (use on game end)
```

### 9.3 Per-player menus in multiplayer

`BoonSelection_Show` is **per-local-player** — only the machine that runs
it sees the panel. To present a menu on every human player's screen,
loop over `World_GetPlayerCount()`:

```lua
for i = 1, World_GetPlayerCount() do
    local p = World_GetPlayerAt(i)
    -- … call BoonSelection_Show with a closure that captures p …
end
```

A complete version of this pattern is `Example_PerPlayerWelcome` in
`boon_examples.scar`.

### 9.4 Restyling the panel

Open `boon_selection_xaml.scar`. The XAML inside the `[[ ... ]]` block is
plain WPF. Common edits:

- **Card colors**: search for `BoonCardButtonStyle` and change the
  `Background` / `BorderBrush` hex values (e.g. `#CC1A2332`).
- **Title color**: search for `Foreground="#FFD54F"` (the gold title) and
  pick your own hex color.
- **Card width**: change `MinWidth="200" MaxWidth="220"` on the card
  border.

> **Safety rules** when editing the XAML (these are non-negotiable):
> - Don't bind `Opacity` directly inside an `ItemsControl` template — use
>   alpha-encoded `Fill` strings instead. The current XAML has no
>   `ItemsControl`, so as long as you keep it that way you're fine.
> - Don't bind raw numbers; bind only strings and the existing `BoolToVis`
>   visibility flags.

These two rules prevent a known D3D crash class. They are part of the
project's hardened UI conventions.

### 9.5 Replacing the data layer

The starter `boon_examples.scar` is just **one** way to provide cards.
You can build your own data layer (a table per civ, a random rotation, a
condition-driven dispatcher, …) and pass it to `BoonSelection_Show` the
same way. The engine doesn't care where the `choices` table came from.

---

## 10. Summary — The 30-Second Version

- Drop the **`boonui-starter/`** folder into your mod.
- `import("boonui/boon_selection.scar")` in your main script.
- Call **`BoonSelection_Show({ title=…, choices=…, on_select=… })`**.
- Up to **4 cards**. `timeout = 0` means "wait forever."
- Edit `boon_examples.scar` for ready-made copy-paste menus.
- **For multiplayer:** read [Section 11](#11-multiplayer-safety-the-only-pattern-that-works).
  `on_select` is local-only; sim changes must go through a network
  handler.
- If something breaks: check commas, quotes, braces — almost always the
  culprit.

Have fun building menus!

---

## 11. Multiplayer Safety — The Only Pattern That Works

> **Required reading for any mod that may be played with more than one
> human.** Skip only if your mod is locked to single-player.

### 11.1 Why `on_select` is dangerous in MP

BoonUI shows the panel and runs `on_select` **only on the machine of the
player who clicks**. The other peers never see the click and never enter
your `on_select` function. So this code:

```lua
on_select = function(idx)
    Player_AddResource(player.id, RT_Wood, 500) -- ❌ ONLY local peer runs this
end
```

produces *immediate* divergence: one machine has +500 wood, the others do
not. AoE4's lockstep simulation detects the mismatch within a few frames
and drops everyone with a **Sync Error**.

The same applies to `Player_CompleteUpgrade`, `Player_SetCurrentAge`,
`Modify_PlayerResourceRate`, `World_*`, `Cmd_*`, `Squad_*`, `Entity_*`,
and any other API that changes simulation state.

### 11.2 The pattern: **intent → broadcast → handler**

```
  player clicks card
        │
        ▼
┌─────────────────────────┐
│  on_select  (LOCAL)     │   1) read which card was picked
│                         │   2) call Network_CallEvent(...)
│  NO Player_*/Modify_*   │      ── that's it ──
└─────────────────────────┘
        │  (engine broadcasts to every peer)
        ▼
┌─────────────────────────┐
│  MyMod_ApplyChoiceNtw   │   runs on EVERY player's machine
│  (sender, data)         │   with the same (sender, data)
│                         │
│  HERE you call          │   • Player_AddResource
│  Player_*, Modify_*,    │   • Player_CompleteUpgrade
│  World_*, etc.          │   • Modify_PlayerResourceRate
└─────────────────────────┘   • …
```

### 11.3 Copy-paste template (MP-safe `+500 wood` example)

```lua
-- =====================================================================
-- 1. REGISTER ONCE, somewhere your mod runs at startup
--    (Mod_OnInit, Mod_PreInit, or any Scar_AddInit function).
-- =====================================================================
function MyMod_Init()
    Network_RegisterEvent("MyMod_ApplyWelcomeChoiceNtw")
end
Scar_AddInit(MyMod_Init)

-- =====================================================================
-- 2. OPEN THE MENU. on_select only RECORDS the choice and broadcasts.
--    No Player_* calls in here.
-- =====================================================================
function MyMod_StartingChoice()
    BoonSelection_Show({
        title = "Welcome — Pick a Bonus",
        timeout = 30,
        default_choice = 1,
        choices = {
            { title = "+500 Wood", desc = "A lumber shipment." },
            { title = "+500 Food", desc = "A food shipment."   },
        },
        on_select = function(idx)
            -- target_player_index = whoever owns this menu instance.
            -- For a per-player loop, capture the index in a closure.
            local local_idx = Game_GetLocalPlayer().PlayerID
            Network_CallEvent(
                "MyMod_ApplyWelcomeChoiceNtw",
                string.format("%d,%d", local_idx, idx))
        end,
    })
end

-- =====================================================================
-- 3. THE HANDLER. Top-level global. Runs on EVERY peer with the same
--    arguments. THIS is where you actually change the game.
-- =====================================================================
function MyMod_ApplyWelcomeChoiceNtw(sendingPlayer, data)
    local parts = string.split(data) -- comma-separated
    local target_id = tonumber(parts[1])
    local choice = tonumber(parts[2])

    -- Resolve target by ID, NOT by Game_GetLocalPlayer().
    local target = Player_FromId(target_id) -- or World_GetPlayerAt(...)
    if target == nil then return end

    if choice == 1 then
        Player_AddResource(target, RT_Wood, 500) -- ✅ runs on every peer
    else
        Player_AddResource(target, RT_Food, 500) -- ✅ runs on every peer
    end

    -- UI-only side effects (sound, event cue) — gated to the local viewer.
    if sendingPlayer == Game_GetLocalPlayer() then
        -- e.g. UI_CreateEventCue(...) for a confirmation pop-up
    end
end
```

### 11.4 The five rules (do not break any of them)

1. **Register the event before any peer can call it.** One
   `Network_RegisterEvent("<Name>")` call from `Mod_OnInit` /
   `Scar_AddInit` is enough.
2. **The handler is a top-level global function.** Not a `local`, not a
   closure. The engine looks it up by name through `_G`.
3. **The payload is a string.** Encode any IDs/indices/flags as
   `"a,b,c"` and parse them on the other side. Never try to send a Lua
   table, function, or blueprint handle.
4. **Identify the target player by ID/index inside the handler.** Never
   assume the target is `Game_GetLocalPlayer()` — that value is different
   on every machine.
5. **`Game_GetLocalPlayer()` inside the handler is allowed only for
   purely visual side effects** (a popup, a sound, hiding the panel).
   Never for deciding *whether* a Player_*/Modify_*/World_* call runs.

### 11.5 Anti-patterns — do not ship any of these

```lua
-- ❌ Mutation directly inside the click callback
on_select = function(idx)
    Player_CompleteUpgrade(player.id, upg_bp)
end

-- ❌ "Show menu only to local, autopick for everyone else" — peers diverge
if not player.isLocal then
    Player_AddResource(player.id, RT_Wood, 500) -- non-local mutates immediately
    return
end
BoonSelection_Show(...)                          -- local waits for click

-- ❌ Per-player loop reading the local player's data to make the call
for _, p in ipairs(PLAYERS) do
    if Game_GetLocalPlayer().civ == "malian" then -- always local's civ!
        Player_AddResource(p.id, RT_Gold, 100)
    end
end

-- ❌ Closure passed to a rule (rules require named globals for determinism)
Rule_AddOneShot(function() Player_AddResource(...) end, 5)
```

If you find yourself writing any of these because the safe version feels
harder, that's a signal to re-read 11.3 — not to skip the safety.

### 11.6 Per-player menus (MP-safe loop)

When you want every human to see their own panel, the *show* loop runs
on every peer (each peer's BoonUI only renders for its local player), and
each `on_select` broadcasts only the local player's pick:

```lua
for i = 1, World_GetPlayerCount() do
    local p = World_GetPlayerAt(i)
    if p == Game_GetLocalPlayer() then
        BoonSelection_Show({
            title = "Pick your bonus",
            choices = { ... },
            on_select = function(idx)
                Network_CallEvent(
                    "MyMod_ApplyWelcomeChoiceNtw",
                    string.format("%d,%d", p.PlayerID, idx))
            end,
        })
    end
end
```

Each human originates one broadcast. The handler runs on every peer once
per broadcast, applies the resource grant to the correct target, and
state stays identical everywhere.

### 11.7 Where to read more

For the full architecture rationale, the engine call chain
(`Network_CallEvent` → `Command_PlayerBroadcastMessage` →
`GE_BroadcastMessage` → `Network_Callback` → your handler), and the
migration checklist used by the Onslaught gamemode, see
[`docs/game_systems/systems/mp-deterministic-mutation-pattern.md`](../../../game_systems/systems/mp-deterministic-mutation-pattern.md)
in this workspace.

The single best official example to mirror is `chart_a_course.scar` from the
base-game script dump (not published in this public workspace). For local
extraction context and acquisition notes, see
[`docs/game_data/README.md`](../../../game_data/README.md).
