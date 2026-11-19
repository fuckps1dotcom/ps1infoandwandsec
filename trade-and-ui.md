# Trade and UI Notes

## Trade Invoke Patterns

```lua
:InvokeServer(Func, ...)
```

### Ready

```lua
:InvokeServer("Ready", TradeId)
```

This only works for the player's own trade.

### Cancelling

```lua
:InvokeServer("Cancel", TradeId)
```

This can cancel another player's trade.

### InvIgnore

```lua
:InvokeServer("InvIgnore", TradeId)
```

This receives a message saying the other player declined the trade, even after accepting, and cancels immediately afterward.

When investigating trade behavior, monitor:

```lua
m_Library.Remotes.TradeUpdate
```

## Rejoin and UI Cache Behavior

After rejoining, the UI may break because local stat data is not updated. This is not necessarily a UI issue.

For UI updates:

```lua
game:GetService("Players").LocalPlayer.PlayerGui.Events.StatChanged:Fire()
```

The game then checks the cache inside:

```lua
require(Library).Stats
```

This cache is different from:

```lua
require(game.StarterGui.Modules['3 | Stats'])
```

The client uses `require(Library).Stats`. If the player rejoins the same server, this cache stops updating and `StatChanged` stops firing.

## Inventory UI Refresh

```lua
-- game:GetService("Players").LocalPlayer.PlayerGui.Inventory.Frame.Pets:ClearAllChildren()
wait(1)
getsenv(game:GetService("Players").LocalPlayer.PlayerGui.Scripts.GUIs.Inventory).loadDisplay()
```
