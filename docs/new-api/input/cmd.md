> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# User Command


## UserCmd — object type

The input command that the client sends to the server every tick. It holds the movement, the
view angles and the button states.

It is passed to the `createmove`, `pre_movement` and `post_movement` events. You can read the
fields and assign new values to change the input of the player. Reading an unknown field
returns nil. Assigning an unknown field throws an error.

To turn the view, use the `events.input_poll` event with `input.InputPollContext:GetViewAngles`
and `input.InputPollContext:SetViewAngles` instead.

The button fields are handles. To change the state of a button, assign a value to a field of the
handle, for example `cmd.in_jump.down = true`. Assigning a value to the button field itself throws
an error.

The user command for a single tick. It holds the input and view state that is sent to the server.


  

### `UserCmd.attack1_start_history_index`

The index in the input history at which the primary attack started, or nil if it did not start.


  

### `UserCmd.attack2_start_history_index`

The index in the input history at which the secondary attack started, or nil if it did not start.


  

### `UserCmd.client_tick`

The client tick at which this command was created.


  

### `UserCmd.forwardmove`

The forward and backward movement, as a fraction of the maximum movement speed. Assigned values are normalized when the command is processed.


  

### `UserCmd.has_new_snapshot`

True if a new world snapshot arrived before this pass. Read-only.


  

### `UserCmd.impulse`

The impulse command number. An impulse triggers an action for a single tick.


  

### `UserCmd.in_attack`

Primary fire.


  

### `UserCmd.in_attack2`

Secondary fire or scope.


  

### `UserCmd.in_back`

Move backward.


  

### `UserCmd.in_duck`

Duck.


  

### `UserCmd.in_forward`

Move forward.


  

### `UserCmd.in_joyautosprint`

Automatic sprint with a gamepad.


  

### `UserCmd.in_jump`

Jump.


  

### `UserCmd.in_look_at_weapon`

Inspect the weapon.


  

### `UserCmd.in_moveleft`

Move left.


  

### `UserCmd.in_moveright`

Move right.


  

### `UserCmd.in_reload`

Reload.


  

### `UserCmd.in_score`

Show the scoreboard.


  

### `UserCmd.in_speed`

Walk.


  

### `UserCmd.in_turnleft`

Turn left with the keyboard or a gamepad.


  

### `UserCmd.in_turnright`

Turn right with the keyboard or a gamepad.


  

### `UserCmd.in_use`

Use or interact.


  

### `UserCmd.in_useorreload`

The shared button for use and reload.


  

### `UserCmd.in_zoom`

Zoom or toggle the scope.


  

<a id="usercmdinputhistory"></a>
### `UserCmd.input_history`

The input samples of each frame that are attached to this command. Read-only.


  

### `UserCmd.is_first_pass`

True on the first pass over this command, and false while the command is processed again. Read-only.


  

### `UserCmd.leftmove`

The left and right movement, as a fraction of the maximum movement speed. Assigned values are normalized when the command is processed.


  

### `UserCmd.legacy_command_number`

The sequence number of the command. The server uses it to confirm the command.


  

### `UserCmd.mousedx`

The raw horizontal mouse movement in this tick.


  

### `UserCmd.mousedy`

The raw vertical mouse movement in this tick.


  

### `UserCmd.moveangles`

The angles that give the direction of movement. They are separate from the view angles.


  

### `UserCmd.needs_full_recompute`

True if the command must be built again from the start. Read-only.


  

### `UserCmd.random_seed`

The random seed that client side prediction uses to get the same results as the server.


  

### `UserCmd.should_set_viewangles`

Assign `true` to apply `viewangles` to the local camera after the callback. The angles are copied at the moment of the assignment, so later changes to `viewangles` are not applied. Assign `false` to cancel the request. This moves the camera even when it is set on a copy, so do not set it on copies used for simulation. It does not change what is sent to the server.


  

<a id="usercmdsubtickmoves"></a>
### `UserCmd.subtick_moves`

The subtick input steps. Read-only.


  

### `UserCmd.upmove`

The vertical movement, for example when swimming up or down.


  

### `UserCmd.viewangles`

The view angles of the player, as pitch, yaw and roll.


  

### `UserCmd.weaponselect`

The entity index of the weapon that the player wants to switch to.


  

### `UserCmd:Finalized`

```lua
UserCmd:Finalized(sim: simulation.Player): UserCmd
```

Returns a copy of this command with the movement resolved and corrected against the given simulation. This command is not changed.


| Parameter | Type | Description |
| --- | --- | --- |
| sim | `simulation.Player` | The simulation that the command is finalized against. |


    
Clone a simulation that an event gave you before you run commands on it. The result is only a
prediction and is not sent to the server.


  

  

### `UserCmd:Clone`

```lua
UserCmd:Clone(): UserCmd
```

Returns a full copy of this command.


## UserCmd.InButtonHandle — object type

The state of one button in a command. Reading an unknown field returns nil. Assigning an
unknown field throws an error.


  

### `UserCmd.InButtonHandle.down`

True if the button is down. Assigning a value forces the button state.


  

### `UserCmd.InButtonHandle.pressed`

True if the button was pressed in this command. Assigning a value throws an error.


  

### `UserCmd.InButtonHandle.released`

True if the button was released in this command. Assigning a value throws an error.


  

### `UserCmd.InButtonHandle.state`

The raw state of the button. Assigning a value sets the button state.


  

### `UserCmd.InButtonHandle:RemoveButton`

```lua
UserCmd.InButtonHandle:RemoveButton()
```

Removes this button from the command for this tick.


## UserCmd.SubtickMoveStepHandle — object type

One subtick input step. Assigning an unknown field throws an error. If the step was removed from
the command, using the handle throws an error.


  

### `UserCmd.SubtickMoveStepHandle.button`

