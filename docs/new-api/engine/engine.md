> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Engine


<a id="engine-1"></a>

## engine  — global table


Returns information about the state of the engine.


  

### `engine.GetScreenSize`

```lua
engine.GetScreenSize(): Vector2D?
```

Returns the current render width and height in pixels as a new `Vector2D`. Changing the returned vector does not change the engine state. The render size can be different from the size of the game window. Returns **nil** if the engine state is not available.


  

### `engine.GetViewAngles`

```lua
engine.GetViewAngles(): QAngle
```

Returns a copy of the current view angles of the engine.


    
Changing this copy does not move the camera. To change the view angles, use
`input.InputPollContext:GetViewAngles` and `input.InputPollContext:SetViewAngles` in the
`events.input_poll` event. The value from `input.InputPollContext:GetViewAngles` includes
input changes that are not applied yet. This function returns the angles that the engine
has now.


  

  

### `engine.GetLevelName`

```lua
engine.GetLevelName(): string?
```

Returns the full name of the map that is loaded now. Returns nil if there is no network game client.


  

### `engine.GetLevelNameShort`

```lua
engine.GetLevelNameShort(): string?
```

Returns the short name of the map that is loaded now. Returns nil if there is no network game client.


  

### `engine.GetClientTick`

```lua
engine.GetClientTick(): integer?
```

Returns the current client tick. Returns nil if there is no network game client.


  

### `engine.GetServerTick`

```lua
engine.GetServerTick(): integer?
```

Returns the current server tick. Returns nil if there is no network game client.


  

### `engine.GetDisplayMode`

```lua
engine.GetDisplayMode(): engine.DisplayMode?
```

Returns the current display mode of the engine swap chain. Returns nil if the engine has no display mode.


    
Inside the `display_mode_changed` event, this function already returns the new mode.


  


## engine.DisplayMode — object type

A display mode copied from the engine. The object stays valid after the function or callback
that created it returns. All fields are read-only.


  

### `engine.DisplayMode.back_buffer_count`

The number of back buffers.


  

### `engine.DisplayMode.height`

The height of the mode in pixels.


  

### `engine.DisplayMode.high_dpi`

Whether the mode is marked as high DPI.


  

### `engine.DisplayMode.multisample`

The MSAA sample count. The value is 0 when multisampling is off.


  

### `engine.DisplayMode.refresh_rate`

The refresh rate in Hz in fullscreen. The value is 0 when the mode uses the default rate, for example in a window.


  

### `engine.DisplayMode.vsync`

Whether the game waits for vertical sync before it shows a frame.


  

### `engine.DisplayMode.width`

The width of the mode in pixels.


  

### `engine.DisplayMode.window_mode`

How the game window is shown.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "exclusive_fullscreen" |  |  |
| "fullscreen" |  |  |
| "borderless" |  |  |
| "windowed" |  |  |
| "unknown" |  |  |
