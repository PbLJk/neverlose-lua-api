> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Entity System


## entity — global table

Adds functions for game entities to the engine `entity` namespace. They find the local
player, list the players, and return the game rules and weapon data.

Use this table to choose the function that returns the pawn you need.

| Need                                                                                      | Call                                                |
| ----------------------------------------------------------------------------------------- | --------------------------------------------------- |
| The pawn that you move and shoot with, which is your own pawn or the bot that you control | `GetLocalPlayerPawn()`                              |
| Your own player pawn, also while you control a bot                                        | `GetOwnLocalPlayerPawn()`                           |
| The pawn that the controller points to, which can be an observer pawn                     | `GetLocalPawn()`                                    |
| A pawn that you control and that is not your own                                          | `GetLocalControlledPawn()`                          |
| The player that you spectate                                                              | `GetObservedPawn()`                                 |
| The pawn that the camera renders from                                                     | `GetViewPawn()`                                     |
| The player that you spectate in some observer modes, and your pawn in other cases         | `GetLocalOrObservedPawn()`, `GetLocalOrInEyePawn()` |

`GetLocalPlayerController()` always returns your controller. `GetLocalObserverPawn()` returns
your own observer entity. It can exist while you play, and it is never the player that you
spectate.

A pawn can be missing during a transition, and it can be dead. Get the pawn again in every
callback, and call `pawn:IsAlive()` when you need a living player.


  

### `entity.LookupByIndex`

```lua
entity.LookupByIndex(index: integer): client.C_BaseEntity?
```

Returns the entity with the given entity index. Returns **nil** if no entity has this index.


| Parameter | Type | Description |
| --- | --- | --- |
| index | `integer` | The entity index. |


  

### `entity.LookupByHandle`

```lua
entity.LookupByHandle(handle: integer): client.C_BaseEntity?
```

Returns the entity with the given handle. Returns **nil** if the handle is not valid, or if the entity of the handle was deleted.


| Parameter | Type | Description |
| --- | --- | --- |
| handle | `integer` | The entity handle. |


    
A handle always refers to one entity. If a new entity later gets the same index, the old
handle does not return the new entity.


  

  

### `entity.LookupPlayerControllerBySlot`

```lua
entity.LookupPlayerControllerBySlot(slot: integer): client.CBasePlayerController?
```

Returns the player controller in the given player slot. Returns **nil** if the slot is empty. Throws an error if the slot is less than `-1` or greater than `64`.


| Parameter | Type | Description |
| --- | --- | --- |
| slot | `integer` | The index of the player slot. |


  

### `entity.LookupPlayerControllerByUserId`

```lua
entity.LookupPlayerControllerByUserId(userid: integer): client.CBasePlayerController?
```

Returns the player controller of the player with the given user ID. Returns **nil** if no player has this ID.


| Parameter | Type | Description |
| --- | --- | --- |
| userid | `integer` | The user ID. |


  

### `entity.ListByClassName`

```lua
entity.ListByClassName(classname: T[, recursive: boolean]): T[]
```

Returns a list of all entities of the given class.


| Parameter | Type | Description |
| --- | --- | --- |
| classname | `T` | The name of the schema class. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.Iterate`

```lua
entity.Iterate(): fun(table: table<integer, client.C_BaseEntity>, index?: integer): integer, client.C_BaseEntity
```

Returns an iterator over all entities. Use it in a `for` loop. Each step gives the entity index and the entity.


  

### `entity.IterateByClassName`

```lua
entity.IterateByClassName(classname: T[, recursive: boolean]): fun(table: table<integer, T>, index?: integer): integer, T
```

Returns an iterator over the entities of the given class. Use it in a `for` loop. Each step gives the entity index and the entity.


| Parameter | Type | Description |
| --- | --- | --- |
| classname | `T` | The name of the schema class. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.FirstByClassName`

```lua
entity.FirstByClassName(classname: T[, recursive: boolean]): T?
```

Returns the first entity of the given class. Returns **nil** if there is no such entity.


| Parameter | Type | Description |
| --- | --- | --- |
| classname | `T` | The name of the schema class. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.ListByDesignerName`

```lua
entity.ListByDesignerName([designer_name: string, recursive: boolean]): client.C_BaseEntity[]
```

Returns a list of all entities with the given designer name.


| Parameter | Type | Description |
| --- | --- | --- |
| designer_name? | `string` | The designer name. If it is **nil**, all entities are returned. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.IterateByDesignerName`

