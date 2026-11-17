> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Particles


## particles.Create.Options — object type

Options for `particles.Create`. If a field has a value that is not in its enum, an error is
thrown.


  

### `particles.Create.Options.attachment`

How control point 0 is placed. Defaults to `WORLDORIGIN`. The values `POINT`, `POINT_FOLLOW`, `CUSTOMORIGIN` and `CUSTOMORIGIN_FOLLOW` throw an error here. To use them, create the effect with another value, and then bind the point with `SetEntity`.


  

### `particles.Create.Options.check_fow`

Whether the effect is hidden in fog of war, in the same way as the effects of the game. Defaults to `true`.


  

### `particles.Create.Options.create_pvs`

Whether the scene objects of the effect take part in visibility culling. Defaults to `true`.


  

### `particles.Create.Options.entity`

The entity that the effect is attached to. It is required for every `attachment` value except `WORLDORIGIN`. An invalid entity throws an error.


  

### `particles.Create.Options.lifespan`

The number of seconds until the effect is destroyed. The end cap of the effect is played when it is destroyed. The default is `0`, which means that the effect never expires. A negative value throws an error.


## particles.Particle — object type

A particle effect that was created by this script.

The effect is not destroyed when the last reference to this object is gone. The effect runs
until you call `Destroy`, until its `lifespan` ends, until the script unloads, or until the map
ends. After that, every method returns `false` or `nil`.


  

### `particles.Particle:IsValid`

```lua
particles.Particle:IsValid(): boolean
```

Returns whether the effect is still alive and owned by this object.


  

### `particles.Particle:GetName`

```lua
particles.Particle:GetName(): string?
```

Returns the path of the resource that the effect was created from. Returns `nil` after the effect is gone.


  

### `particles.Particle:SetControlPoint`

```lua
particles.Particle:SetControlPoint(point: integer, position: Vector): boolean
```

Moves a control point. The orientation of the point is reset to the identity rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| point | `integer` | The control point, from `0` to `63`. Any other value throws an error. |
| position | `Vector` | The position in world space. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the effect is gone. |


  

### `particles.Particle:SetTransform`

```lua
particles.Particle:SetTransform(point: integer, transform: CTransform[, interpolation: number]): boolean
```

Sets the position and the orientation of a control point.


| Parameter | Type | Description |
| --- | --- | --- |
| point | `integer` | The control point, from `0` to `63`. Any other value throws an error. |
| transform | `CTransform` | The transform in world space. |
| interpolation? | `number` | The number of seconds to blend from the current value to the new value. Defaults to `0`. A negative value throws an error. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the effect is gone. |


  

### `particles.Particle:SetEntity`

```lua
particles.Particle:SetEntity(point: integer, entity: Entity[, attachment: particles.Attachment, attachment_name: string]): boolean
```

Binds a control point to an entity. An invalid entity throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| point | `integer` | The control point, from `0` to `63`. Any other value throws an error. |
| entity | `Entity` | The entity to follow. |
| attachment? | `particles.Attachment` | How the point follows the entity. Defaults to `ABSORIGIN_FOLLOW`. |
| attachment_name? | `string` | The name of the attachment on the model. It is required for `POINT` and `POINT_FOLLOW`, and a missing or empty name throws an error for them. It is ignored for the other values. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the effect is gone. |


  

### `particles.Particle:SetPath`

```lua
particles.Particle:SetPath(point: integer, points: Vector[]): boolean
```

Sets the shape of a rope or trail effect from a list of points. This works for effects that read a particle snapshot from a control point. For example, the effect `"particles/entity/spectator_utility_trail.vpcf"` reads it from control point `0`.


| Parameter | Type | Description |
| --- | --- | --- |
| point | `integer` | The control point for the snapshot, from `0` to `63`. Any other value throws an error. |
| points | `Vector[]` | The points in world space, in order. At least 2 points are required, and fewer points throw an error. Points after the maximum particle count of the effect spawn nothing. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the effect is gone. |


    
Each call replaces the points of the previous call. The effect decides when it reads the
points. Most effects, including the spectator trail, copy the points only when particles
spawn. A later call does not move particles that are already alive. Point `i` gets a creation
time of `(i - 1) / (#points - 1)`.

The effect gets one particle for each point. The spectator trail scales the width of each
particle by its index along the path. Because of this, a path with only two points draws
nothing that you can see. Split a straight line into 16 to 24 points.