The button that this step presses or releases.


  

### `UserCmd.SubtickMoveStepHandle.index`

The index of this step. Read-only.


  

### `UserCmd.SubtickMoveStepHandle.move`

The analog movement. Assign nil to remove it.


  

### `UserCmd.SubtickMoveStepHandle.moveangles`

The direction used for the movement fix. Assign nil to remove it.


  

### `UserCmd.SubtickMoveStepHandle.preserve`

Set it to true to stop the engine from removing this step.


  

### `UserCmd.SubtickMoveStepHandle.pressed`

True if the button is pressed, false if it is released.


  

### `UserCmd.SubtickMoveStepHandle.viewangles`

The absolute view angles. The roll is ignored. Assign nil to remove them.


  

### `UserCmd.SubtickMoveStepHandle.when`

The fraction of the tick at which the step happens.


## CSGOInterpolationInfo — cdata

An FFI cdata value that describes an interpolation between two recorded ticks.

Use `ffi.new("CSGOInterpolationInfo", { src_tick = 100, dst_tick = 101, frac = 0.5 })` to create
a separate value.

A value read from the command history is a reference into the history. Get it again after you
replace the field or change the history that holds it.


  

### `CSGOInterpolationInfo.dst_tick`

The tick at which the interpolation ends.


  

### `CSGOInterpolationInfo.frac`

The interpolation amount between the start tick and the end tick.


  

### `CSGOInterpolationInfo.src_tick`

The tick at which the interpolation starts.


## TickAndInterpolationAmount\_t — cdata


An FFI cdata value that stores a tick and a fraction of a tick. It holds an `int tick` followed
by a `float fraction`.

Create one with `TickAndInterpolationAmount_t(tick, fraction)`. Keep the fraction at 0 or more
and less than 1. The constructor does not normalize it.

The tick fields of the command history return separate copies. To update an entry, assign the
edited copy back to the field. Assign nil to clear the field.


  

### `TickAndInterpolationAmount_t.fraction`

The fraction of a tick, at 0 or more and less than 1, stored as a 32-bit float.


  

### `TickAndInterpolationAmount_t.tick`

The whole number of ticks, stored as a signed 32-bit integer.


<a id="tickandinterpolationamount_t-1"></a>

## TickAndInterpolationAmount_t  — ctype · callable


  

<a id="tickandinterpolationamount_t"></a>
### `TickAndInterpolationAmount_t()`

```lua
TickAndInterpolationAmount_t(): TickAndInterpolationAmount_t
```

Zero tick and fraction


  

### `TickAndInterpolationAmount_t(tick, fraction)`

```lua
TickAndInterpolationAmount_t(tick: integer, fraction: number): TickAndInterpolationAmount_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| tick | `integer` |  |
| fraction | `number` |  |


  

### `TickAndInterpolationAmount_t(self)`

```lua
TickAndInterpolationAmount_t(self: TickAndInterpolationAmount_t): TickAndInterpolationAmount_t
```

Copy


| Parameter | Type | Description |
| --- | --- | --- |
| self | `TickAndInterpolationAmount_t` |  |


## UserCmd.InputHistoryEntryHandle — object type

One recorded input sample of a command. Assigning an unknown field throws an error. If the entry
was removed from the command, using the handle throws an error.

The tick fields return separate FFI cdata copies. To update the entry, edit a copy and assign it
back. Assign nil to clear an optional field.

The interpolation fields return `CSGOInterpolationInfo` references into the entry, and you can
change them in place. Get them again after you replace or clear the field, change the history,
or after the command is no longer valid. Assigning an interpolation value copies it into the entry.


  

### `UserCmd.InputHistoryEntryHandle.cl_interp`

The client interpolation amount. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.index`

The index of this entry, starting at zero. Read-only.


  

### `UserCmd.InputHistoryEntryHandle.player_interp`

The player interpolation sample, as a reference into the entry. Assigning a value copies it. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.player_tick`

The player time, as a separate FFI cdata copy. Assign it back after you edit it. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.render_tick`

The render time, as a separate FFI cdata copy. Assign it back after you edit it. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.sv_interp0`

The first server interpolation sample, as a reference into the entry. Assigning a value copies it. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.sv_interp1`

The second server interpolation sample, as a reference into the entry. Assigning a value copies it. Assign nil to clear it.


  

### `UserCmd.InputHistoryEntryHandle.viewangles`

The view angles recorded in this sample. It is a reference into the entry, and you can change it in place.


## UserCmd.SubtickMoves — object type


The subtick steps of a command. Indices start at zero. Reading an index that does not exist
returns nil. A command can hold at most 32 steps.


  

### `UserCmd.SubtickMoves:Size`

```lua
UserCmd.SubtickMoves:Size(): integer
```


  

### `UserCmd.SubtickMoves:Remove`

```lua
UserCmd.SubtickMoves:Remove(i: integer)
```

Removes the step at index `i`. Indices start at zero. The indices of the steps after it go down by one, so get new handles afterwards. If the index does not exist, the function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| i | `integer` |  |


  

### `UserCmd.SubtickMoves:PopBack`

```lua
UserCmd.SubtickMoves:PopBack()
```

Removes the last step. If there are no steps, nothing happens.


  

### `UserCmd.SubtickMoves:Clear`

```lua
UserCmd.SubtickMoves:Clear()
```

Removes all steps.


  

### `UserCmd.SubtickMoves:EmplaceBack`

```lua
UserCmd.SubtickMoves:EmplaceBack([when: number]): UserCmd.SubtickMoveStepHandle
```

Adds a step at the end and returns its handle. If `when` is not given, it is `0`.


| Parameter | Type | Description |
| --- | --- | --- |
| when? | `number` |  |


    
A command can hold at most 32 steps. Adding more throws an error. With a button, the value must
be a single button, otherwise the function throws an error.


  


