> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Vector 4D


## Vector4D — cdata


A vector with four float components. It is used by convars of type `CONVAR_TYPE_VECTOR4D`
and by homogeneous coordinates, for example in `VMatrix.V4Mul`.

The `+` and `-` operators add and subtract two vectors. The `*` and `/` operators take a
number or a vector. With a number, every component is multiplied or divided by it. With a
vector, each component is multiplied or divided by the matching component. The unary `-`
operator returns a negated copy, and the `#` operator returns the length. The `==` operator
compares every component and returns `false` when the other value is not a `Vector4D`.

```cpp lines=false
typedef struct Vector4D {
    float x, y, z, w;
} Vector4D;
```


  

### `Vector4D.w`

The W component.


  

### `Vector4D.x`

The X component.


  

### `Vector4D.y`

The Y component.


  

### `Vector4D.z`

The Z component.


  

### `Vector4D + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector4D` |  |


  

### `Vector4D - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector4D` |  |


  

### `Vector4D * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector4D\|number` |  |


  

### `Vector4D / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector4D\|number` |  |


  

<a id="vector4d"></a>
### `-Vector4D`


  

<a id="vector4d"></a>
### `#Vector4D`


<a id="vector4d-1"></a>

## Vector4D  — ctype · callable


Call `Vector4D()` to create a vector with every component set to 0. Call
`Vector4D(x, y, z, w)` to set the components. A component that is not given is set to 0.
Call `Vector4D(xyz, w)` with a `Vector` or `VectorAligned` to take X, Y and Z from it. If `w`
is not given, it is set to 0. Call `Vector4D(other)` to make a copy of another `Vector4D`.

Any other first argument throws an error.


  

<a id="vector4d"></a>
### `Vector4D()`

```lua
Vector4D(): Vector4D
```


  

### `Vector4D(x, y, z, w)`

```lua
Vector4D(x: number[, y: number, z: number, w: number]): Vector4D
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |
| w? | `number` |  |


  

### `Vector4D(xyz, w)`

```lua
Vector4D(xyz: Vector|VectorAligned[, w: number]): Vector4D
```


| Parameter | Type | Description |
| --- | --- | --- |
| xyz | `Vector\|VectorAligned` |  |
| w? | `number` |  |


  

### `Vector4D(self)`

```lua
Vector4D(self: Vector4D): Vector4D
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Vector4D` |  |


  

### `Vector4D.Unpack`

```lua
Vector4D.Unpack(v: Vector4D): number, number, number, number
```

Returns the X, Y, Z and W components of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |
| w | `number` |  |


  

### `Vector4D.Copy`

```lua
Vector4D.Copy(src: Vector4D, dst: Vector4D)
```

Copies the components of one vector into another vector.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector4D` | The vector to copy from. |
| dst | `Vector4D` | The vector to copy into. |


  

### `Vector4D.Init`

```lua
Vector4D.Init(v: Vector4D[, x: number, y: number, z: number, w: number])
```

Sets the components of the vector from four numbers. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to change. |
| x? | `number` | The X component. |
| y? | `number` | The Y component. |
| z? | `number` | The Z component. |
| w? | `number` | The W component. |


  

### `Vector4D.Init`

```lua
Vector4D.Init(v: Vector4D, xyz: Vector|VectorAligned[, w: number])
```

Sets the components of the vector from a 3D vector and a W value.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to change. |
| xyz | `Vector\|VectorAligned` | The vector to take the X, Y and Z components from. |
| w? | `number` | The W component. The default is 0. |


  

### `Vector4D.Zero`

```lua
Vector4D.Zero(v: Vector4D)
```

Sets every component of the vector to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to change. |


  

### `Vector4D.Negate`

```lua
Vector4D.Negate(v: Vector4D)
```

Negates every component of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to change. |


  

### `Vector4D.MulAdd`

