> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Trace


<a id="trace-1"></a>

## trace  — global table


Traces rays and shapes through the world and returns what they hit.


  

<a id="tracefilter"></a>
### `trace.Filter`

```lua
trace.Filter([ignore_entities: client.C_BaseEntity|client.C_BaseEntity[], interacts_with: uint64_t, collision_group: integer, object_set: integer]): trace.Filter
```

Creates a trace filter. You can give entities that the trace skips, and the layers, collision group and object types that the trace uses.


| Parameter | Type | Description |
| --- | --- | --- |
| ignore_entities? | `client.C_BaseEntity\|client.C_BaseEntity[]` | The entities that the trace skips. |
| interacts_with? | `uint64_t` | A bit mask of `trace.CONTENTS` layers that the trace hits. The default is the mask used for bullets, which is `SOLID`, `HITBOX`, `SKY`, `WINDOW`, `GRATE`, `PLAYER`, `NPC` and `DEBRIS`. |
| collision_group? | `integer` | The collision group of the trace. See `trace.BuiltInCollisionGroup_t` and `trace.StandardCollisionGroups_t`. The default is `CONDITIONALLY_SOLID`. |
| object_set? | `integer` | A bit mask of `trace.RnQueryObjectSet` object types that the trace checks. The default is `ALL`. |


    
To skip entities, pass one entity or a table of entities. Up to two entities are fast. Each
entity after the second makes traces slower.


  

  

<a id="tracefilter"></a>
### `trace.Filter`

```lua
trace.Filter(params: table): trace.Filter
```

Creates a trace filter from a table of settings. The keys of the table are the writable fields of `trace.Filter`.


| Parameter | Type | Description |
| --- | --- | --- |
| params | `table` | The filter settings, with field names as keys. |


    
Fields that you do not set keep the values of an empty filter. In an empty filter,
`interacts_with` is `0`, so the trace hits nothing. `collision_group` is `CONDITIONALLY_SOLID`
and `object_set_mask` is `ALL`.


  

  

### `trace.Ray`

```lua
trace.Ray(startpos: Vector, endpos: Vector, filter: trace.Filter): trace.Trace
```

Traces a ray, which is a single point, from `startpos` to `endpos`.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the ray. |
| endpos | `Vector` | The end position of the ray. |
| filter | `trace.Filter` | The filter that decides which objects and layers the trace hits. |


  

### `trace.Sphere`

```lua
trace.Sphere(startpos: Vector, endpos: Vector, radius: number, filter: trace.Filter): trace.Trace
```

Moves a sphere from `startpos` to `endpos` and returns what it hits.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the center of the sphere. |
| endpos | `Vector` | The end position of the center of the sphere. |
| radius | `number` | The radius of the sphere in units. |
| filter | `trace.Filter` | The filter that decides which objects and layers the trace hits. |


  

### `trace.Capsule`

```lua
trace.Capsule(startpos: Vector, endpos: Vector, p1: Vector, p2: Vector, radius: number, filter: trace.Filter): trace.Trace
```

Moves a capsule from `startpos` to `endpos` and returns what it hits. The end points of the capsule are relative to the position of the moving capsule.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the trace. |
| endpos | `Vector` | The end position of the trace. |
| p1 | `Vector` | The first end point of the line segment inside the capsule. |
| p2 | `Vector` | The second end point of the line segment inside the capsule. |
| radius | `number` | The radius of the capsule in units. |
| filter | `trace.Filter` | The filter that decides which objects and layers the trace hits. |


  

### `trace.AABB`

```lua
trace.AABB(startpos: Vector, endpos: Vector, mins: Vector, maxs: Vector, filter: trace.Filter): trace.Trace
```

Moves an axis aligned box from `startpos` to `endpos` and returns what it hits. The corners of the box are relative to the position of the moving box.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the origin of the box. |
| endpos | `Vector` | The end position of the origin of the box. |
| mins | `Vector` | The minimum corner of the box, relative to the origin. |
| maxs | `Vector` | The maximum corner of the box, relative to the origin. |
| filter | `trace.Filter` | The filter that decides which objects and layers the trace hits. |


  