## UserCmd.InputHistory — object type


The input history entries of a command. Indices start at zero. Reading an index that does not
exist returns nil. A command can hold at most 16 entries.


  

### `UserCmd.InputHistory:Size`

```lua
UserCmd.InputHistory:Size(): integer
```


  

### `UserCmd.InputHistory:Remove`

```lua
UserCmd.InputHistory:Remove(i: integer)
```

Removes the entry at index `i`. Indices start at zero. The indices of the entries after it go down by one, so get new handles afterwards. If the index does not exist, the function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| i | `integer` |  |


  

### `UserCmd.InputHistory:PopBack`

```lua
UserCmd.InputHistory:PopBack()
```

Removes the last entry. If there are no entries, nothing happens.


  

### `UserCmd.InputHistory:Clear`

```lua
UserCmd.InputHistory:Clear()
```

Removes all entries.


  

### `UserCmd.InputHistory:EmplaceBack`

```lua
UserCmd.InputHistory:EmplaceBack(): UserCmd.InputHistoryEntryHandle
```

Adds an empty entry at the end and returns its handle. A command can hold at most 16 entries. Adding more throws an error. Update the attack history indices of the command when you change the history.


  

### `UserCmd.InputHistory:Resize`

```lua
UserCmd.InputHistory:Resize(size: integer)
```

Adds or removes entries at the end, so that the history has exactly `size` entries.


| Parameter | Type | Description |
| --- | --- | --- |
| size | `integer` | The new number of entries, from 0 to 16. |


    
If `size` is less than 0 or more than 16, the function throws an error.


  


## simulation — global table

The simulation of players, movement and weapons. It is used by `entity:GetPlayerSimulation` and
the movement events.


  

<a id="simulationgrenade"></a>
### `simulation.Grenade`

```lua
simulation.Grenade(source: integer|client.C_BaseEntity[, thrower: client.C_CSPlayerPawn]): simulation.Grenade?
```

Creates a grenade simulation.


| Parameter | Type | Description |
| --- | --- | --- |
| source | `integer\|client.C_BaseEntity` | An item definition index, a held grenade, or a grenade projectile. |
| thrower? | `client.C_CSPlayerPawn` | The thrower. For entities, the default is the owner of the grenade. |


| Return | Type | Description |
| --- | --- | --- |
|  | `simulation.Grenade?` | Nil if the entity is not valid, or is not a held grenade or a projectile. An unsupported index or an argument of another type throws an error. |


    
Pass an item definition index to simulate a grenade without an entity. The supported indices
are 43 for the flashbang, 44 for the HE grenade, 45 for the smoke grenade, 46 for the molotov,
47 for the decoy and 48 for the incendiary grenade. You can also pass the `m_iItemDefinitionIndex`
of a held weapon.

Pass a held grenade or a grenade projectile in flight to simulate that entity. A projectile
follows its networked state during `Run`.

Without a thrower, hits on players are skipped. If the simulation has neither a thrower nor a
grenade entity, `GetDamage` throws an error for HE grenades. The spread of fire from a molotov
or incendiary grenade is not simulated.


  

  

<a id="simulation-SimOpt"></a>
### `simulation.SimOpt`

Flags that make a simulation faster by skipping parts of it. Combine them with `bit.bor` into the mask that `entity:GetPlayerSimulation` takes. Each flag skips the named part. Only combine the flags for parts that your simulation does not need.


    

### `simulation.SimOpt`


| Name | Value | Description |
| --- | --- | --- |
| kNone | 0 | Nothing is skipped, so the full simulation runs |
| kNoPlayerCollision | 1 | Skips collision between players |
| kNoEyePos | 2 | Skips updates of the eye position |
| kNoWeaponSimulation | 4 | Skips the weapon simulation |
| kNoRareEvents | 8 | Skips rare events |


  


## simulation.Player — object type

A snapshot of a player for prediction.

A snapshot that an event gives you can be write protected. Changing it or running a command on
it then throws an error. Call `Clone` first and change the copy.

Reading an unknown field returns nil. Assigning an unknown field or a read-only field does nothing.


  

### `simulation.Player.controller`

The controller of the simulated pawn, or nil if it no longer exists. Read-only.


  

### `simulation.Player.curtime`

The current simulation time, in seconds.


  

### `simulation.Player.frametime`

The length of one simulation tick, in seconds.


  

### `simulation.Player.m_MoveType`

The current movement type, for example walk, fly, ladder or noclip.


  

### `simulation.Player.m_angEyeAngles`

The final eye angles after the subtick and aim punch changes.


  

### `simulation.Player.m_angStashedShootAngles`

The saved shoot angles for the queued grenade throw.


  

### `simulation.Player.m_bCanMove`

The saved result of whether the player can move.


  

### `simulation.Player.m_bCarryingHostage`

True while the player carries a hostage.


  

### `simulation.Player.m_bFreezePeriod`

True while the round is in its freeze time.


  

### `simulation.Player.m_bGrenadeParametersStashed`

True if the throw parameters of a grenade are saved for a queued throw.


  

### `simulation.Player.m_bIsDefusing`

True while the player is defusing the bomb.


  

### `simulation.Player.m_bIsGrabbingHostage`

True while the player is picking up a hostage.


  

### `simulation.Player.m_bIsScoped`

True while the player is scoped in.


  

### `simulation.Player.m_bIsWalking`

True while the player holds the walk key.


  

### `simulation.Player.m_bResumeZoom`

True if the scope zooms in again after a shot.


  

### `simulation.Player.m_bWaitForNoAttack`

True if the player cannot fire until the attack button is released.


  

### `simulation.Player.m_fFlags`

The bit mask of entity flags, for example on ground, ducking or frozen.


  