```lua
entity.IterateByDesignerName([designer_name: string, recursive: boolean]): fun(table: table<integer, client.C_BaseEntity>, index?: integer): integer, client.C_BaseEntity
```

Returns an iterator over the entities with the given designer name. Use it in a `for` loop. Each step gives the entity index and the entity.


| Parameter | Type | Description |
| --- | --- | --- |
| designer_name? | `string` | The designer name. If it is **nil**, all entities are returned. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.FirstByDesignerName`

```lua
entity.FirstByDesignerName(designer_name: string[, recursive: boolean]): client.C_BaseEntity?
```

Returns the first entity with the given designer name. Returns **nil** if there is no such entity.


| Parameter | Type | Description |
| --- | --- | --- |
| designer_name | `string` | The designer name. |
| recursive? | `boolean` | Pass `true` to also include entities of classes that are derived from this class. The default is `false`. |


  

### `entity.WrapInstance`

```lua
entity.WrapInstance(instance: userdata|ffi.cdata*): client.C_BaseEntity?
```

Returns an entity object for a pointer to an entity.


| Parameter | Type | Description |
| --- | --- | --- |
| instance | `userdata\|ffi.cdata*` | A raw pointer to an entity instance. |


    


**Warning:** 
This function is for advanced users. The pointer must point to an entity that exists. Use it
only while that entity exists.


  

  

### `entity.GetLocalPlayer`

```lua
entity.GetLocalPlayer(): client.CCSPlayerController?, client.C_CSPlayerPawn?
```

Returns the controller of the local player and the pawn that the local player uses. The pawn is the player's own pawn, or the pawn of a bot while the player controls one.


    
Both values are **nil** if there is no local controller. The pawn alone can be **nil** if it is
not available. To get your own pawn also while you control a bot, use
`entity.GetOwnLocalPlayerPawn`.


  

  

### `entity.GetLocalPlayerController`

```lua
entity.GetLocalPlayerController(): client.CCSPlayerController?
```

Returns the controller of the local player. Returns **nil** if you are not connected. The controller stays your own while you control a bot or spectate another player.


  

### `entity.GetLocalPlayerPawn`

```lua
entity.GetLocalPlayerPawn(): client.C_CSPlayerPawn?
```

Returns the pawn that the local player uses. While the local player controls the pawn of another player or a bot, this is that pawn. In other cases this is the local player's own pawn.


    
Use this function for movement and weapons. While you spectate, it returns your own player
pawn. `entity.GetOwnLocalPlayerPawn` always returns your own pawn, also while you control a
bot. Both functions can return a dead pawn.


  

  

### `entity.GetViewPawn`

```lua
entity.GetViewPawn(): client.C_CSPlayerPawn?
```

Returns the pawn that the camera renders from now. In the in-eye and chase observer modes, this is the player that you spectate. In other cases it is the local player's own pawn.


    
Returns nil if the pawn or its observer services are not available. Use this function for
HUD information that follows the camera. During a transition, the result can be different
from the pawn that `GetLocalOrObservedPawn` returns.


  

  

### `entity.GetLocalOrObservedPawn`

```lua
entity.GetLocalOrObservedPawn([predicate: entity.PawnObserveePredicate]): client.C_CSPlayerPawn?
```

Returns the observed pawn while you spectate. In other cases it returns the same pawn as `entity.GetLocalPlayerPawn`.


| Parameter | Type | Description |
| --- | --- | --- |
| predicate? | `entity.PawnObserveePredicate` | A function that decides whether to use the observed pawn. |


    
Without a predicate, the observed pawn is used in the in-eye and chase observer modes. Pass a
predicate to decide for each observer mode. The predicate gets the current observer mode as a
`server.ObserverMode_t` value and the observed pawn. The values of the observer modes are in
`schema.ObserverMode_t`. The observed pawn is **nil** if there is no observed pawn.

The predicate is called only while you spectate. If the predicate returns `true` and there is
no observed pawn, the result is nil. The default selection for the in-eye and chase modes
works in the same way.


  

  

### `entity.GetLocalOrInEyePawn`

```lua
entity.GetLocalOrInEyePawn(): client.C_CSPlayerPawn?
```

Returns the observed pawn while you spectate in the in-eye mode. In other cases it returns the same pawn as `entity.GetLocalPlayerPawn`.


  

### `entity.GetLocalControlledPawn`

```lua
entity.GetLocalControlledPawn(): client.C_CSPlayerPawn?
```

Returns the pawn that the local player controls if it is not the player's own pawn. Returns **nil** in other cases. While you control a bot, this is the same pawn as `GetLocalPlayerPawn()`.


  

### `entity.GetLocalPawn`

```lua
entity.GetLocalPawn(): client.C_CSPlayerPawnBase?
```

Returns the pawn that the local controller points to now, of any type. `entity.GetLocalPawnType` returns its type. This pawn can be a `client.C_CSObserverPawn`, so use `GetLocalPlayerPawn()` when you need a player pawn.


  

### `entity.GetOwnLocalPlayerPawn`

```lua
entity.GetOwnLocalPlayerPawn(): client.C_CSPlayerPawn?
```

Returns the local player's own player pawn. The result is the same while you control a bot or spectate another player. The pawn can be dead.


  

### `entity.GetLocalObserverPawn`

```lua
entity.GetLocalObserverPawn(): client.C_CSObserverPawn?
```

Returns the observer pawn of the local player. Returns **nil** if there is no observer pawn. The observer pawn can exist while you do not spectate. Use `IsLocalObserving()` to check whether you spectate.


  

### `entity.GetObservedPawn`

```lua
entity.GetObservedPawn(): client.C_CSPlayerPawn?
```

Returns the current observer target if it is a player pawn. Returns **nil** in other cases. In the free camera observer modes, the target can be different from the pawn that the camera renders from.


  

### `entity.GetObserverMode`

```lua
entity.GetObserverMode(): server.ObserverMode_t
```

Returns the current observer mode. Returns `OBS_MODE_NONE` if you do not spectate. The values of the observer modes are in `schema.ObserverMode_t`.


  

### `entity.GetLocalPawnType`

```lua
entity.GetLocalPawnType(): entity.LocalPawnType
```

Returns the type of the current pawn as an `entity.LocalPawnType` value. The value is `kNull` if there is no pawn, or if the type of the pawn is not known yet during a transition.


  

### `entity.IsViewInEye`

```lua
entity.IsViewInEye(): boolean
```

Returns whether the view is a first person view. This is true when the local player spectates in the in-eye mode, or when the pawn of the player is in first person.


  

### `entity.IsLocalPlaying`

```lua
entity.IsLocalPlaying(): boolean
```

Returns whether the current pawn of the local player is a player pawn. This can be the player's own pawn or a pawn that the player controls. The pawn type is `entity.LocalPawnType.kPlayer`. This function does not check whether the pawn is alive.


  

### `entity.IsLocalObserving`

```lua
entity.IsLocalObserving(): boolean
```

Returns whether the current pawn of the local player is an observer pawn, which means that the player spectates. The pawn type is `entity.LocalPawnType.kObserver`. An observer pawn that exists while it is not the current pawn does not count.


  

### `entity.IsLocalPawnOwn`

```lua
entity.IsLocalPawnOwn(): boolean
```

Returns whether the current pawn is the local player's own player pawn. Returns false while the player controls another pawn, and while the player spectates.


  

### `entity.IteratePlayers`

```lua
entity.IteratePlayers([enemies_only: boolean, include_dead: boolean, relative_to: client.C_BaseEntity]): entity.IteratePlayers.Iterator, entity.IteratePlayers.Table, nil
```

Returns an iterator over all players. Each step gives a controller and its pawn.


| Parameter | Type | Description |
| --- | --- | --- |
| enemies_only? | `boolean` | If true, returns only enemies. The default is false. |
| include_dead? | `boolean` | If true, also returns dead players. The default is false. |
| relative_to? | `client.C_BaseEntity` | The entity that `enemies_only` compares teams with. The default is the pawn from `GetLocalPlayerPawn()`, which can be a controlled bot. |


  

### `entity.GetPlayerControllers`

```lua
entity.GetPlayerControllers([enemies_only: boolean, relative_to: client.C_BaseEntity]): client.CCSPlayerController[]
```

Returns all player controllers.


| Parameter | Type | Description |
| --- | --- | --- |
| enemies_only? | `boolean` | If true, returns only the controllers of enemies. The default is false. |
| relative_to? | `client.C_BaseEntity` | The entity that `enemies_only` compares teams with. The default is the pawn from `GetLocalPlayerPawn()`, which can be a controlled bot. |


  

### `entity.GetPlayerPawns`

```lua
entity.GetPlayerPawns([enemies_only: boolean, include_dead: boolean, relative_to: client.C_BaseEntity]): client.C_CSPlayerPawn[]
```

Returns all player pawns.


| Parameter | Type | Description |
| --- | --- | --- |
| enemies_only? | `boolean` | If true, returns only the pawns of enemies. The default is false. |
| include_dead? | `boolean` | If true, also returns dead pawns. The default is false. |
| relative_to? | `client.C_BaseEntity` | The entity that `enemies_only` compares teams with. The default is the pawn from `GetLocalPlayerPawn()`, which can be a controlled bot. |


  

### `entity.GetPlayerResource`

```lua
entity.GetPlayerResource(): client.C_CSPlayerResource?
```

Returns the player resource entity.


  

### `entity.GetGameRules`

```lua
entity.GetGameRules(): client.C_CSGameRules?
```

Returns the game rules schema object. Returns **nil** if it is not available.


  

### `entity.GetGameModeRules`

```lua
entity.GetGameModeRules(): client.CCSGameModeRules?
```

Returns the game mode rules schema object. Returns **nil** if it is not available.


  

### `entity.GetWeaponDataByClassName`

```lua
entity.GetWeaponDataByClassName(classname: string): client.CCSWeaponBaseVData?
```

Returns the weapon vdata for an entity class name. Returns nil if the name is not a known weapon class.


| Parameter | Type | Description |
| --- | --- | --- |
| classname | `string` | The schema class name of the weapon. |


  

### `entity.GetWeaponDataByDesignerName`

```lua
entity.GetWeaponDataByDesignerName(designer_name: string): client.CCSWeaponBaseVData?
```

Returns the weapon vdata for a designer name. Returns nil if the name is not a known weapon.


| Parameter | Type | Description |
| --- | --- | --- |
| designer_name | `string` | The designer name of the weapon, for example `weapon_ak47`. |


  

<a id="entity-PawnObserveePredicate"></a>
### `entity.PawnObserveePredicate`

A function that decides whether to use the observed pawn instead of the local pawn. Return `true` to use the observed pawn.


| Parameter | Type | Description |
| --- | --- | --- |
| observer_mode | `server.ObserverMode_t` |  |
| pawn | `client.C_CSPlayerPawn` |  |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` |  |


    
The function is called only while the local player spectates. In other cases the local pawn
is used.


  

  