```lua
Vector4D.MulAdd(v: Vector4D, a: Vector4D, b: Vector4D, scalar: number)
```

Sets the vector to `a + b * scalar`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to write the result into. |
| a | `Vector4D` | The base vector. |
| b | `Vector4D` | The vector to scale and add. |
| scalar | `number` | The number to multiply `b` by. |


  

### `Vector4D.Dot`

```lua
Vector4D.Dot(a: Vector4D, b: Vector4D): number
```

Returns the dot product of two vectors. All four components are used.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The first vector. |
| b | `Vector4D` | The second vector. |


  

### `Vector4D.Length`

```lua
Vector4D.Length(v: Vector4D): number
```

Returns the length of the vector. All four components are used.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to measure. |


  

### `Vector4D.LengthSqr`

```lua
Vector4D.LengthSqr(v: Vector4D): number
```

Returns the squared length of the vector. All four components are used.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to measure. |


  

### `Vector4D.DistTo`

```lua
Vector4D.DistTo(a: Vector4D, b: Vector4D): number
```

Returns the distance between two points. All four components are used.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The first point. |
| b | `Vector4D` | The second point. |


  

### `Vector4D.DistToSqr`

```lua
Vector4D.DistToSqr(a: Vector4D, b: Vector4D): number
```

Returns the squared distance between two points. All four components are used.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The first point. |
| b | `Vector4D` | The second point. |


  

### `Vector4D.IsValid`

```lua
Vector4D.IsValid(v: Vector4D): boolean
```

Returns `true` if every component is a finite number. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to check. |


  

### `Vector4D.IsZero`

```lua
Vector4D.IsZero(v: Vector4D[, tolerance: number]): boolean
```

Returns `true` if every component is greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `Vector4D.AsVector3D`

```lua
Vector4D.AsVector3D(v: Vector4D): Vector
```

Returns a `Vector` that shares the memory of the X, Y and Z components of this vector. Changes to the `Vector` also change this vector. Keep this vector alive for as long as you use the `Vector`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to view. |


  

### `Vector4D.AsVector2D`

```lua
Vector4D.AsVector2D(v: Vector4D): Vector2D
```

Returns a `Vector2D` that shares the memory of the X and Y components of this vector. Changes to the `Vector2D` also change this vector. Keep this vector alive for as long as you use the `Vector2D`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to view. |


  

### `Vector4D.NormalizeInPlace`

```lua
Vector4D.NormalizeInPlace(v: Vector4D): number
```

Normalizes the vector so that its length is 1. If the length is 0, the vector stays at `(0, 0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to normalize. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of the vector before it was normalized. |


  

### `Vector4D.Normalized`

```lua
Vector4D.Normalized(v: Vector4D): Vector4D
```

Returns a normalized copy of the vector. If the length is 0, the copy is `(0, 0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to normalize. |


  

### `Vector4D.Lerp`

```lua
Vector4D.Lerp(a: Vector4D, b: Vector4D, t: number): Vector4D
```

Returns a new vector between two vectors. This is linear interpolation.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The start vector. |
| b | `Vector4D` | The end vector. |
| t | `number` | The interpolation factor. 0 returns `a` and 1 returns `b`. Values below 0 or above 1 are not clamped. |


  

### `Vector4D.Min`

```lua
Vector4D.Min(a: Vector4D, b: Vector4D): Vector4D
```

Returns a vector that has the smaller value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The first vector. |
| b | `Vector4D` | The second vector. |


  

### `Vector4D.Max`

```lua
Vector4D.Max(a: Vector4D, b: Vector4D): Vector4D
```

Returns a vector that has the larger value of each component of `a` and `b`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector4D` | The first vector. |
| b | `Vector4D` | The second vector. |


  

### `Vector4D.Abs`

```lua
Vector4D.Abs(v: Vector4D): Vector4D
```

Returns a copy of the vector with the absolute value of each component.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector4D` | The vector to read. |
