> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Vector


<a id="vector-1"></a>

## Vector  — cdata


A vector with three components. Use it for positions, directions and offsets in the world.

The components are stored as 32 bit floats. In Source 2, `x` points forward, `y` points left
and `z` points up.

The `+` and `-` operators add and subtract two vectors. The `*` and `/` operators take a
number or a vector. With a number, every component is multiplied or divided by it. With a
vector, each component is multiplied or divided by the matching component. The unary `-`
operator returns a negated copy, and the `#` operator returns the length. The `==` operator
compares every component and returns `false` when the other value is not a `Vector`.


  

### `Vector.x`

The X component, which points forward.


  

### `Vector.y`

The Y component, which points left.


  

### `Vector.z`

The Z component, which points up.


  

### `Vector / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|number` |  |


  

### `Vector * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|number` |  |


  

### `-Vector`


  

### `Vector + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `#Vector`


  

### `Vector - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


<a id="vector-2"></a>

## Vector  — ctype · callable


Call `Vector(x, y, z)` to create a vector. A component that is not given is set to 0. Call
`Vector(other)` to make a copy of another vector.

The constant vectors below cannot be changed.


  

### `Vector(x, y, z)`

```lua
Vector([x: number, y: number, z: number]): Vector
```


| Parameter | Type | Description |
| --- | --- | --- |
| x? | `number` |  |
| y? | `number` |  |
| z? | `number` |  |


  

### `Vector(self)`

```lua
Vector(self: Vector): Vector
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Vector` |  |


  

### `Vector.vForward`

The vector `(1, 0, 0)`.


  

### `Vector.vInvalid`

A vector with every component set to `FLT_MAX`, the largest 32 bit float.


  

### `Vector.vLeft`

The vector `(0, 1, 0)`.


  

### `Vector.vOne`

The vector `(1, 1, 1)`.


  

### `Vector.vUp`

The vector `(0, 0, 1)`.


  

### `Vector.vZero`

The vector `(0, 0, 0)`.


  

### `Vector.ToAngle`

```lua
Vector.ToAngle(fwd: Vector[, pseudo_up: Vector]): QAngle
```

Converts a forward direction into the angle that points along it.


| Parameter | Type | Description |
| --- | --- | --- |
| fwd | `Vector` | The forward direction. It does not need to be normalized. |
| pseudo_up? | `Vector` | An up direction used to find the roll. |


    
Without `pseudo_up`, the roll of the angle is always 0. If the direction points straight up,
the pitch is -90. If it points straight down, the pitch is 90. In both cases the yaw is 0.

With `pseudo_up`, the roll is chosen so that the up direction of the angle is as close as
possible to `pseudo_up`.


  

  

### `Vector.Copy`

```lua
Vector.Copy(src: Vector, dst: Vector)
```