<a id="entity-IteratePlayers-Key"></a>
### `entity.IteratePlayers.Key`


  

<a id="entity-IteratePlayers-Value"></a>
### `entity.IteratePlayers.Value`


  

<a id="entity-IteratePlayers-Table"></a>
### `entity.IteratePlayers.Table`


  

<a id="entity-IteratePlayers-Iterator"></a>
### `entity.IteratePlayers.Iterator`


| Parameter | Type | Description |
| --- | --- | --- |
| table | `entity.IteratePlayers.Table` |  |
| index? | `entity.IteratePlayers.Key` |  |


| Return | Type | Description |
| --- | --- | --- |
|  | `entity.IteratePlayers.Key` |  |
|  | `entity.IteratePlayers.Value` |  |


  

<a id="entity-LocalPawnType"></a>
### `entity.LocalPawnType`

The type of the current pawn of the local player. `entity.GetLocalPawnType` returns this value.


    

### `entity.LocalPawnType`


| Name | Value | Description |
| --- | --- | --- |
| kNull | 0 | There is no current pawn, or its type is not known yet during a transition |
| kPlayer | 1 | A player pawn, which is the local player's own pawn or a pawn that the player controls |
| kObserver | 2 | An observer pawn, which means that the player spectates |


  


<a id="entity-1"></a>