### `trace.ConvexHull`

```lua
trace.ConvexHull(startpos: Vector, endpos: Vector, verts: Vector[], filter: trace.Filter): trace.Trace
```

Moves a convex hull from `startpos` to `endpos` and returns what it hits. The vertices are relative to the position of the moving hull.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the origin of the hull. |
| endpos | `Vector` | The end position of the origin of the hull. |
| verts | `Vector[]` | A table of points that are the vertices of the convex hull. |
| filter | `trace.Filter` | The filter that decides which objects and layers the trace hits. |


  

### `trace.Bullet`

```lua
trace.Bullet(startpos: Vector, endpos: Vector, attacker: client.C_CSPlayerPawn[, vdata: client.CCSWeaponBaseVData, filter: trace.Filter]): trace.Trace
```

Simulates a bullet and calculates its damage through surfaces and penetration. This function does not fire a shot.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start position of the bullet. |
| endpos | `Vector` | A position that sets the direction of the bullet. |
| attacker | `client.C_CSPlayerPawn` | The player pawn that shoots the bullet. |
| vdata? | `client.CCSWeaponBaseVData` | The weapon data for penetration and damage falloff. Pass nil to use the data of the active weapon of the attacker. |
| filter? | `trace.Filter` | The filter that sets which objects and layers the bullet can hit. Pass nil to use a filter that ignores the attacker. |


| Return | Type | Description |
| --- | --- | --- |
| ... | `trace.Trace` | One value for each impact. Returns no values if there are no impacts. |


    
The bullet starts at `startpos` and moves in the direction of `endpos`. It travels the full
range of the weapon, so it can go past `endpos`. It can penetrate up to 4 surfaces.

Returns one value for each impact, starting with the first impact. Use `{trace.Bullet(...)}`
to put the values in a table. Throws an error if there is no weapon data.


  

  

### `trace.IntersectCapsule`

```lua
trace.IntersectCapsule(startpos: Vector, endpos: Vector, p1: Vector, p2: Vector, radius: number): number?, Vector?
```

Tests whether the segment from `startpos` to `endpos` hits a capsule in world space.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start of the segment. |
| endpos | `Vector` | The end of the segment. |
| p1 | `Vector` | The center of the first end of the capsule in world space. |
| p2 | `Vector` | The center of the second end of the capsule in world space. |
| radius | `number` | The radius of the capsule. |


| Return | Type | Description |
| --- | --- | --- |
| fraction | `number?` | The position of the first contact on the segment, from 0 to 1. |
| hitpos | `Vector?` | The first contact point. |


    
This function only does math on the shape. It does not check the world, so it works for
shapes that do not exist in the game, at any position and rotation. To rotate a capsule,
transform the centers of its ends, for example with
`CTransform(origin, rotation):TransformVector(Vector(0, 0, 8))`.

Returns **nil** if the segment does not hit the capsule. A fraction of 0 means that `startpos`
is already inside the capsule.

You can pass the capsule of a hitbox directly, for example
`trace.IntersectCapsule(startpos, endpos, hitbox:GetCapsule())`.

World geometry is ignored. To check whether a bullet reaches the shape, compare the fraction
with the result of `trace.Ray` or `trace.Bullet` for the same segment.


  

  

### `trace.IntersectSphere`

```lua
trace.IntersectSphere(startpos: Vector, endpos: Vector, center: Vector, radius: number): number?, Vector?
```