Copies the components of one vector into another vector.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector` | The vector to copy from. |
| dst | `Vector` | The vector to copy into. |


  

### `Vector.Cross`

```lua
Vector.Cross(a: Vector, b: Vector): Vector
```

Returns the cross product of two vectors.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first vector. |
| b | `Vector` | The second vector. |


  

### `Vector.DistTo`

```lua
Vector.DistTo(a: Vector, b: Vector): number
```

Returns the distance between two points.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first point. |
| b | `Vector` | The second point. |


  

### `Vector.DistTo2D`

```lua
Vector.DistTo2D(a: Vector, b: Vector): number
```

Returns the distance between two points. The Z component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first point. |
| b | `Vector` | The second point. |


  

### `Vector.DistTo2DSqr`

```lua
Vector.DistTo2DSqr(a: Vector, b: Vector): number
```

Returns the squared distance between two points. The Z component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first point. |
| b | `Vector` | The second point. |


  

### `Vector.DistToSqr`

```lua
Vector.DistToSqr(a: Vector, b: Vector): number
```

Returns the squared distance between two points.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first point. |
| b | `Vector` | The second point. |


  

### `Vector.Dot`

```lua
Vector.Dot(a: Vector, b: Vector): number
```

Returns the dot product of two vectors.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first vector. |
| b | `Vector` | The second vector. |


  

### `Vector.Init`

```lua
Vector.Init(vec: Vector[, x: number, y: number, z: number])
```

Sets the components of the vector. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to change. |
| x? | `number` | The X component. |
| y? | `number` | The Y component. |
| z? | `number` | The Z component. |


  

### `Vector.Length`

```lua
Vector.Length(vec: Vector): number
```

Returns the length of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |


  

### `Vector.Length2D`

```lua
Vector.Length2D(vec: Vector): number
```

Returns the length of the vector. The Z component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |


  

### `Vector.Length2DSqr`

```lua
Vector.Length2DSqr(vec: Vector): number
```

Returns the squared length of the vector. The Z component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |


  

### `Vector.LengthSqr`

```lua
Vector.LengthSqr(vec: Vector): number
```

Returns the squared length of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |


  

### `Vector.Lerp`

```lua
Vector.Lerp(a: Vector, b: Vector, t: number): Vector
```

Returns a new vector between two vectors. This is linear interpolation.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The start vector. |
| b | `Vector` | The end vector. |
| t | `number` | The interpolation factor. 0 returns `a` and 1 returns `b`. Values below 0 or above 1 are not clamped. |


  

### `Vector.Negate`

```lua
Vector.Negate(vec: Vector)
```

Negates every component of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to negate. |


  

### `Vector.NormalizeInPlaceSafe`

```lua
Vector.NormalizeInPlaceSafe(vec: Vector, fallback: Vector): number
```

Normalizes the vector so that its length is 1. If the length is 0, the components of `fallback` are copied into the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to normalize. |
| fallback | `Vector` | The value to use when the length is 0. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of the vector before it was normalized. |


  

### `Vector.NormalizeInPlace`

```lua
Vector.NormalizeInPlace(vec: Vector): number
```

Normalizes the vector so that its length is 1. If the length is 0, the vector stays at `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to normalize. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of the vector before it was normalized. |


  

### `Vector.NormalizedSafe`

```lua
Vector.NormalizedSafe(vec: Vector, fallback: Vector): Vector
```

Returns a normalized copy of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to normalize. |
| fallback | `Vector` | The value to return when the length is 0. |


    
If the length of the vector is 0, this function returns the `fallback` object itself. It
does not make a copy, so changes to the returned vector also change `fallback`. Use
`Vector(result)` to make a separate copy.


  

  

### `Vector.Normalized`

```lua
Vector.Normalized(vec: Vector): Vector
```

Returns a normalized copy of the vector. If the length is 0, the copy is `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to normalize. |


  

### `Vector.Scale`

```lua
Vector.Scale(vec: Vector, scalar: number)
```

Multiplies every component of the vector by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to scale. |
| scalar | `number` | The number to multiply each component by. |


  

### `Vector.Scaled`

```lua
Vector.Scaled(vec: Vector, scalar: number): Vector
```

Returns a copy of the vector with every component multiplied by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to scale. |
| scalar | `number` | The number to multiply each component by. |


  

### `Vector.To`

```lua
Vector.To(a: Vector, b: Vector): Vector
```

Returns the normalized direction from `a` to `b`. If the two points are the same, the result is `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The start point. |
| b | `Vector` | The target point. |


  

### `Vector.Unpack`

```lua
Vector.Unpack(vec: Vector): number, number, number
```

Returns the X, Y and Z components of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |


  

### `Vector.RayDist`

```lua
Vector.RayDist(vec: Vector, start: Vector, dir: Vector): number
```

Returns the length of the cross product of `dir` and `vec - start`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The point to measure from. |
| start | `Vector` | A point on the line. |
| dir | `Vector` | The direction of the line. Use a normalized direction to get a real distance. |


    
When `dir` has a length of 1, this is the shortest distance from the point to the infinite
line that goes through `start` in the direction of `dir`. Points behind `start` are measured
to the same line.


  

  

### `Vector.ClosestLinePoint`

```lua
Vector.ClosestLinePoint(vec: Vector, a: Vector, b: Vector): Vector
```

