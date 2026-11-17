> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Motion


## motion.WalkTo.Options — object type

Options for `motion.WalkTo`. All fields are optional. If `approach` or `stop` is not a value of
its enum, `motion.WalkTo` throws an error.


  

### `motion.WalkTo.Options.approach`

How the path toward the target is shaped. The default is `motion.ApproachMode.kArc`.


  

### `motion.WalkTo.Options.nudge`

Allows small corrections near the target. The default is `true`.


  

### `motion.WalkTo.Options.stop`

How the point to start stopping is chosen. The default is `motion.StopMode.kClosest`.


  

### `motion.WalkTo.Options.velocity`

The velocity that the player should have on arrival, in units per second. Use it to follow a moving target. The default is a zero vector.


  

### `motion.WalkTo.Options.walk`

Pass `true` to always walk, and `false` to always run. If it is nil, the walk key of the user is kept.


## motion.Status — object type

The result of the last command that the planner planned. It is returned by `motion.Status`.


  

### `motion.Status.command_number`

The number of the command that this status was planned for.


  

### `motion.Status.distance`

The distance that is left to the target.


  

<a id="motion-Status-Phase"></a>
### `motion.Status.phase`

The current phase of the planner.


  

### `motion.Status.predicted_miss`

The predicted distance by which the player misses the target. It is nil when there is no prediction.


  

### `motion.Status.speed`

The planned speed for the command.


  

### `motion.Status.ticks_to_rest`

The predicted number of ticks until the player stops. It is nil when there is no prediction.


  

<a id="motion-Status-Phase"></a>
### `motion.Status.Phase`

The phase of the movement planner, returned in `motion.Status`.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "approach" |  | Moving toward the target position. |
| "solve" |  | Calculating where to start stopping. |
| "bleed" |  | Losing speed before the stop. |
| "track" |  | Following a moving target. |
| "nudge" |  | Making a last small correction. |
| "hold" |  | Staying at the target. The player also stays in place when a wall or another object stops a nudge from getting closer. |


<a id="motion-1"></a>

## motion  — global table


  

### `motion.WalkTo`

```lua
motion.WalkTo(target: Vector[, options: motion.WalkTo.Options])
```

Asks the movement planner to walk the local player to `target`. The request is valid only for the command that is being built, so call this function in every `pre_movement` event.


| Parameter | Type | Description |
| --- | --- | --- |
| target | `Vector` | The position to walk to. |
| options? | `motion.WalkTo.Options` | Options for the planner. |


    
If `options` is not a table or nil, the function throws an error.


  

  

### `motion.Active`

```lua
motion.Active(): boolean
```

Returns true if a `motion.WalkTo` request is active for the command that is being built.


  

<a id="motionstatus"></a>
### `motion.Status`

```lua
motion.Status(): motion.Status?
```

Returns the result of the last command that the planner planned.


    
In the `pre_movement` event, this is the result of the previous command, because the current
command is planned after the event returns. In the `post_movement` event, this is the result of
the current command.

Returns nil if the planner did not control the last command.


  

  

<a id="motion-ApproachMode"></a>
### `motion.ApproachMode`

How `motion.WalkTo` shapes the path toward the target.


    

### `motion.ApproachMode`


| Name | Value | Description |
| --- | --- | --- |
| kArc | 0 | Turns the current velocity onto the line through the target and keeps the speed. |
| kStop | 1 | Stops completely when the direction is wrong, then speeds up straight toward the target. |


  

  

<a id="motion-StopMode"></a>
### `motion.StopMode`

How `motion.WalkTo` chooses the point at which the player starts stopping.


    

### `motion.StopMode`


| Name | Value | Description |
| --- | --- | --- |
| kClosest | 0 | The point after which the player is predicted to stop closest to the target. |
| kSafest | 1 | The point after which the player is predicted to stop before the target. The player never stops past it. |
