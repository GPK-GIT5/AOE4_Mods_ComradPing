# DevMenu Network Routing Fix — 2026-05-13

## Root cause

OOS at tick 164 in a 2-player Onslaught MP game. Player 1004 had exactly 7 new
entities, 7 population, 3 permanent modifiers, and 16 state-tree entries appear
on the pressing peer only. The scarlog confirmed `[DEVMENU] spawn army at
town_centre` fired ~30 seconds before the desync frame.

`DevMenu_DoSpawnArmy()` was calling `CheatSpawnCoreUnits(player, pos)` directly
from a UI button handler. UI handlers run on **one peer only**. The
`_DEVMENU_NET_ACTIONS` dispatch table (Phase 6, added 2026-05-12) had full
handler implementations for all spawn and selection-based actions, but
**no callsite in the action functions ever invoked `_devmenu_mp_net_action`**.
The bridge was never connected.

## Fix

Added `_devmenu_mp_net_action(player, "ACTION_KEY", payload)` routing to all
sim-mutating DevMenu action functions. In MP the call routes through
`Network_CallEvent("DevMenu_NetworkDispatch", msg)` → lockstep bus → fires
`GE_BroadcastMessage` on ALL peers at the same sim tick → handler executes
the mutation deterministically everywhere. In SP `_devmenu_mp_net_action`
returns `false` and the existing direct-call path continues unchanged.

### Files changed

**`devmenuUI/devmenu_actions.scar`**

| Function | Routing key | Payload |
|---|---|---|
| `DevMenu_DoSpawnArmy` | `DEVMENU_SPAWN_ARMY` | _(none — handler uses player's Keep)_ |
| `DevMenu_DoSpawnArmyAtCamera` | `DEVMENU_SPAWN_ARMY_CAM` | `"x y z"` (camera-forward pos) |
| `DevMenu_DoSpawnPhotonMan` | `DEVMENU_SPAWN_PHOTON` | _(none)_ |
| `DevMenu_DoDestroySelected` | `DEVMENU_DESTROY` | space-separated entity IDs |
| `DevMenu_DoConvertSelected` | `DEVMENU_CONVERT` | `"target_pid nsquads sqid... eid..."` |
| `DevMenu_DoBurnSelected` | `DEVMENU_BURN` / `DEVMENU_UNBURN` | space-separated entity IDs |
| `DevMenu_DoInvulnSelectedUnits` | `DEVMENU_INVULN_SEL` | `"dir nsquads sqid..."` |

**`devmenuUI/devmenu.scar`**

| Function | Routing key | Payload |
|---|---|---|
| `DevMenu_TeleportSelectedToCameraCenter` | `DEVMENU_TELEPORT` | `"x y z sqid..."` |

**`scripts/audit_devmenu_mp_safety.ps1`**

Updated `$hasGate` detection to accept `_devmenu_mp_net_action` in addition to
`_devmenu_mp_gate`, so Phase 6 routing satisfies the lint. Script passes clean.

## Notes

- Keep-skip and invincible-check guards are applied **at serialization time**
  (pressing peer) for DESTROY, so the handler does not need to re-check them.
- BURN splits the selection into burn/unburn batches and sends two separate
  `Network_CallEvent` messages. Both are enqueued into the lockstep bus in the
  same sim frame.
- TELEPORT routing is in `devmenu.scar`, not `devmenu_actions.scar`, because
  `DevMenu_DoTeleportSelected` delegates to `DevMenu_TeleportSelectedToCameraCenter`.
- The `DoSpawnArmyAtCamera` fallback path (position not serializable) routes as
  `DEVMENU_SPAWN_ARMY` (Keep-based) rather than silently running locally.