## Entity  — object type


An entity object refers to one entity through the handle of that entity. After the entity is
deleted, `IsValid` returns `false`, and reading or writing a field throws an error. This is
also true when a new entity gets the same index.

`==` returns `true` if two objects refer to the same entity.

The entities that `entity` returns have their schema fields and the methods below.

Read a field with `pawn.m_iHealth` or `pawn:GetField("m_iHealth")`. Write a field with an
assignment or with `SetField`.

The `self` annotation of each method shows the entity classes that the method works with. For
example, player pawn methods work with `client.C_CSPlayerPawn`, and weapon methods need a
weapon. Use the Schema System and Schema Values namespaces to inspect types and to work with
field values.

### Methods: C\_BaseEntity


  

### `Entity:GetField`

```lua
Entity:GetField(name: string): any
```

Reads a schema field by name. This does the same as `self.<name>`. Use it when the name of the field is held in a variable, or when the field has the same name as a method.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the schema field. |


  

### `Entity:SetField`

```lua
Entity:SetField(name: string, value: any)
```

Writes a schema field by name. This does the same as `self.<name> = value`.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the schema field. |
| value | `any` | The value to write. It is converted to the schema type of the field. |


  

### `Entity:GetClassIndex`

```lua
Entity:GetClassIndex(): integer
```

