> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Vector 2D


## Vector2D — cdata


A vector with two components, stored as `cdata<struct Vector2D>`.

The `+` and `-` operators add and subtract two vectors. The `*` and `/` operators take a
number or a vector. With a number, every component is multiplied or divided by it. With a
vector, each component is multiplied or divided by the matching component. The unary `-`
operator returns a negated copy, and the `#` operator returns the length. The `==` operator
compares both components and returns `false` when the other value is not a `Vector2D`.


  

### `Vector2D.x`

The X component.


  

### `Vector2D.y`

The Y component.


  

### `Vector2D + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector2D` |  |


  

### `Vector2D - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector2D` |  |


  

### `Vector2D * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector2D\|number` |  |


  

### `Vector2D / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector2D\|number` |  |


  

<a id="vector2d"></a>
### `-Vector2D`


  

<a id="vector2d"></a>
### `#Vector2D`


<a id="vector2d-1"></a>

## Vector2D  — ctype · callable


Call `Vector2D(x, y)` to create a vector. A component that is not given is set to 0. Call
`Vector2D(other)` to make a copy of another vector.

The constant vectors below cannot be changed.


  

### `Vector2D(x, y)`

```lua
Vector2D([x: number, y: number]): Vector2D
```


| Parameter | Type | Description |
| --- | --- | --- |
| x? | `number` |  |
| y? | `number` |  |


  

### `Vector2D(self)`

```lua
Vector2D(self: Vector2D): Vector2D
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Vector2D` |  |


  

### `Vector2D.vOne`

The vector `(1, 1)`.


  

### `Vector2D.vZero`

The vector `(0, 0)`.


  

### `Vector2D.Unpack`

```lua
Vector2D.Unpack(vec: Vector2D): number, number
```

Returns the X and Y components of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |


  

### `Vector2D.Copy`

```lua
Vector2D.Copy(src: Vector2D, dst: Vector2D)
```