### `simulation.Player.m_fImmuneToGunGameDamageTime`

The time at which the spawn protection in gun game ends.


  

### `simulation.Player.m_fRoundStartTime`

The time at which the current round started.


  

### `simulation.Player.m_flFlinchStack`

The flinch that has built up from recent damage.


  

### `simulation.Player.m_flFriction`

The friction multiplier of the surface for the player.


  

### `simulation.Player.m_flGravityScale`

The multiplier for the world gravity for this player.


  

### `simulation.Player.m_flPlayerMaxSpeed`

The maximum speed at which the player can move.


  

### `simulation.Player.m_flVelocityModifier`

The speed multiplier after the player takes damage.


  

### `simulation.Player.m_flWaterJumpTime`

The time that is left in the current water jump.


  

### `simulation.Player.m_flWaterLevel`

How deep the player is in water.


  

### `simulation.Player.m_grenadeParameterStashTime`

The time at which the throw parameters of the grenade were saved.


  

### `simulation.Player.m_hGroundEntity`

The entity the player stands on, or nil. Read-only.


  

### `simulation.Player.m_iShotsFired`

The number of shots fired in a row. Recoil grows with it.


  

### `simulation.Player.m_iTeamNum`

The team number of the player.


  

### `simulation.Player.m_ignoreLadderJumpTime`

The time until the player can jump off a ladder again.


  

### `simulation.Player.m_nInteractsWith`

The collision mask of the contents that the player interacts with.


  

### `simulation.Player.m_nRandomSeed`

The random seed for spread and recoil.


  

### `simulation.Player.m_nTickBase`

The tick base. The prediction time of the player is calculated from it.


  

### `simulation.Player.m_nWaterType`

The contents mask of the water the player is in.


  

### `simulation.Player.m_nodeToWorld`

The transform from the scene node of the player to world space. Read-only.


  

### `simulation.Player.m_predictableBaseAngle`

The base angle of the predictable part of the aim punch.


  

### `simulation.Player.m_predictableBaseAngleVel`

The base angular velocity of the predictable part of the aim punch.


  

### `simulation.Player.m_predictableBaseTick`

The base tick of the predictable part of the aim punch.


  

### `simulation.Player.m_predictableBaseTickInterpAmount`

The interpolation fraction of the base tick of the predictable aim punch.


  

### `simulation.Player.m_unpredictableBaseAngle`

The base angle of the unpredictable part of the aim punch.


  

### `simulation.Player.m_unpredictableBaseTick`

The base tick of the unpredictable part of the aim punch.


  

### `simulation.Player.m_vecAbsOrigin`

The origin of the player in world space.


  

### `simulation.Player.m_vecAbsVelocity`

The velocity of the player in world space.


  

### `simulation.Player.m_vecBaseVelocity`

The velocity given by the surface the player stands on, for example a conveyor or a moving platform.


  

### `simulation.Player.m_vecRootBoneOffset`

The offset of the root bone of the skeleton from the origin.


  

### `simulation.Player.m_vecStashedGrenadeThrowPosition`

The saved throw position for the queued grenade throw.


  

### `simulation.Player.m_vecStashedVelocity`

The saved velocity of the player for the queued grenade throw.


  

### `simulation.Player.m_vecViewOffset`

The offset from the origin to the eye position.


  

### `simulation.Player.m_vecWaterJumpVel`

The velocity used during the current water jump.


  

### `simulation.Player.movement`

The movement part, which handles walking, jumping, ducking and collision. Read-only.


  

### `simulation.Player.mp_teammates_are_enemies`

True if teammates count as enemies for collision and damage.


  

### `simulation.Player.optimizations`

The mask of enabled `simulation.SimOpt` flags.


  

### `simulation.Player.pawn`

The pawn this snapshot was taken from, or nil if it no longer exists. Read-only.


  

### `simulation.Player.tick_frac`

The fraction of the current tick, from 0 to 1.


  

### `simulation.Player.tickcount`

The current tick of the simulation.


  

### `simulation.Player.v_angle`

The raw view angles from the command.


  

### `simulation.Player.weapon`

The weapon part, which handles firing, accuracy and grenades. Read-only.


  

### `simulation.Player:RunCommand`

```lua
simulation.Player:RunCommand(cmd: UserCmd)
```

Advances the simulation by one user command.


| Parameter | Type | Description |
| --- | --- | --- |
| cmd | `UserCmd` | The command to simulate for this tick. |


    
Clone a simulation that an event gave you before you run commands on it. If the simulation is
write protected, this function throws an error. The result is only a prediction and is not sent
to the server.


  

  

### `simulation.Player:Clone`

```lua
simulation.Player:Clone(): simulation.Player
```

Returns a full copy of this simulation snapshot. The copy is not write protected.


  

### `simulation.Player:IsFreezePeriod`

```lua
simulation.Player:IsFreezePeriod(): boolean
```

Returns true if the round is in its freeze time and the player cannot move yet.


  

### `simulation.Player:SetAbsOrigin`

```lua
simulation.Player:SetAbsOrigin(origin: Vector)
```

Moves the player to the given origin in world space. If the simulation is write protected, this function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| origin | `Vector` | The new origin of the player. |


  

### `simulation.Player:IsThrowingGrenade`

```lua
simulation.Player:IsThrowingGrenade(): boolean
```

Returns true if the player is throwing a grenade at this moment.


  

### `simulation.Player:IsJumpThrow`

```lua
simulation.Player:IsJumpThrow(throw_duration: number): boolean
```

Checks the timing window of a jump throw. The function adds the given throw delay to the current simulation time and subtracts the time at which the grenade parameters were saved. It returns true if the result is more than 0 and at most 0.2 seconds. The delay is not the time for which a button is held.