Returns the numeric class ID of the entity.


  

### `Entity:IsRuntimeIndex`

```lua
Entity:IsRuntimeIndex(classid: number): boolean
```

Returns `true` if the runtime class of the entity itself has the given class ID.


| Parameter | Type | Description |
| --- | --- | --- |
| classid | `number` | The class ID to compare with. |


  

### `Entity:IsRecursiveClassIndex`

```lua
Entity:IsRecursiveClassIndex(classid: number): boolean
```

Returns `true` if the class of the entity or one of its base classes has the given class ID.


| Parameter | Type | Description |
| --- | --- | --- |
| classid | `number` | The class ID to compare with. |


  

### `Entity:EntIndex`

```lua
Entity:EntIndex(): integer
```

Returns the index of the entity in the entity list. This works also after the entity is deleted.


  

### `Entity:GetSkeleton`

```lua
Entity:GetSkeleton(): client.CSkeletonInstance?
```

Returns the skeleton instance of the entity. Returns **nil** if the entity has no skeleton.


  

### `Entity:GetDesignerName`

```lua
Entity:GetDesignerName(): string
```

Returns the designer name of the entity.


  

### `Entity:GetHealth`

```lua
Entity:GetHealth(): integer
```

Returns the current health of the entity.


  

### `Entity:IsAlive`

```lua
Entity:IsAlive(): boolean
```

Returns `true` if the entity is alive.


  

### `Entity:IsDormant`

```lua
Entity:IsDormant(): boolean
```

Returns `true` if the entity is dormant. A dormant entity is an entity that the server does not send updates for at the moment.


  

### `Entity:GetWorldGroupId`

```lua
Entity:GetWorldGroupId(): integer
```

Returns the world group ID of the entity.


  

### `Entity:GetOwnerEntity`

```lua
Entity:GetOwnerEntity(): client.C_BaseEntity?
```

Returns the entity that owns this entity. Returns **nil** if the entity has no valid owner.


  

### `Entity:GetRefEHandle`

```lua
Entity:GetRefEHandle(): integer
```

Returns the handle of the entity as a raw integer. This works also after the entity is deleted. Pass the handle to `entity.LookupByHandle` to get the entity again.


  

### `Entity:IsValid`

```lua
Entity:IsValid(): boolean
```

Returns `true` while the entity exists. Returns `false` after the entity is deleted, also when a new entity gets the same index.


  

### `Entity:GetAbsOrigin`

```lua
Entity:GetAbsOrigin(): Vector
```

Returns the absolute position of the entity in the world.


  

### `Entity:SetAbsOrigin`

```lua
Entity:SetAbsOrigin(new_origin: Vector)
```

Sets the absolute position of the entity in the world.


| Parameter | Type | Description |
| --- | --- | --- |
| new_origin | `Vector` | The new position. |


    
This change is made on the client only. An update from the server can overwrite it.


  

  

### `Entity:GetAbsAngles`

```lua
Entity:GetAbsAngles(): QAngle
```