Copies the components of one vector into another vector.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector2D` | The vector to copy from. |
| dst | `Vector2D` | The vector to copy into. |


  

### `Vector2D.Init`

```lua
Vector2D.Init(vec: Vector2D[, x: number, y: number])
```

Sets the components of the vector. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to change. |
| x? | `number` | The X component. |
| y? | `number` | The Y component. |


  

### `Vector2D.AsVector`

```lua
Vector2D.AsVector(vec: Vector2D, z: number): Vector
```

Returns a new `Vector` with the X and Y components of this vector and the given Z component.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to convert. |
| z | `number` | The Z component of the new vector. This argument is required. |


  

### `Vector2D.Cross`

```lua
Vector2D.Cross(a: Vector2D, b: Vector2D): number
```

Returns the 2D cross product of two vectors. This is the Z component of the 3D cross product, `a.x * b.y - a.y * b.x`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first vector. |
| b | `Vector2D` | The second vector. |


  

### `Vector2D.DistTo`

```lua
Vector2D.DistTo(a: Vector2D, b: Vector2D): number
```

Returns the distance between two points.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first point. |
| b | `Vector2D` | The second point. |


  

### `Vector2D.DistToSqr`

```lua
Vector2D.DistToSqr(a: Vector2D, b: Vector2D): number
```

Returns the squared distance between two points.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first point. |
| b | `Vector2D` | The second point. |


  

### `Vector2D.Dot`

```lua
Vector2D.Dot(a: Vector2D, b: Vector2D): number
```

Returns the dot product of two vectors.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first vector. |
| b | `Vector2D` | The second vector. |


  

### `Vector2D.Length`

```lua
Vector2D.Length(vec: Vector2D): number
```

Returns the length of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to measure. |


  

### `Vector2D.LengthSqr`

```lua
Vector2D.LengthSqr(vec: Vector2D): number
```

Returns the squared length of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to measure. |


  

### `Vector2D.Lerp`

```lua
Vector2D.Lerp(a: Vector2D, b: Vector2D, t: number): Vector2D
```

Returns a new vector between two vectors. This is linear interpolation.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The start vector. |
| b | `Vector2D` | The end vector. |
| t | `number` | The interpolation factor. 0 returns `a` and 1 returns `b`. Values below 0 or above 1 are not clamped. |


  

### `Vector2D.NormalizeInPlace`

```lua
Vector2D.NormalizeInPlace(vec: Vector2D): number
```

Normalizes the vector so that its length is 1. If the length is 0, the vector stays at `(0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to normalize. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of the vector before it was normalized. |


  

### `Vector2D.Normalized`

```lua
Vector2D.Normalized(vec: Vector2D): Vector2D
```

Returns a normalized copy of the vector. If the length is 0, the copy is `(0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to normalize. |


  

### `Vector2D.Scale`

```lua
Vector2D.Scale(vec: Vector2D, s: number)
```

Multiplies both components of the vector by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to scale. |
| s | `number` | The number to multiply each component by. |


  

### `Vector2D.Scaled`

```lua
Vector2D.Scaled(vec: Vector2D, s: number): Vector2D
```

Returns a copy of the vector with both components multiplied by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to scale. |
| s | `number` | The number to multiply each component by. |


  

### `Vector2D.To2DDirection`

```lua
Vector2D.To2DDirection(vec: Vector2D): number
```

Returns the direction of the vector in degrees, in the range from -180 to 180. An angle of 0 points along +X, and 90 points along +Y. The value is calculated with `atan2(y, x)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The direction to measure. |


  

### `Vector2D.Zero`

```lua
Vector2D.Zero(vec: Vector2D)
```

Sets both components of the vector to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to change. |


  

### `Vector2D.IsZero`

```lua
Vector2D.IsZero(vec: Vector2D[, tolerance: number]): boolean
```

Returns `true` if both components are greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `Vector2D.IsValid`

```lua
Vector2D.IsValid(vec: Vector2D): boolean
```

Returns `true` if both components are finite numbers. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to check. |


  

### `Vector2D.Negate`

```lua
Vector2D.Negate(vec: Vector2D)
```

Negates both components of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to change. |


  

### `Vector2D.MulAdd`

```lua
Vector2D.MulAdd(vec: Vector2D, a: Vector2D, b: Vector2D, scalar: number)
```

Sets the vector to `a + b * scalar`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to write the result into. |
| a | `Vector2D` | The base vector. |
| b | `Vector2D` | The vector to scale and add. |
| scalar | `number` | The number to multiply `b` by. |


  

### `Vector2D.Min`

```lua
Vector2D.Min(a: Vector2D, b: Vector2D): Vector2D
```

Returns a vector that has the smaller value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first vector. |
| b | `Vector2D` | The second vector. |


  

### `Vector2D.Max`

```lua
Vector2D.Max(a: Vector2D, b: Vector2D): Vector2D
```

Returns a vector that has the larger value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first vector. |
| b | `Vector2D` | The second vector. |


  

### `Vector2D.LargestComponentValue`

```lua
Vector2D.LargestComponentValue(vec: Vector2D): number
```

Returns the component with the larger absolute value. The sign of the component is kept. If both have the same absolute value, Y is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to inspect. |


  

### `Vector2D.IsLengthGreaterThan`

```lua
Vector2D.IsLengthGreaterThan(vec: Vector2D, val: number): boolean
```

Returns `true` if the length of the vector is greater than `val`. The squared values are compared, so no square root is calculated.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to measure. |
| val | `number` | The length to compare with. |


  

### `Vector2D.IsLengthLessThan`

```lua
Vector2D.IsLengthLessThan(vec: Vector2D, val: number): boolean
```

Returns `true` if the length of the vector is less than `val`. The squared values are compared, so no square root is calculated.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to measure. |
| val | `number` | The length to compare with. |


  

### `Vector2D.NormalizeInPlaceSafe`

```lua
Vector2D.NormalizeInPlaceSafe(vec: Vector2D, fallback: Vector2D): number
```

Normalizes the vector so that its length is 1. If the length is 0, the components of `fallback` are copied into the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to normalize. |
| fallback | `Vector2D` | The value to use when the length is 0. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of the vector before it was normalized. |


  

### `Vector2D.NormalizedSafe`

```lua
Vector2D.NormalizedSafe(vec: Vector2D, fallback: Vector2D): Vector2D
```

Returns a normalized copy of the vector. If the length is 0, a copy of `fallback` is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector2D` | The vector to normalize. |
| fallback | `Vector2D` | The value to return when the length is 0. |