| Parameter | Type | Description |
| --- | --- | --- |
| throw_duration | `number` | The planned throw delay, in seconds. |


  

### `simulation.Player:GetEyePosition`

```lua
simulation.Player:GetEyePosition(): Vector
```

Returns the current eye position of the player in world space.


  

### `simulation.Player:IsEnemy`

```lua
simulation.Player:IsEnemy(other: client.C_BaseEntity): boolean
```

Returns true if `other` is an enemy of the simulated player. The `mp_teammates_are_enemies` setting is taken into account. Returns false if `other` is nil or the simulated player.


| Parameter | Type | Description |
| --- | --- | --- |
| other | `client.C_BaseEntity` | The entity to check. |


  

### `simulation.Player:IsTeamMate`

```lua
simulation.Player:IsTeamMate(other: client.C_BaseEntity): boolean
```

Returns true if `other` is a teammate of the simulated player. It always returns the opposite of `player:IsEnemy`, so it also returns true if `other` is nil or the simulated player.


| Parameter | Type | Description |
| --- | --- | --- |
| other | `client.C_BaseEntity` | The entity to check. |


  

### `simulation.Player:GetSimpleFilter`

```lua
simulation.Player:GetSimpleFilter([collision_group: integer]): trace.Filter
```

Returns a trace filter that is set up in the same way as the filter of the movement code. The filter ignores the simulated player and uses the given collision group.


| Parameter | Type | Description |
| --- | --- | --- |
| collision_group? | `integer` | The collision group of the trace. The default is `trace.StandardCollisionGroups_t.PLAYER_MOVEMENT`. |


  

### `simulation.Player:GetShape`

```lua
simulation.Player:GetShape(): userdata
```

Returns the current collision shape of the player. Its size depends on the current duck amount.


    


**Warning:** 
The shape is an opaque `GenericShape_t` value for FFI code. It has no fields or methods in Lua.


  


## simulation.Movement — object type

The movement part of a simulated player. It handles walking, movement in the air, jumping,
ducking, ladders, and the console variables that control them.

Reading an unknown field returns nil. Assigning an unknown field does nothing. If the simulation
is write protected, assigning a field throws an error.


  

### `simulation.Movement.host_timescale`

The time scale of the simulation.


  

### `simulation.Movement.m_bDesiresDuck`

True while the duck button is held.


  

### `simulation.Movement.m_bDuckOverride`

True if ducking is forced, whatever the input is.


  

### `simulation.Movement.m_bDucked`

True if the player is fully ducked.


  

### `simulation.Movement.m_bDucking`

True while the player is ducking.


  

### `simulation.Movement.m_bHasWalkMovedSinceLastJump`

True if the player has walked since the last jump.


  

### `simulation.Movement.m_bJumpApexPending`

True while the player is still rising toward the highest point of a jump.


  

### `simulation.Movement.m_bUseFrictionStashedSpeed`

True if the speed saved before friction is used again.


  

### `simulation.Movement.m_bUsingGroundTopologyOffset`

True if a view offset for the shape of the ground is applied.


  

### `simulation.Movement.m_fStashGrenadeParameterWhen`

The subtick time at which the grenade parameters should be saved.


  

### `simulation.Movement.m_flAccumulatedJumpError`

The error in subtick jump timing that has built up.


  

### `simulation.Movement.m_flBombPlantViewOffset`

The vertical view offset caused by planting the bomb.


  

### `simulation.Movement.m_flDuckAmount`

The current duck progress. `0` means standing and `1` means fully ducked.


  

### `simulation.Movement.m_flDuckRootOffset`

The vertical offset of the root bone caused by ducking.


  

### `simulation.Movement.m_flDuckSpeed`

The speed at which the duck amount changes.


  

### `simulation.Movement.m_flDuckViewOffset`

The vertical view offset caused by ducking.


  

### `simulation.Movement.m_flFallVelocity`

The downward speed during the current fall.


  

### `simulation.Movement.m_flFrictionStashedSpeed`

The speed saved before friction was applied.


  

### `simulation.Movement.m_flLastDuckTime`

The time of the last change between ducking and standing.


  

### `simulation.Movement.m_flLastJumpFrac`

The subtick fraction of the last jump.


  

### `simulation.Movement.m_flLastJumpVelocityZ`

The vertical velocity at the moment of the last jump.


  

### `simulation.Movement.m_flMaxspeed`

The current maximum movement speed.


  

### `simulation.Movement.m_flStamina`

The current stamina. Low stamina limits repeated jumps.


  

### `simulation.Movement.m_flSurfaceFriction`

The friction of the surface the player stands on.


  

### `simulation.Movement.m_flUseFrictionStashedSpeedUntilFrac`

The subtick fraction until which the saved speed is used.


  

### `simulation.Movement.m_flUsingGroundTopologyOffsetTransitionSmoothing`

The smoothing amount for changes of the ground shape offset.


  

### `simulation.Movement.m_nLastJumpTick`

The tick at which the player last jumped.


  

### `simulation.Movement.m_vecCmdMove`

The movement input of the previous command.


  

### `simulation.Movement.m_vecLadderNormal`

The surface normal of the ladder the player is on.


  

### `simulation.Movement.m_vecLastMovementImpulses`

The movement impulses applied in the previous tick.


  

### `simulation.Movement.m_vecLastPositionAtFullCrouchSpeed`

The last position recorded while the player moved at full crouch speed.


  

### `simulation.Movement.m_vecWalkWishVel`

The walking velocity that the input asks for.


  

### `simulation.Movement.mp_solid_teammates`

The collision mode between teammates.


  

### `simulation.Movement.mp_tagging_scale`

The multiplier for the slowdown when the player is hit by enemy fire.


  

### `simulation.Movement.sv_accelerate`

The acceleration rate on the ground.


  

### `simulation.Movement.sv_accelerate_use_weapon_speed`