Returns the absolute angles of the entity in the world.


  

### `Entity:SetAbsAngles`

```lua
Entity:SetAbsAngles(new_angles: QAngle)
```

Sets the absolute angles of the entity in the world.


| Parameter | Type | Description |
| --- | --- | --- |
| new_angles | `QAngle` | The new angles. |


    
This change is made on the client only. An update from the server can overwrite it.


  

  

### `Entity:GetAbsVelocity`

```lua
Entity:GetAbsVelocity(): Vector
```

Returns the absolute velocity of the entity.


  

### `Entity:GetEntityIdentity`

```lua
Entity:GetEntityIdentity(): entity2.CEntityIdentity
```

Returns the identity object of the entity.


  

### `Entity:GetHitboxPosition`

```lua
Entity:GetHitboxPosition(i: number): Vector?
```

Returns the center of a hitbox volume in world space. Returns **nil** if it is not available.


| Parameter | Type | Description |
| --- | --- | --- |
| i | `number` | The index of the hitbox. |


    
For a sphere hitbox, this is the center of the sphere. For a box or capsule hitbox, this is
the middle point between its two ends. The hitbox transform moves the point into world
space. The result is the same as `entity:GetHitbox(i):GetCenter()`. To get the origin of the
transform, use `Hitbox:GetOrigin()`.


  

  

### `Entity:GetHitbox`

```lua
Entity:GetHitbox(i: number): Hitbox?
```

Returns the hitbox with the given index. Returns nil if the index is out of range.


| Parameter | Type | Description |
| --- | --- | --- |
| i | `number` | The index of the hitbox. |


    
Hitbox indices are different for each model. They depend on the hitbox set of the model and
on the meshes that the bodygroups of the entity enable. Index 0 is the first hitbox of this
model, and it can be any part of the body.


  

  

### `Entity:UpdateBones`

```lua
Entity:UpdateBones()
```

Calculates the world space bones of this entity again at its current position and pose. After this call, hitbox functions return the data of this frame.


    
Without this call, hitbox functions use the bones that the game calculated last. These bones
can be behind the current position of the entity. For example, in `override_view` the bones
of the local pawn are still from the previous frame. This function calculates all bones, so
call it only before reads that need the latest data.

Do not call it on a model whose bones follow the animation of another model, such as a HUD
weapon that follows the HUD arms. The calculation uses the own pose of the model without the
animation.


  

  

### `Entity:GetBoundingBox`

```lua
Entity:GetBoundingBox(): Vector2D?, Vector2D?, number?
```

Returns the ESP bounds on the screen. The values are the top left corner, the bottom right corner, and the draw alpha.


| Return | Type | Description |
| --- | --- | --- |
| min | `Vector2D?` |  |
| max | `Vector2D?` |  |
| alpha | `number?` |  |


    
For players and hostages, the bounds are around the body on the screen. For world entities,
the bounds use the ESP label positions, so both corners can be the same point.

Returns **nil** if there is no local or observed pawn, the scene or collision data of the
entity is missing, the draw alpha of the entity is zero, or the ESP cannot calculate valid
bounds. Valid bounds can be outside the screen, so a result does not mean that the entity is
visible.


  

  

### `Entity:GetMaxHealth`

```lua
Entity:GetMaxHealth(): number
```

Returns the maximum health of the entity.


  

### `Entity:IsEnemy`

```lua
Entity:IsEnemy([to: client.C_BaseEntity]): boolean
```

Returns true if this entity is an enemy of the given entity. Without an argument, it compares with the pawn from `entity.GetLocalPlayerPawn()`, which can be a controlled bot. If there is no local pawn, it returns true.


| Parameter | Type | Description |
| --- | --- | --- |
| to? | `client.C_BaseEntity` | The entity to compare with. The default is the pawn from `GetLocalPlayerPawn()`, which can be a controlled bot. |


    
The default pawn does not change to the spectated player, so the result stays the same when
the local player dies and spectates an enemy. To follow the camera, pass
`entity.GetViewPawn()`.


  


### Methods: C\_CSPlayerPawnBase


  

### `Entity:GetPlayerController`

```lua
Entity:GetPlayerController(): client.CCSPlayerController?
```

Returns the controller of this pawn.


  

