# BoonUI Starter Pack

Drop-in pop-up menu (1–4 selectable cards) for AoE IV SCAR mods.

## Files in this folder

| File | Purpose | Edit it? |
|---|---|---|
| `boon_selection.scar` | Engine (show/hide/timer/click). | No |
| `boon_selection_xaml.scar` | Visual look (XAML). | Optional restyling |
| `boon_examples.scar` | Ready-to-use example menus. | **Yes — your starting point** |

## Quick start

1. Copy this whole folder into your mod, e.g. `<your-mod>/assets/scar/boonui/`.
2. In your mod's main script, add:

   ```lua
   import("boonui/boon_selection.scar")
   import("boonui/boon_examples.scar")
   ```

3. Trigger an example menu from anywhere in your scripts:

   ```lua
   Rule_AddOneShot(Example_WelcomeBonus, 5.0)
   ```

That's it. See [../boonui-guide.md](../boonui-guide.md) for the full
beginner-friendly walkthrough, templates, and troubleshooting.

## The minimum API

```lua
BoonSelection_Show({
    title    = "Pick One",
    choices  = {
        { title = "A", desc = "Choice A" },
        { title = "B", desc = "Choice B" },
    },
    on_select = function(index)
        -- index is 1 or 2
    end,
})
```

That single function is 95 % of what you'll ever need.