True if the acceleration depends on the speed of the active weapon.


  

### `simulation.Movement.sv_air_max_wishspeed`

The maximum wish speed for acceleration in the air.


  

### `simulation.Movement.sv_airaccelerate`

The acceleration rate in the air.


  

### `simulation.Movement.sv_autobunnyhopping`

True if automatic bunny hopping is enabled.


  

### `simulation.Movement.sv_bhop_time_window`

The time window in which a queued jump can start a bunny hop.


  

### `simulation.Movement.sv_bounce`

How much speed is kept when bouncing off surfaces.


  

### `simulation.Movement.sv_enablebunnyhopping`

True if bunny hopping without a speed limit on jumps is allowed.


  

### `simulation.Movement.sv_falldamage_scale`

The multiplier for fall damage.


  

### `simulation.Movement.sv_friction`

The base friction on the ground.


  

### `simulation.Movement.sv_gravity`

The world gravity, in units per second squared.


  

### `simulation.Movement.sv_jump_impulse`

The upward velocity added by a jump.


  

### `simulation.Movement.sv_jump_precision_enable`

True if exact subtick jump timing is enabled.


  

### `simulation.Movement.sv_jump_spam_penalty_time`

The cooldown that punishes pressing jump too often.


  

### `simulation.Movement.sv_ladder_angle`

The view angle limit that affects getting onto a ladder.


  

### `simulation.Movement.sv_ladder_dampen`

How much movement is slowed down on ladders.


  

### `simulation.Movement.sv_ladder_scale_speed`

The speed multiplier for climbing ladders.


  

### `simulation.Movement.sv_legacy_jump`

True if the old jump behavior is used.


  

### `simulation.Movement.sv_maxspeed`

The global maximum speed of players.


  

### `simulation.Movement.sv_maxvelocity`

The maximum velocity along any single axis.


  

### `simulation.Movement.sv_noclipaccelerate`

The acceleration rate in noclip.


  

### `simulation.Movement.sv_noclipspeed`

The movement speed in noclip.


  

### `simulation.Movement.sv_optimizedmovement`

True if the optimized movement code is used.


  

### `simulation.Movement.sv_quantize_movement_input`

True if the movement input is rounded before it is applied.


  

### `simulation.Movement.sv_staminajumpcost`

The stamina that a jump costs.


  

### `simulation.Movement.sv_staminalandcost`

The stamina that a landing costs.


  

### `simulation.Movement.sv_staminamax`

The maximum stamina.


  

### `simulation.Movement.sv_staminarecoveryrate`

The rate at which stamina recovers.


  

### `simulation.Movement.sv_standable_normal`

The minimum Z value of a surface normal for a slope that the player can stand on.


  

### `simulation.Movement.sv_step_move_vel_min`

The minimum velocity needed to try a step move.


  

### `simulation.Movement.sv_stepsize`

The maximum height that the player can step up without a jump.


  

### `simulation.Movement.sv_stopspeed`

The speed below which stronger stopping friction is applied.


  

### `simulation.Movement.sv_subtick_movement_view_angles`

True if the subtick view angles are used for movement.


  

### `simulation.Movement.sv_timebetweenducks`

The minimum time between two duck inputs.


  

### `simulation.Movement.sv_walkable_normal`

The minimum Z value of a surface normal for a slope that the player can walk on.


  

### `simulation.Movement.sv_water_slow_amount`

How much the player is slowed down in water.


  

### `simulation.Movement:CanMove`

```lua
simulation.Movement:CanMove(): boolean
```

Returns true if the player can move. The player cannot move while frozen, while defusing the bomb, or while arming the bomb.


  

### `simulation.Movement:CanJump`

```lua
simulation.Movement:CanJump(): boolean
```

Returns true if the player can jump. The player must be on the ground, and the jump cooldown must be over.


  

### `simulation.Movement:GetMaxSpeed`

```lua
simulation.Movement:GetMaxSpeed(): number
```

Returns the current maximum movement speed. The `forwardmove` and `leftmove` input is multiplied by this speed to get the wish velocity.


    
The value uses the current state. It includes the walk speed limit, the duck speed limit,
stamina, the slowdown from damage, the surface, the movement speed while attacking, and the
slowdown after landing.

To find the `forwardmove` or `leftmove` fraction for a given speed, divide that speed by this
value, for example `cmd.forwardmove = target_speed / sim.movement:GetMaxSpeed()`.


  


## simulation.Weapon — object type

The weapon part of a simulated player. It handles when the weapon can fire, accuracy and recoil,
reloading, and the throw parameters of grenades. Use a full simulation with
`simulation.SimOpt.kNone` to include the weapon behavior.

Reading an unknown field returns nil. Assigning an unknown field or a read-only field does
nothing. If the simulation is write protected, assigning a field throws an error.


  

### `simulation.Weapon.m_bBurstMode`

True if the weapon is in burst fire mode.


  

### `simulation.Weapon.m_bFireOnEmpty`

True if the weapon tried to fire with an empty clip.


  

### `simulation.Weapon.m_bInReload`

True while the weapon is reloading.


  

### `simulation.Weapon.m_bIsHauledBack`

True while the hammer of the revolver is pulled back.


  

### `simulation.Weapon.m_bIsHeldByPlayer`

True while the player holds the grenade.


  

### `simulation.Weapon.m_bJumpThrow`

True if the grenade is queued for a jump throw.


  

### `simulation.Weapon.m_bJustPulledPin`

True if the pin of the grenade was pulled in this tick.


  

### `simulation.Weapon.m_bPinPulled`

True if the pin of the grenade is pulled.


  

### `simulation.Weapon.m_bRedraw`

True while the weapon is drawn again after a throw.


  

### `simulation.Weapon.m_bStartedArming`