Returns the point on the segment from `a` to `b` that is closest to the given point. The result is always on the segment, between `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The point to project. |
| a | `Vector` | The start of the segment. |
| b | `Vector` | The end of the segment. |


  

### `Vector.InverseLerp`

```lua
Vector.InverseLerp(vec: Vector, a: Vector, b: Vector): number, Vector
```

Projects the point onto the line through `a` and `b` and returns how far along the line it is. The factor is 0 at `a` and 1 at `b`. It is not clamped, so it can be below 0 or above 1.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The point to project. |
| a | `Vector` | The start of the segment. |
| b | `Vector` | The end of the segment. |


| Return | Type | Description |
| --- | --- | --- |
| factor | `number` | The factor and the vector `b - a`. |
| delta | `Vector` | The factor and the vector `b - a`. |


    
If the squared distance between `a` and `b` is below 0.00001, the factor is 0.


  

  

### `Vector.To2DDirection`

```lua
Vector.To2DDirection(vec: Vector): number
```

Returns the yaw of the direction in degrees, in the range from -180 to 180. A yaw of 0 points along +X, and 90 points along +Y. The value is calculated with `atan2(y, x)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The direction to measure. The Z component is ignored. |


  

### `Vector.InitFLU`

```lua
Vector.InitFLU(vec: Vector[, f: number, l: number, u: number])
```

Sets the components from forward, left and up values. A value that is not given is set to 0. In Source 2, forward is X, left is Y and up is Z, so this is the same as `Init`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to change. |
| f? | `number` | The forward component. |
| l? | `number` | The left component. |
| u? | `number` | The up component. |


  

### `Vector.FLU`

```lua
Vector.FLU([f: number, l: number, u: number]): Vector
```

Creates a vector from forward, left and up values. A value that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| f? | `number` | The forward component. |
| l? | `number` | The left component. |
| u? | `number` | The up component. |


  

### `Vector.Zero`

```lua
Vector.Zero(vec: Vector)
```

Sets every component of the vector to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to change. |


  

### `Vector.Invalidate`

```lua
Vector.Invalidate(vec: Vector)
```

Sets every component of the vector to NaN.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to change. |


  

### `Vector.IsValid`

```lua
Vector.IsValid(vec: Vector): boolean
```

Returns `true` if every component is a finite number. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to check. |


  

### `Vector.IsZero`

```lua
Vector.IsZero(vec: Vector[, tolerance: number]): boolean
```

Returns `true` if every component is greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `Vector.EqualsZero`

```lua
Vector.EqualsZero(vec: Vector): boolean
```

Returns `true` if every component is exactly 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to check. |


  

### `Vector.IsReasonable`

```lua
Vector.IsReasonable(vec: Vector[, range: number]): boolean
```

Returns `true` if the length of the vector is finite and less than `range`. Use it to check that a world position has a sensible value.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to check. |
| range? | `number` | The upper limit for the length. The default is 1000000. |


  

### `Vector.IsLengthGreaterThan`

```lua
Vector.IsLengthGreaterThan(vec: Vector, val: number): boolean
```

Returns `true` if the length of the vector is greater than `val`. The squared values are compared, so no square root is calculated.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |
| val | `number` | The length to compare with. |


  

### `Vector.IsLengthLessThan`

```lua
Vector.IsLengthLessThan(vec: Vector, val: number): boolean
```

Returns `true` if the length of the vector is less than `val`. The squared values are compared, so no square root is calculated.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to measure. |
| val | `number` | The length to compare with. |


  

### `Vector.Min`

```lua
Vector.Min(a: Vector, b: Vector): Vector
```

Returns a vector that has the smaller value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first vector. |
| b | `Vector` | The second vector. |


  

### `Vector.Max`

```lua
Vector.Max(a: Vector, b: Vector): Vector
```

