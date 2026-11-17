> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Events


<a id="events-1"></a>

## events  — global table


Runs your functions when something happens in the cheat or in the game. Index `events` with
the name of an event to get an `events.Event` object for it. Call `events.<name>:Set(fn)` to
add a callback, and call `events.<name>:Unset(fn)` to remove it.

Every name returns an event object. So a misspelled name does not throw an error, but its
callback never runs.

There are three kinds of events.

**Cheat events** come from the cheat itself. Some are about the cheat, such as `render`,
`shutdown`, `config_state` and `mouse_input`. Others come from the game loop, such as
`createmove`, `pre_movement`, `override_view` and `entity_created`. Each event passes its own
arguments. They are listed on [Cheat Events](../events/cheat.md).

**Game events** are the game events of the engine, under their engine names, such as
`player_death`, `round_start` and `bomb_planted`. The callback receives one table with the
fields of the event. The fields are listed on [Game Events](../events/game.md).
A player field such as `userid` holds the player entity, or **nil** if the entity is not
available. `userid_raw` always holds the raw value from the engine.

**Custom events** use any other name. Scripts in the same runtime use them to send data to each
other. `events.<name>:Fire(...)` passes its arguments to every callback that is set on that
name.

The example adds a menu toggle that turns a `render` callback on and off. The callback is a
named function that is defined once, because `Unset` removes only the same function that `Set`
added.

```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/runtime/events:0:1b4a03b2654b"
local font = render.LoadFont(render.EspFont.kRegular)
local watermark = ui.AddTab("Lua"):AddGroup("Example"):AddToggle("Watermark")

local function draw_watermark()
    render.DrawText(Vector2D(16, 16), Color(255, 255, 255), font, nil, "neverlose")
end

watermark:AddCallback(function(toggle)
    if toggle:Get() then
        events.render:Set(draw_watermark)
    else
        events.render:Unset(draw_watermark)
    end
end, true) -- `true` also runs it once now, for the toggle's current value
```


  

### `events[string]`


  

<a id="events-Event"></a>
### `events.Event`

The object that `events.<name>` returns for one event name. `T` is the type of the callback of that event. The [Cheat Events](../events/cheat.md) and [Game Events](../events/game.md) pages list it for each event. The callback of a custom event receives the values that are passed to `Fire`.


    
The object does not store anything. Each time you index `events`, you get a new object, and
two objects for the same name are equal. Callbacks belong to the script that set them, and
they are removed when the script is unloaded. If one callback throws an error, the error is
printed and the other callbacks still run.

`event:Set(callback)` starts calling `callback` each time the event fires.

`event:Unset(callback)` stops calling it. You must pass the same function value that you
passed to `Set`. A new function with the same code is a different function.

`event:Fire(...)` fires a custom event.

You can also call the object directly. `event(callback)` and `event(callback, true)` set the
callback, and `event(callback, false)` removes it.


  


## events.Event.Traits — object type

The methods of every `events.Event`.


  

### `events.Event.Traits:Fire`

```lua
events.Event.Traits:Fire([...: any]): boolean
```

Fires a custom event. Every callback that scripts in the same runtime set on this name is called with `...`. Returns `true` when the event was fired.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` |  |


    
If the name belongs to an event that the cheat fires itself, the function does nothing and
returns `false`. These names include `render`, `mouse_input`, `shutdown`, `config_state` and
the game events. Use a name of your own for custom events.

The first time this happens for a name, a warning is also added to the errors of the script.


  

  

### `events.Event.Traits:Set`

```lua
events.Event.Traits:Set(callback: T)
```

Adds a callback that runs each time this event fires. If this script already set the same callback, nothing happens.


| Parameter | Type | Description |
| --- | --- | --- |
| callback | `T` |  |


  

### `events.Event.Traits:Unset`

```lua
events.Event.Traits:Unset(callback: T)
```

Removes a callback that this script set for this event. Pass the same function that you passed to `Set`.


| Parameter | Type | Description |
| --- | --- | --- |
| callback | `T` |  |