True if the player has started to arm the bomb.


  

### `simulation.Weapon.m_fAccuracyPenalty`

The inaccuracy penalty that has built up from recent actions.


  

### `simulation.Weapon.m_fLastShotTime`

The time of the last shot.


  

### `simulation.Weapon.m_fThrowTime`

The time at which the grenade is thrown.


  

### `simulation.Weapon.m_flNextAttack`

The earliest time at which the player can attack again.


  

### `simulation.Weapon.m_flNextHoldFrac`

The subtick fraction at which the next grenade hold action is ready.


  

### `simulation.Weapon.m_flNextPrimaryAttackTickRatio`

The subtick fraction at which the next primary attack is ready.


  

### `simulation.Weapon.m_flNextSecondaryAttackTickRatio`

The subtick fraction at which the next secondary attack is ready.


  

### `simulation.Weapon.m_flPostponeFireReadyFrac`

The subtick fraction at which the delayed shot is ready.


  

### `simulation.Weapon.m_flRecoilIndex`

The current recoil index. It goes up with each shot.


  

### `simulation.Weapon.m_flThrowStrength`

The throw strength of the held grenade, from 0 to 1.


  

### `simulation.Weapon.m_flWatTickOffset`

The tick offset of the weapon attack time. It is used to interpolate the shoot position.


  

### `simulation.Weapon.m_hActiveWeapon`

The weapon the player is holding. Read-only.


  

### `simulation.Weapon.m_iClip1`

The ammo in the primary clip.


  

### `simulation.Weapon.m_iClip2`

The ammo in the secondary clip.


  

### `simulation.Weapon.m_iItemDefinitionIndex`

The item definition index, which identifies the weapon type.


  

### `simulation.Weapon.m_nNextHoldTick`

The tick at which the next grenade hold action is ready.


  

### `simulation.Weapon.m_nNextPrimaryAttackTick`

The tick at which the next primary attack is ready.


  

### `simulation.Weapon.m_nNextSecondaryAttackTick`

The tick at which the next secondary attack is ready.


  

### `simulation.Weapon.m_nOldTotalInputHistoryCount`

The previous total number of recorded input history entries.


  

### `simulation.Weapon.m_nOldTotalShootPositionHistoryCount`

The previous total number of recorded shoot positions.


  

### `simulation.Weapon.m_nPostponeFireReadyTicks`

The tick at which a delayed shot, for example of the revolver, is ready.


  

### `simulation.Weapon.m_weaponMode`

The current fire mode of the weapon.


  

### `simulation.Weapon.m_zoomLevel`

The current zoom level of the scope. `0` means not zoomed.


  

### `simulation.Weapon:GetMaxSpeed`

```lua
simulation.Weapon:GetMaxSpeed(): number
```

Returns the maximum movement speed while the player holds this weapon in its current mode.


  

### `simulation.Weapon:GetInaccuracy`

```lua
simulation.Weapon:GetInaccuracy(): number
```

Returns the current inaccuracy of the weapon. It includes movement, jumping and the built up accuracy penalty.


  

### `simulation.Weapon:GetSpread`

```lua
simulation.Weapon:GetSpread(): number
```

Returns the base spread of the weapon in its current mode.


  

### `simulation.Weapon:IsPrimaryAttackReady`

```lua
simulation.Weapon:IsPrimaryAttackReady(): boolean
```

Returns true if the primary attack of the weapon is ready at the current simulation time.


  

### `simulation.Weapon:IsSecondaryAttackReady`

```lua
simulation.Weapon:IsSecondaryAttackReady(): boolean
```

Returns true if the secondary attack of the weapon is ready at the current simulation time.


  

### `simulation.Weapon:IsPostponeFireReady`

```lua
simulation.Weapon:IsPostponeFireReady(): boolean
```

Returns true if the delayed shot of the revolver is ready at the current simulation time.


  

### `simulation.Weapon:GetThrowStrength`

```lua
simulation.Weapon:GetThrowStrength(): number
```

Returns the throw strength of the held grenade, from 0 to 1.


  

### `simulation.Weapon:GetPlayerShootPosition`

```lua
simulation.Weapon:GetPlayerShootPosition(tick: TickAndInterpolationAmount_t): Vector
```

Returns the position in world space from which shots are fired at the given tick and fraction. The position is interpolated from the recorded shoot position history.


| Parameter | Type | Description |
| --- | --- | --- |
| tick | `TickAndInterpolationAmount_t` | The tick and fraction to sample. Take it from a history entry or create it with `TickAndInterpolationAmount_t(tick, fraction)`. |


    
For the shot of the current input poll, read the `shoot_position` field of the input poll
context instead.


  

  

### `simulation.Weapon:UpdateAccuracyPenalty`

```lua
simulation.Weapon:UpdateAccuracyPenalty()
```

Advances the accuracy penalty of the player. If the simulation is write protected, this function throws an error.


  

### `simulation.Weapon:IsGun`

```lua
simulation.Weapon:IsGun(): boolean
```

Returns true if the active weapon is a gun. Guns are pistols, rifles, submachine guns, shotguns, sniper rifles, machine guns and the taser.


  

### `simulation.Weapon:IsKnife`

```lua
simulation.Weapon:IsKnife(): boolean
```

Returns true if the active weapon is a knife.


  

### `simulation.Weapon:HasZoom`

```lua
simulation.Weapon:HasZoom(): boolean
```

Returns true if the active weapon has a scope with zoom levels.


  

### `simulation.Weapon:HasSecondaryAttack`

```lua
simulation.Weapon:HasSecondaryAttack(): boolean
```

Returns true if the active weapon has a secondary attack. This is true for weapons with zoom, burst mode, a removable silencer or secondary ammo, and for the revolver.


  

### `simulation.Weapon:CanAttack`

