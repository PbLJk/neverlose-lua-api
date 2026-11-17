> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Sounds


## sounds.PlayEvent.Options — object type

Options for `sounds.PlayEvent`.


  

### `sounds.PlayEvent.Options.lifetime`

The time in seconds until the emitter is removed. The default is `30`. Pass `0` to keep the emitter until you call `Destroy`, the script unloads, or the map ends. Use `0` for looping sounds. A negative value throws an error.


  

### `sounds.PlayEvent.Options.stop_on_new`

Whether to stop the previous event when the emitter starts again. The default is `false`.


## sounds.Sound — object type

A soundevent that this script started at a world position.

The sound does not stop when no variable refers to this object anymore. It plays until you
call `Destroy`, its `lifetime` ends, the script unloads, or the map ends. After that, every
method returns `false` or `nil`.

The game does not tell when a sound that plays once has finished, so `IsValid` returns `true`
until one of the events above happens.


  

### `sounds.Sound:IsValid`

```lua
sounds.Sound:IsValid(): boolean
```

Returns whether the sound still plays from the emitter of this object.


  

### `sounds.Sound:GetName`

```lua
sounds.Sound:GetName(): string?
```

Returns the name of the soundevent that started the sound. Returns `nil` after the sound is removed.


  

### `sounds.Sound:SetOrigin`

```lua
sounds.Sound:SetOrigin(origin: Vector): boolean
```

Moves the emitter to a new position. A looping sound moves with the emitter. A sound that plays once and has finished does not play again. Throws an error if `origin` is not a finite vector.


| Parameter | Type | Description |
| --- | --- | --- |
| origin | `Vector` | The position in world space. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the sound was already removed. |


  

### `sounds.Sound:Destroy`

```lua
sounds.Sound:Destroy(): boolean
```

Stops the sound and removes its emitter.


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the sound was already removed. |


<a id="sounds-1"></a>

## sounds  — global table


Plays sound files in 2D and soundevents at world positions.

A script can have at most 32 world space sounds at the same time.


  

### `sounds.PlayFile`

```lua
sounds.PlayFile(path: string[, volume: number])
```

Plays a sound file by name in 2D. The volume is multiplied by the master volume of the game.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The name or path of the sound file. |
| volume? | `number` | The volume from `0` to `1`. The default is `1`. |


    
The file must be in a sound search path of the game. A sound file cannot play at a world
position. To play a sound at a world position, use `sounds.PlayEvent` with a soundevent.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/sounds:0:f9b06593884d"
sounds.PlayFile("hitmarker", 0.5)
```


  

  

### `sounds.PlayEvent`

```lua
sounds.PlayEvent(event: string, origin: Vector[, options: sounds.PlayEvent.Options]): sounds.Sound?
```

Plays a soundevent at a world position. The definition of the event sets its volume and falloff. The game changes the direction and the volume of the sound by the position of the listener, in the same way as for other world sounds.


| Parameter | Type | Description |
| --- | --- | --- |
| event | `string` | The name of the soundevent. |
| origin | `Vector` | The position in world space. |
| options? | `sounds.PlayEvent.Options` | The lifetime options. |


    
Only soundevents can play at a world position, for example `"Weapon_AK47.Single"` or
`"Inferno.Loop"`. The sound file names that `sounds.PlayFile` takes do not work here.

Returns `nil` outside a game, for an unknown soundevent, or when the game cannot create the
emitter in this frame. Throws an error if `event` is empty, `origin` is not a finite vector,
`options` is not a table, or the script already has 32 sounds.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/sounds:1:5273519775ed"
local pawn = entity.GetLocalPlayerPawn()
if pawn then
    local origin = pawn:GetAbsOrigin()
    sounds.PlayEvent("Weapon_AK47.Single", origin + Vector(300, 0, 0))

    local loop = sounds.PlayEvent("Inferno.Loop", origin, { lifetime = 0 })
    events.render:Set(function()
        if loop and loop:IsValid() and pawn:IsValid() then loop:SetOrigin(pawn:GetAbsOrigin()) end
    end)
end
```