### `Entity:GetActiveWeapon`

```lua
Entity:GetActiveWeapon(): client.C_CSWeaponBase?
```

Returns the active weapon of this pawn.


  

### `Entity:GetMyWeapons`

```lua
Entity:GetMyWeapons(): value.AtomicCollection<client.C_CSWeaponBase>?
```

Returns all weapons that this pawn holds.


    
The collection shows the current state of the game. Its indices start at 0.


  

  

### `Entity:GetEyeAngles`

```lua
Entity:GetEyeAngles(): QAngle?
```

Returns the eye angles of this pawn.


  

### `Entity:GetEyePosition`

```lua
Entity:GetEyePosition(): Vector?
```

Returns the eye position of this pawn.


  

### `Entity:GetAbsViewOffset`

```lua
Entity:GetAbsViewOffset(): Vector?
```

Returns the view offset of this pawn from its origin.


### Methods: CCSPlayerController


  

### `Entity:GetPlayerSlot`

```lua
Entity:GetPlayerSlot(): integer?
```

Returns the player slot index of this controller.


  

### `Entity:GetPlayerUserId`

```lua
Entity:GetPlayerUserId(): integer?
```

Returns the user ID of this controller.


  

### `Entity:GetPawn`

```lua
Entity:GetPawn(): client.C_CSPlayerPawnBase?
```

Returns the active pawn of this controller. It can be a player pawn or an observer pawn.


  

### `Entity:GetPlayerPawn`

```lua
Entity:GetPlayerPawn(): client.C_CSPlayerPawn?
```

Returns the player pawn of this controller. The player pawn can exist while the controller spectates.


  

### `Entity:GetObserverPawn`

```lua
Entity:GetObserverPawn(): client.C_CSObserverPawn?
```

Returns the observer pawn of this controller. Returns **nil** if it is not available. The observer pawn can exist while it is not the active pawn of the controller.


### Methods: C\_CSPlayerPawn


  

### `Entity:GetPlayerMaxSpeed`

```lua
Entity:GetPlayerMaxSpeed(): number?
```

Returns the maximum movement speed of this pawn.


  

### `Entity:ScaleDamage`

```lua
Entity:ScaleDamage(damage: number, weapon_data: client.CCSWeaponBaseVData, hitgroup: number[, attacker: client.C_CSPlayerPawn]): number
```

Scales raw damage by the armor and hitgroup modifiers of this pawn. This function does not fire a shot.


| Parameter | Type | Description |
| --- | --- | --- |
| damage | `number` | The raw damage. |
| weapon_data | `client.CCSWeaponBaseVData` | The weapon vdata for the damage scaling. |
| hitgroup | `number` | The index of the hitgroup that was hit. |
| attacker? | `client.C_CSPlayerPawn` | The pawn that attacks. It is used for team modifiers. |


  

### `Entity:GetBombDamage`

```lua
Entity:GetBombDamage([bomb: client.C_PlantedC4]): number?, number?
```

Estimates the health that this pawn would lose if the planted bomb exploded now.


| Parameter | Type | Description |
| --- | --- | --- |
| bomb? | `client.C_PlantedC4` | The planted bomb. The default is the active bomb. |


| Return | Type | Description |
| --- | --- | --- |
| minimum | `number?` | The lowest expected damage. This is **nil** if no bomb is ticking, or if the pawn is dormant, dead or cannot take damage. |
| maximum | `number?` | The highest expected damage. |


    
On maps with baked bomb damage, the game's own damage table is used, so both values are
equal. On other maps, the damage falls off with the distance and armor is applied. The
minimum and maximum are measured over the body of the pawn. Returns `0, 0` if the pawn is
out of range. The result does not depend on the bomb visuals settings.


  

  

### `Entity:GetPlayerSimulation`

```lua
Entity:GetPlayerSimulation([optimizations: simulation.SimOpt]): simulation.Player
```

Copies the state of this pawn into a separate simulation snapshot. Use `simulation.Player:RunCommand` to move the snapshot forward. This does not change the real player.