```lua
simulation.Weapon:CanAttack(mode: integer): boolean
```

Returns true if the weapon can attack in the given mode at the current simulation time.


| Parameter | Type | Description |
| --- | --- | --- |
| mode | `integer` | The attack mode to check. `0` is the primary attack and `1` is the secondary attack. |


## simulation.GrenadePoint — object type

One point of a simulated grenade path.


  

### `simulation.GrenadePoint.bounced`

True if the grenade bounced at this point.


  

### `simulation.GrenadePoint.position`

The position in world space.


  

### `simulation.GrenadePoint.tick`

The simulation tick of this point.


  

### `simulation.GrenadePoint.time`

The time since the start of the simulation, in seconds.


  

### `simulation.GrenadePoint.velocity`

The velocity at this point.


## simulation.GrenadeDamage — object type

The predicted damage of an HE grenade to one player.


  

### `simulation.GrenadeDamage.is_enemy`

True if the player is an enemy of the thrower.


  

### `simulation.GrenadeDamage.max_damage`

The highest predicted damage.


  

### `simulation.GrenadeDamage.min_damage`

The lowest predicted damage.


  

### `simulation.GrenadeDamage.passed`

True if the lowest damage reaches the health of the player or the quarter range limit of the game. It does not always mean that the grenade kills the player.


  

### `simulation.GrenadeDamage.player`

The damaged player.


## simulation.Grenade — object type

A grenade simulation that runs separately from the real game state. Each `Run` traces up to
1000 ticks, so do not run it more often than the result can change. All fields are read-only.


  

### `simulation.Grenade.definition_index`

The item definition index of the simulated grenade.


  

### `simulation.Grenade.detonated`

True if the last `Run` reached a detonation.


  

### `simulation.Grenade.detonation_time`

The detonation time in seconds, or nil if the grenade did not detonate.


  

### `simulation.Grenade.entity`

The grenade entity, or nil if there is none or it no longer exists.


  

### `simulation.Grenade.exploded_from_inferno`

The fire that set off this smoke grenade, or nil.


  

### `simulation.Grenade.extinguished_by_smoke`

The smoke that put out this grenade, or nil.


  

### `simulation.Grenade.ground_entity`

The entity that the grenade came to rest on, or nil.


  

### `simulation.Grenade.hit_enemy`

The player that the grenade hit, or nil.


  

### `simulation.Grenade.initial_position`

The start position.


  

### `simulation.Grenade.initial_velocity`

The start velocity.


  

### `simulation.Grenade.molotov_burn_position`

The position at which a molotov starts to burn, or nil.


  

### `simulation.Grenade.molotov_splash_normal`

The surface normal at which the molotov splashed, or nil.


  

### `simulation.Grenade.origin`

The current simulated origin. After `Run`, this is the final origin.


  

### `simulation.Grenade.simulated_time`

The time simulated so far, in seconds.


  

### `simulation.Grenade.thrower`

The thrower, or nil if there is none or it no longer exists.


  

### `simulation.Grenade.velocity`

The current simulated velocity.


  

### `simulation.Grenade:SetInitial`

```lua
simulation.Grenade:SetInitial(position: Vector, velocity: Vector): boolean
```

Sets the start position and the start velocity directly. If a value is not a finite vector, the function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector` | The start position. |
| velocity | `Vector` | The start velocity. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` for projectiles, or if the grenade entity no longer exists. |


  

### `simulation.Grenade:SetThrow`

```lua
simulation.Grenade:SetThrow(eye_position: Vector, angles: QAngle, velocity: Vector, strength: number[, pawn_center: Vector]): boolean
```

Sets the start state from a throw, with the same calculation as the game. If a value is not finite, the function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| eye_position | `Vector` | The eye position of the thrower. |
| angles | `QAngle` | The throw angles. |
| velocity | `Vector` | The velocity of the thrower. |
| strength | `number` | The throw strength, from 0 to 1. |
| pawn_center? | `Vector` | The center of the thrower in world space. If the simulation has no thrower, this value is required and leaving it out throws an error. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the throw could not be applied, for example for projectiles. |


  

### `simulation.Grenade:Run`

```lua
simulation.Grenade:Run(): boolean
```

Runs the simulation. You can call it again to simulate again.


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the grenade entity no longer exists, or if a grenade that is not a projectile has no start state from `SetInitial` or `SetThrow` yet. |


  

### `simulation.Grenade:GetPath`

```lua
simulation.Grenade:GetPath([time_offset: number]): simulation.GrenadePoint[]
```

Returns the simulated path.


| Parameter | Type | Description |
| --- | --- | --- |
| time_offset? | `number` | Points earlier than this many seconds are left out. The default is `0`. |


  

### `simulation.Grenade:GetBounces`

```lua
simulation.Grenade:GetBounces([time_offset: number]): simulation.GrenadePoint[]
```

Returns only the points of the simulated path at which the grenade bounced.


| Parameter | Type | Description |
| --- | --- | --- |
| time_offset? | `number` | Points earlier than this many seconds are left out. The default is `0`. |


  

### `simulation.Grenade:GetDamage`

```lua
simulation.Grenade:GetDamage([origin: Vector]): simulation.GrenadeDamage[]
```

Returns the predicted damage of an HE grenade. For other grenades, it returns an empty table.


| Parameter | Type | Description |
| --- | --- | --- |
| origin? | `Vector` | The point of the explosion. The default is the simulated detonation point. |


    
If `origin` is given, the damage is calculated at that point and `Run` is not needed. This way
you can use the end point of a recorded path directly. If `origin` is not given, the damage is
calculated at the point where the last `Run` detonated. If the grenade did not detonate, the
table is empty.

Players are checked at their positions at the time of the call, not at the time of the
detonation. Dormant, dead and immune players are left out.