The spectator trail draws a beam once. Control point `3` holds the particle life in seconds,
the width and the alpha. Control point `16` holds the colour. The alpha of a particle grows
with its age. Its width grows during the first half of its life and shrinks to zero during the
second half. Give the effect a `lifespan` that is a little longer than the particle life.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/particles:0:bdd7e82b4f31"
local from, to = Vector(0, 0, 64), Vector(256, 0, 64)
local points = {}
for i = 0, 23 do
    local t = i / 23
    points[#points + 1] = from + (to - from) * t
end
local beam = particles.Create("particles/entity/spectator_utility_trail.vpcf", { lifespan = 2.3 })
if beam then
    beam:SetPath(0, points)
    beam:SetControlPoint(16, Vector(255, 0, 0)) -- color
    beam:SetControlPoint(3, Vector(2, 0.4, 1))  -- particle life, width, alpha
end
```


  

  

### `particles.Particle:Destroy`

```lua
particles.Particle:Destroy([play_endcap: boolean]): boolean
```

Destroys the effect.


| Parameter | Type | Description |
| --- | --- | --- |
| play_endcap? | `boolean` | Whether the effect plays its end sequence first. Defaults to `true`. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the effect was already gone. |


<a id="particles-1"></a>

## particles  — global table


Creates and controls particle effects. The game simulates and renders the effects.

A script can have at most 256 effects alive at the same time. Creating one more throws an
error.


  

### `particles.Create`

```lua
particles.Create(path: string[, options: particles.Create.Options]): particles.Particle?
```

Creates a particle effect from a compiled `.vpcf` resource.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path of the resource, for example `"particles/entity/spectator_utility_trail.vpcf"`. |
| options? | `particles.Create.Options` | The options for the attachment and the lifetime of the effect. |


    
Returns `nil` when the client is not in a game or when the resource cannot be found. Throws an
error if another script registered the name with `particles.Register`.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/particles:1:0ee9dbd59084"
local fx = particles.Create("particles/entity/spectator_utility_trail.vpcf", { lifespan = 3 })
if fx then fx:SetControlPoint(0, Vector(0, 0, 64)) end
```


  

  

### `particles.Register`

```lua
particles.Register(name: string, bytes: string): boolean, string?
```

Loads a compiled particle system from memory, so that `particles.Create(name)` can use it. Use this function to add an effect that the game does not have, such as a rope that stays in the world.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the resource in the form `particles/<path>.vpcf`, with at most 255 characters. Any other name throws an error. |
| bytes | `string` | The data of the compiled particle system. An empty string throws an error. |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` | `true` if the particle system was loaded. |
| reason | `string?` | The reason why the loading failed, if `ok` is `false`. |


    
`bytes` must be a compiled CS2 particle system, which is the content of a `.vpcf_c` file. Bad
data can crash the game.

The name must not be used by any resource of the game. A name that a script registered before
it unloaded can be registered again. A name that is already registered throws an error.

The registration belongs to this script. Only this script can create effects from the name.
When the script unloads, those effects are removed without their end cap and the resource is
freed.

A script can register at most 32 particle systems. Each one can be at most 4 MB. Going over
either limit throws an error.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/particles:2:b3060b0a4590"
local ok, err = particles.Register("particles/my_script/rope.vpcf", require("rope_bytes"))
if not ok then print(err) return end

local rope = particles.Create("particles/my_script/rope.vpcf")
if rope then rope:SetPath(0, { Vector(0, 0, 64), Vector(256, 0, 64) }) end
```


  

  

<a id="particles-Attachment"></a>
### `particles.Attachment`

How an effect or a control point follows its entity.


    

### `particles.Attachment`


| Name | Value | Description |
| --- | --- | --- |
| ABSORIGIN | 0 | At the origin of the entity when the effect is created. |
| ABSORIGIN_FOLLOW | 1 | Follows the origin of the entity. |
| CUSTOMORIGIN | 2 | At a custom origin when the effect is created. |
| CUSTOMORIGIN_FOLLOW | 3 | Follows a custom origin. |
| POINT | 4 | At a named attachment when the effect is created. |
| POINT_FOLLOW | 5 | Follows a named attachment. |
| EYES_FOLLOW | 6 | Follows the eyes of the entity. |
| OVERHEAD_FOLLOW | 7 | Follows a point above the entity. |
| WORLDORIGIN | 8 | In world space. The script sets the control points. |
| ROOTBONE_FOLLOW | 9 | Follows the root bone. |
| RENDERORIGIN_FOLLOW | 10 | Follows the render origin of the entity. |
| CENTER_FOLLOW | 13 | Follows the center of the entity. |