Tests whether the segment from `startpos` to `endpos` hits a sphere in world space. In the same way as `trace.IntersectCapsule`, this function only does math on the shape and does not check the world.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector` | The start of the segment. |
| endpos | `Vector` | The end of the segment. |
| center | `Vector` | The center of the sphere in world space. |
| radius | `number` | The radius of the sphere. |


| Return | Type | Description |
| --- | --- | --- |
| fraction | `number?` | The position of the first contact on the segment, from 0 to 1. |
| hitpos | `Vector?` | The first contact point. |


    
Returns **nil** if the segment does not hit the sphere. A fraction of 0 means that `startpos`
is already inside the sphere.


  

  

### `trace.CONTENTS`

The interaction layer bits for the `interacts_with`, `interacts_as` and `interacts_exclude` fields of a trace filter. Use `bit.bor` to combine bits, or use a predefined `trace.MASK`.


    

### `trace.CONTENTS`


| Name | Value | Description |
| --- | --- | --- |
| TEAM1 | 2147483648 | Geometry for team 1 only |
| TEAM2 | 4294967296 | Geometry for team 2 only |
| GRENADECLIP | 8589934592 | Invisible barriers that block grenade movement |
| DRONECLIP | 17179869184 | Invisible barriers that block drone movement |
| MOVEABLE | 34359738368 | Moveable physics objects |
| OPAQUE | 68719476736 | Opaque surfaces that block visibility |
| MONSTER | 137438953472 | Collision bodies of monsters and bots |
| CHICKEN | 274877906944 | Collision bodies of chickens |
| THROWN_GRENADE | 549755813888 | Thrown grenades in flight |
| DROPPED_HOSTAGE | 1099511627776 | Collision bodies of dropped hostages |
| EMPTY | 0 | No contents |
| SOLID | 1 | Solid world geometry |
| HITBOX | 2 | Player and entity hitboxes |
| TRIGGER | 4 | Trigger volumes |
| SKY | 8 | Sky geometry |
| PLAYER_CLIP | 16 | Player movement clip brushes |
| NPC_CLIP | 32 | NPC movement clip brushes |
| BLOCK_LOS | 64 | Line-of-sight blockers |
| BLOCK_LIGHT | 128 | Light blockers |
| LADDER | 256 | Climbable ladder surfaces |
| PICKUP | 512 | Item pickup volumes |
| BLOCK_SOUND | 1024 | Sound propagation blockers |
| NODRAW | 2048 | Non-rendered surfaces |
| WINDOW | 4096 | Breakable glass windows |
| GRATE | 8192 | Grates and bars |
| WORLD_GEOMETRY | 16384 | Standard world brush geometry |
| WATER | 32768 | Water volumes |
| SLIME | 65536 | Slime and toxic liquid volumes |
| TOUCH_TRIGGERS | 131072 | Touch-only trigger volumes |
| PLAYER | 262144 | Player collision bodies |
| NPC | 524288 | NPC collision bodies |
| DEBRIS | 1048576 | Debris and gibs |
| PHYSICS_PROP | 2097152 | Physics prop bodies |
| NAV_IGNORE | 4194304 | Ignored by nav mesh generation |
| NAV_LOCAL_IGNORE | 8388608 | Locally ignored by nav mesh generation |
| POSTPROCESSING_VOLUME | 16777216 | Post-processing effect volumes |
| UNUSED3 | 33554432 | Unused |
| CARRIED_OBJECT | 67108864 | Objects currently being carried by a player |
| PUSHAWAY | 134217728 | Objects that push players away on contact |
| SERVER_ENTITY_ON_CLIENT | 268435456 | Server-side entity replicated to the client |
| CARRIED_WEAPON | 536870912 | Weapons currently carried by a player |
| STATIC_LEVEL | 1073741824 | Static level geometry |


  

  

### `trace.MASK`

Predefined combinations of `trace.CONTENTS` bits for common traces.


    

### `trace.MASK`


| Name | Value | Description |
| --- | --- | --- |
| PLAYERSOLID_BRUSHONLY | 34359750673 | Brush geometry that is solid for players, including team geometry |
| FLOORTRACE | 34360791041 | Finds floor surfaces that players can walk on |
| VISIBLE | 1 | Visible solid geometry only |
| BLOCKLOS | 66 | Surfaces that block line of sight |
| OPAQUE | 128 | Surfaces that block light |
| NPCWORLDSTATIC_FLUID | 4129 | NPC world static geometry including fluid |
| SOLID_BRUSHONLY | 12289 | Solid brush geometry only, no entities |
| DEFAULTPLAYERSOLID_BRUSHONLY | 12305 | Default player-solid brush geometry only |
| NPCWORLDSTATIC | 12321 | NPC world static geometry |
| NPCSOLID_BRUSHONLY | 12321 | NPC-solid brush geometry only |
| WATER | 98304 | Water and slime volumes |
| VISIBLE_AND_NPCS | 524289 | Visible geometry and NPC bodies |
| BLOCKLOS_AND_NPCS | 524354 | Line-of-sight blockers and NPC bodies |
| OPAQUE_AND_NPCS | 524416 | Opaque surfaces and NPC bodies |
| SOLID | 798721 | All solid surfaces including players and NPCs |
| DEFAULTPLAYERSOLID | 798737 | Default solid mask for player movement |
| NPCSOLID | 798753 | Default solid mask for NPC movement |
| SHOT_BRUSHONLY | 1052673 | Brush surfaces only for bullet traces |
| SHOT | 1839107 | Full bullet trace mask including players, NPCs, and debris |
| SHOT_HULL | 1847297 | Hull-based shot mask for grenades and larger projectiles |
| ALL | 0xFFFFFFFFFFFFFFFF | All layers |


  

  

### `trace.RnQueryObjectSet`

The object types that a trace checks. Use them for the `object_set` argument of `trace.Filter` and for the `object_set_mask` field of a filter. Use `bit.bor` to combine bits.


    

### `trace.RnQueryObjectSet`


| Name | Value | Description |
| --- | --- | --- |
| STATIC | 1 | Static world geometry |
| KEYFRAMED | 2 | Keyframed bodies, which are animated |
| DYNAMIC | 4 | Dynamic physics bodies |
| LOCATABLE | 8 | Locatable bodies |
| ALL_GAME_ENTITIES | 14 | Every entity body, which means keyframed, dynamic and locatable bodies |
| ALL | 15 | Static geometry and every entity body |
| KEYFRAMED_ONLY | 2 | Keyframed bodies only |
| DYNAMIC_ONLY | 4 | Dynamic bodies only |


    


**Note:** 
The members and their values depend on the game build. `STATIC`, `DYNAMIC`,
`ALL_GAME_ENTITIES`, `ALL`, `KEYFRAMED_ONLY` and `DYNAMIC_ONLY` exist in every build.


  

  

### `trace.BuiltInCollisionGroup_t`

The collision groups that the engine defines for every game. Use them for the `collision_group` argument of `trace.Filter` and for the `collision_group` field of a filter.


    

### `trace.BuiltInCollisionGroup_t`


| Name | Value | Description |
| --- | --- | --- |
| ALWAYS | 0 | Collides with everything |
| NONPHYSICAL | 1 | Non-physical objects |
| TRIGGER | 2 | Trigger volumes |
| CONDITIONALLY_SOLID | 3 | Solid depending on the other object. This is the default group of a trace |
| FIRST_USER | 4 | First group a game may define |
| COLLISION_GROUPS_MAX_ALLOWED | 64 | Number of group slots |


  

  

### `trace.StandardCollisionGroups_t`

The collision groups that Source 2 games share. Their values start at the value of `BuiltInCollisionGroup_t.FIRST_USER`.


    

### `trace.StandardCollisionGroups_t`


| Name | Value | Description |
| --- | --- | --- |
| DEFAULT | 4 | Default entity collision |
| DEBRIS | 5 | Debris that collides with the world only |
| INTERACTIVE_DEBRIS | 6 | Debris that also collides with players |
| INTERACTIVE | 7 | Interactive entities |
| PLAYER | 8 | Player bodies |
| BREAKABLE_GLASS | 9 | Breakable glass |
| VEHICLE | 10 | Vehicles |
| PLAYER_MOVEMENT | 11 | Player movement traces |
| NPC | 12 | NPC bodies |
| IN_VEHICLE | 13 | Players inside vehicles |
| WEAPON | 14 | Weapons |
| VEHICLE_CLIP | 15 | Vehicle clip brushes |
| PROJECTILE | 16 | Projectiles |
| DOOR_BLOCKER | 17 | Door blockers |
| PASSABLE_DOOR | 18 | Doors players can pass through |
| DISSOLVING | 19 | Dissolving entities |
| PUSHAWAY | 20 | Objects that push players away |
| NPC_ACTOR | 21 | NPC actors |
| NPC_SCRIPTED | 22 | Scripted NPCs |
| PZ_CLIP | 23 | PZ clip brushes |
| PROPS | 24 | Props |
| LAST_SHARED_COLLISION_GROUP | 25 | First group specific to a game |


  


## trace.Trace — object type

The result of a trace. All trace functions return it. It describes what the trace hit and
where. All fields are read-only.


  

### `trace.Trace.attributes`

The collision attributes of the shape that was hit.


  

### `trace.Trace.body`

The physics body that was hit.


  

### `trace.Trace.contents`

A bit mask of the interaction layers at the hit point, as `trace.CONTENTS` bits.


  

### `trace.Trace.damage`

The damage after the surface and penetration modifiers are applied.


  

### `trace.Trace.damage_is_valid`

True if the damage fields have values.


  

### `trace.Trace.damage_unscaled`

The damage before any modifiers are applied.


  

### `trace.Trace.endpos`

The position where the trace ended. If something was hit, this is the point of impact. If nothing was hit, this is the end position that you passed.


  

### `trace.Trace.enthit`

The entity that was hit. It is **nil** if only world geometry was hit.


  

### `trace.Trace.fraction`

How far along the trace the hit happened. `0` is the start. `1` means that nothing was hit, or that the hit is at the end.


  

### `trace.Trace.hitbox`

The hitbox that was hit. It is **nil** if the hitbox cannot be found on the entity that was hit.


  

### `trace.Trace.hitpos`

The exact point of contact on the surface that was hit.


  

### `trace.Trace.hitpos_is_valid`

`true` if the `hitpos` field holds valid data.


  

### `trace.Trace.normal`

The normal of the surface at the hit point.


  

### `trace.Trace.offset`

The plane constant of the plane that was hit. It is the dot product of the normal and a position on the plane.


  

### `trace.Trace.physicsbone`

The index of the physics bone, for skeletal meshes.


  

### `trace.Trace.shape`

The physics shape that was hit.


  

### `trace.Trace.startpos`

The start position of the trace.


  

### `trace.Trace.startsolid`

`true` if the trace started inside solid geometry.


  

### `trace.Trace.surface`

The surface properties of the surface that was hit, such as friction and density.


  

### `trace.Trace.transform`

The transform of the shape that was hit.


  

### `trace.Trace.triangle`

The index of the face or triangle on the surface that was hit. It is `-1` if there is no such index.


  

### `trace.Trace.type`

The type of shape that was traced. `0` is a ray, `1` is a sphere, `2` is a box, `3` is a capsule and `4` is a hull.


## trace.Filter — object type

Decides which objects and interaction layers a trace collides with.

`ignore_entities` and `should_hit_entity` are write-only. Reading them throws an error. Writing a
field that does not exist also throws an error.

`ignore_entities` takes a table of entities. Up to two entities are fast. Each entity after the
second makes traces slower. Setting `ignore_entities` again replaces the entities that were set
before.


  

### `trace.Filter.collision_group`

The collision group of the trace. See `trace.BuiltInCollisionGroup_t` and `trace.StandardCollisionGroups_t`.


  

### `trace.Filter.ignore_entities`

Write-only. A table of entities that the trace skips. Up to two entities are fast. Each entity after the second makes traces slower.


  

### `trace.Filter.interacts_as`

A bit mask of the layers that the trace itself belongs to. Other objects collide with the trace as these layers.


  

### `trace.Filter.interacts_exclude`

A bit mask of the layers that the trace never collides with.


  

### `trace.Filter.interacts_with`

A bit mask of the interaction layers that the trace hits.


  

### `trace.Filter.object_set_mask`

A bit mask of the `trace.RnQueryObjectSet` object types that the trace checks.


  

### `trace.Filter.should_hit_entity`

Write-only. A function that is called for each entity that the trace touches. Return `true` to hit the entity. Return `false` or any other value to skip it. Setting this function makes traces slower.