Returns a vector that has the larger value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` | The first vector. |
| b | `Vector` | The second vector. |


  

### `Vector.MulAdd`

```lua
Vector.MulAdd(vec: Vector, a: Vector, b: Vector, scalar: number)
```

Sets the vector to `a + b * scalar`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to write the result into. |
| a | `Vector` | The base vector. |
| b | `Vector` | The vector to scale and add. |
| scalar | `number` | The number to multiply `b` by. |


  

### `Vector.ProjectOnto`

```lua
Vector.ProjectOnto(vec: Vector, onto: Vector): Vector
```

Returns the part of the vector that is parallel to `onto`. This is the projection of the vector onto `onto`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to project. |
| onto | `Vector` | The direction to project onto. If its length is 0, the result contains NaN. |


  

### `Vector.Flatten`

```lua
Vector.Flatten(vec: Vector, up: Vector): Vector
```

Returns a copy of the vector with the part along `up` removed. `up` is normalized first.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to flatten. |
| up | `Vector` | The direction to remove. |


  

### `Vector.LargestComponent`

```lua
Vector.LargestComponent(vec: Vector): integer
```

Returns the index of the component with the largest absolute value. The index is 0 for X, 1 for Y and 2 for Z.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to inspect. |


  

### `Vector.SmallestComponent`

```lua
Vector.SmallestComponent(vec: Vector): integer
```

Returns the index of the component with the smallest absolute value. The index is 0 for X, 1 for Y and 2 for Z.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to inspect. |


  

### `Vector.LargestComponentValue`

```lua
Vector.LargestComponentValue(vec: Vector): number
```

Returns the largest absolute value of the three components.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to inspect. |


  

### `Vector.SmallestComponentValue`

```lua
Vector.SmallestComponentValue(vec: Vector): number
```

Returns the smallest absolute value of the three components.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to inspect. |


  

### `Vector.AsVector2D`

```lua
Vector.AsVector2D(vec: Vector): Vector2D
```

Returns a `Vector2D` that shares the memory of the X and Y components of the vector. Changes to the `Vector2D` also change the vector. Keep the vector alive for as long as you use the `Vector2D`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to view. |


  

### `Vector.GetLeftVectors`

```lua
Vector.GetLeftVectors(fwd: Vector): Vector, Vector
```

Returns the left and up directions for a forward direction. Both results are normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| fwd | `Vector` | The forward direction. It does not need to be normalized. |


| Return | Type | Description |
| --- | --- | --- |
| left | `Vector` |  |
| up | `Vector` |  |


    
If the forward direction points almost straight up or down, the left direction is
`(0, 1, 0)`.


  

  

### `Vector.GetRightVectors`

```lua
Vector.GetRightVectors(fwd: Vector): Vector, Vector
```

Returns the right and up directions for a forward direction. Both results are normalized. The right direction is the negated left direction from `GetLeftVectors`.


| Parameter | Type | Description |
| --- | --- | --- |
| fwd | `Vector` | The forward direction. It does not need to be normalized. |


| Return | Type | Description |
| --- | --- | --- |
| right | `Vector` |  |
| up | `Vector` |  |


  

### `Vector.Get2DDirection`

```lua
Vector.Get2DDirection(vec: Vector, other: Vector): number
```

Returns the yaw in degrees of the direction from `other` to this vector, in the range from -180 to 180. The Z component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The end point. |
| other | `Vector` | The start point. |


  

### `Vector.GetVectorDirection2D`

```lua
Vector.GetVectorDirection2D(vec: Vector, b: Vector): Vector
```

Returns the normalized direction from `b` to this vector, with the Z component set to 0. If the two points have the same X and Y, the result is `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The end point. |
| b | `Vector` | The start point. |


  

### `Vector.IsIntersect`

```lua
Vector.IsIntersect(vec: Vector, v: Vector, tolerance: number, ignore_z: boolean): boolean
```

Returns `true` if the difference between each compared component of the two points is less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The first point. |
| v | `Vector` | The second point. |
| tolerance | `number` | The tolerance for each component. |
| ignore_z | `boolean` | If `true`, only X and Y are compared. |


  

### `Vector.OffsetX`

```lua
Vector.OffsetX(vec: Vector, d: number): Vector
```

Returns a copy of the vector with `d` subtracted from the X component.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to read. |
| d | `number` | The amount to subtract. |


  

### `Vector.OffsetY`

```lua
Vector.OffsetY(vec: Vector, d: number): Vector
```

Returns a copy of the vector with `d` subtracted from the Y component.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to read. |
| d | `number` | The amount to subtract. |


  

### `Vector.OffsetZ`

```lua
Vector.OffsetZ(vec: Vector, d: number): Vector
```

Returns a copy of the vector with `d` subtracted from the Z component.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` | The vector to read. |
| d | `number` | The amount to subtract. |