| Parameter | Type | Description |
| --- | --- | --- |
| optimizations? | `simulation.SimOpt` | The optimizations to use. The default is `simulation.SimOpt.kNoPlayerCollision \| simulation.SimOpt.kNoRareEvents \| simulation.SimOpt.kNoWeaponSimulation`. |


    
By default, the simulation skips the weapon simulation and the costly movement details. Pass
`simulation.SimOpt.kNone` for the full simulation.

For the local player, use the snapshot that the movement callback gives you.


  


### Methods: CCSPlayerController / C\_CSPlayerPawnBase


  

### `Entity:GetPlayerName`

```lua
Entity:GetPlayerName(): string?
```

Returns the display name of the player.


  

### `Entity:GetPlayerAvatar`

```lua
Entity:GetPlayerAvatar(): Image
```

Returns the 32x32 Steam avatar of the player. The name ESP and the spectator list draw the same avatar. For a bot, this function returns the icon of its team, which is larger. Pass a size to `render.DrawImage` to draw both at the same size.


    
The avatar is loaded one or two frames after the player first appears. Until then, and for a
user without an avatar, this function returns an empty image. Its `failed` field is true, and
`render.DrawImage` does not draw it. Call this function in every frame, and do not keep the
result.


  


### Methods: C\_CSWeaponBase


  

### `Entity:GetWeaponData`

```lua
Entity:GetWeaponData(): client.CCSWeaponBaseVData?
```

Returns the vdata of the weapon.


  

### `Entity:GetInaccuracy`

```lua
Entity:GetInaccuracy(): number
```

Returns the current inaccuracy of this weapon.


  

### `Entity:GetSpread`

```lua
Entity:GetSpread(): number
```

Returns the current spread of this weapon.


### Methods: C\_EconEntity


  

### `Entity:GetItem`

```lua
Entity:GetItem(): client.C_EconItemView
```

Returns the econ item view of this entity.


### Methods: C\_BaseModelEntity


  

### `Entity:SetGlowColor`

```lua
Entity:SetGlowColor(color: Color)
```

Adds this entity to the glow list of the current frame with the given color. Call it in every frame while you draw. Entities that cannot be drawn are ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| color | `Color` | The glow color. |


## Hitbox — object type


One hitbox of the skeleton of an entity. Its fields are read from the `modellib.CHitBox` of the
model through the schema, so the field names are the names that the game uses.

Hitbox data is read-only and moves with the entity when the entity is animated. Use it only
while the entity is valid. Reading a field throws an error if the hitbox no longer exists.


  

### `Hitbox:GetOrigin`

```lua
Hitbox:GetOrigin(): Vector?
```

Returns the origin of the world transform of this hitbox. Returns nil if it is not available. The transform can come from a bone or from a shape without a bone. To get the center of the hitbox volume, use `Hitbox:GetCenter()`.


  

### `Hitbox:GetTransform`

```lua
Hitbox:GetTransform(): CTransform?
```

Returns the world transform of this hitbox. Returns nil if it is not available.


    
The transform places the shape of the hitbox in the world. This also works for shapes that do
not follow a bone.


  

  

### `Hitbox:GetCenter`

```lua
Hitbox:GetCenter(): Vector?
```

Returns the center of the volume of this hitbox in world space. Returns nil if it is not available. The result is the same as `entity:GetHitboxPosition(index)`.


  

### `Hitbox:GetCapsule`

```lua
Hitbox:GetCapsule(): Vector?, Vector?, number?
```

Returns this hitbox as a capsule in world space. The values are the centers of the two end spheres and the radius, with the scale of the transform applied. For a sphere hitbox, both ends are the same point. Returns **nil** for other shapes, or if the hitbox is not available.


| Return | Type | Description |
| --- | --- | --- |
| start | `Vector?` | The center of the first end sphere. |
| finish | `Vector?` | The center of the second end sphere. |
| radius | `number?` | The radius in world units. |


    
To draw the capsule, project each end with `projection.SphereEllipse(end, radius)`. To test
whether a segment hits it, pass the results to `trace.IntersectCapsule`.


  

  

### `Hitbox:GetOwnerEntity`

```lua
Hitbox:GetOwnerEntity(): Entity
```

Returns the entity that this hitbox belongs to.


  

### `Hitbox:GetIndex`

```lua
Hitbox:GetIndex(): number
```

Returns the index of this hitbox. This is the index that was passed to `entity:GetHitbox`.
