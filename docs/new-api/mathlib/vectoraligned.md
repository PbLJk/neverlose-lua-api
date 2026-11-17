> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Aligned Vector


## VectorAligned — cdata


A 3D vector that is aligned to 16 bytes. It has a fourth component `w`. In a plain vector,
`w` is padding and is usually 0. Inside a `CTransform`, `w` holds the uniform scale. The
arithmetic operators treat `w` as a real component and include it in the result.

The `+`, `-`, `*` and `/` operators take a `VectorAligned` or a `Vector` on the right side.
A `Vector` is treated as having `w = 0`. The `*` and `/` operators also take a number, which
multiplies or divides all four components. The unary `-` operator negates all four
components. The `#` operator returns the length of X, Y and Z.

When a `Vector` is on the left side of an operator, the `Vector` operator is used, so the
result is a `Vector`.

The `==` operator compares only X, Y and Z, and it returns `false` when the other value is
not a `VectorAligned`. Use `IsEqual4D` to compare all four components.

```cpp lines=false
typedef struct __declspec(align(16)) VectorAligned {
    float x, y, z, w;
} VectorAligned;
```


  

### `VectorAligned.w`

The fourth component. It is 0 for a plain vector and holds the scale inside a `CTransform`.


  

### `VectorAligned.x`

The X component.


  

### `VectorAligned.y`

The Y component.


  

### `VectorAligned.z`

The Z component.


  

### `VectorAligned + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned\|Vector` |  |


  

### `VectorAligned - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned\|Vector` |  |


  

### `VectorAligned * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned\|Vector\|number` |  |


  

### `VectorAligned / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned\|Vector\|number` |  |


  

<a id="vectoraligned"></a>
### `-VectorAligned`


  

<a id="vectoraligned"></a>
### `#VectorAligned`


<a id="vectoraligned-1"></a>

## VectorAligned  — ctype · callable


Call `VectorAligned()` to create a vector with every component set to 0. Call
`VectorAligned(x, y, z, w)` to set the components. A component that is not given is set to
0\. Call `VectorAligned(vec)` with a `Vector` to copy X, Y and Z and set `w` to 0. Call
`VectorAligned(other)` to make a copy of another `VectorAligned`.

Any other first argument throws an error.

The constant vectors below cannot be changed. Their `w` component is 0.


  

<a id="vectoraligned"></a>
### `VectorAligned()`

```lua
VectorAligned(): VectorAligned
```


  

### `VectorAligned(x, y, z, w)`

```lua
VectorAligned(x: number[, y: number, z: number, w: number]): VectorAligned
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |
| w? | `number` |  |


  

### `VectorAligned(vec)`

```lua
VectorAligned(vec: Vector): VectorAligned
```


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `Vector` |  |


  

### `VectorAligned(self)`

```lua
VectorAligned(self: VectorAligned): VectorAligned
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `VectorAligned` |  |


  

### `VectorAligned.vBackward`

The vector `(-1, 0, 0)`.


  

### `VectorAligned.vDown`

The vector `(0, 0, -1)`.


  

### `VectorAligned.vForward`

The vector `(1, 0, 0)`.


  

### `VectorAligned.vLeft`

The vector `(0, 1, 0)`.


  

### `VectorAligned.vNegativeOne`

The vector `(-1, -1, -1)`.


  

### `VectorAligned.vOne`

The vector `(1, 1, 1)`.


  

### `VectorAligned.vRight`

The vector `(0, -1, 0)`.


  

### `VectorAligned.vUp`

The vector `(0, 0, 1)`.


  

### `VectorAligned.vZero`

The vector `(0, 0, 0)`.


  

### `VectorAligned.Unpack`

```lua
VectorAligned.Unpack(vec: VectorAligned): number, number, number, number
```

Returns the X, Y, Z and W components of the vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |
| w | `number` |  |


  

### `VectorAligned.Copy`

```lua
VectorAligned.Copy(src: VectorAligned, dst: VectorAligned)
```

Copies all four components of one vector into another vector.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `VectorAligned` | The vector to copy from. |
| dst | `VectorAligned` | The vector to copy into. |


  

### `VectorAligned.Init`

```lua
VectorAligned.Init(vec: VectorAligned[, x: number, y: number, z: number])
```

Sets the X, Y and Z components of the vector and sets `w` to 0. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to change. |
| x? | `number` | The X component. |
| y? | `number` | The Y component. |
| z? | `number` | The Z component. |


  

### `VectorAligned.InitZero`

```lua
VectorAligned.InitZero(vec: VectorAligned)
```

Sets all four components of the vector to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to change. |


  

### `VectorAligned.IsValid`

```lua
VectorAligned.IsValid(vec: VectorAligned): boolean
```

Returns `true` if X, Y and Z are finite numbers. NaN and infinity are not finite. The `w` component is not checked.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |


  

### `VectorAligned.Length`

```lua
VectorAligned.Length(vec: VectorAligned): number
```

Returns the length of X, Y and Z.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to measure. |


  

### `VectorAligned.Length2D`

```lua
VectorAligned.Length2D(vec: VectorAligned): number
```

Returns the length of X and Y.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to measure. |


  

### `VectorAligned.Length4D`

```lua
VectorAligned.Length4D(vec: VectorAligned): number
```

Returns the length of all four components.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to measure. |


  

### `VectorAligned.LengthSqr`

```lua
VectorAligned.LengthSqr(vec: VectorAligned): number
```

Returns the squared length of X, Y and Z.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to measure. |


  

### `VectorAligned.LengthSqr2D`

```lua
VectorAligned.LengthSqr2D(vec: VectorAligned): number
```

Returns the squared length of X and Y.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to measure. |


  

### `VectorAligned.NormalizeInPlace`

```lua
VectorAligned.NormalizeInPlace(vec: VectorAligned): number
```

Normalizes X, Y and Z so that their length is 1. The `w` component does not change. If the length is 0, X, Y and Z stay at 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of X, Y and Z before the vector was normalized. |


  

### `VectorAligned.NormalizeInPlaceSafe`

```lua
VectorAligned.NormalizeInPlaceSafe(vec: VectorAligned, fallback: VectorAligned|Vector): number
```

Normalizes X, Y and Z so that their length is 1. The `w` component does not change. If the length is 0, X, Y and Z are copied from `fallback`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |
| fallback | `VectorAligned\|Vector` | The value to use when the length is 0. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of X, Y and Z before the vector was normalized. |


  

### `VectorAligned.Normalized`

```lua
VectorAligned.Normalized(vec: VectorAligned): VectorAligned
```

Returns a copy of the vector with X, Y and Z normalized. The `w` component does not change. If the length is 0, X, Y and Z of the copy are 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |


  

### `VectorAligned.NormalizedSafe`

```lua
VectorAligned.NormalizedSafe(vec: VectorAligned, fallback: VectorAligned): VectorAligned
```

Returns a copy of the vector with X, Y and Z normalized. The `w` component does not change. If the length of X, Y and Z is 0, a copy of all four components of `fallback` is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |
| fallback | `VectorAligned` | The value to return when the length is 0. |


  

### `VectorAligned.NormalizeInPlace2D`

```lua
VectorAligned.NormalizeInPlace2D(vec: VectorAligned): number
```

Normalizes X and Y so that their length is 1. The Z and W components do not change. If the length is 0, X and Y stay at 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of X and Y before the vector was normalized. |


  

### `VectorAligned.NormalizeInPlaceSafe2D`

```lua
VectorAligned.NormalizeInPlaceSafe2D(vec: VectorAligned, fallback: VectorAligned|Vector): number
```

Normalizes X and Y so that their length is 1. The Z and W components do not change. If the length is 0, X and Y are copied from `fallback`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |
| fallback | `VectorAligned\|Vector` | The value whose X and Y are used when the length is 0. |


| Return | Type | Description |
| --- | --- | --- |
|  | `number` | The length of X and Y before the vector was normalized. |


  

### `VectorAligned.Normalized2D`

```lua
VectorAligned.Normalized2D(vec: VectorAligned): VectorAligned
```

Returns a copy of the vector with X and Y normalized. The Z and W components do not change. If the length is 0, X and Y of the copy are 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |


  

### `VectorAligned.NormalizedSafe2D`

```lua
VectorAligned.NormalizedSafe2D(vec: VectorAligned, fallback: VectorAligned): VectorAligned
```

Returns a copy of the vector with X and Y normalized. The Z and W components do not change. If the length of X and Y is 0, a copy of all four components of `fallback` is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to normalize. |
| fallback | `VectorAligned` | The value to return when the length is 0. |


  

### `VectorAligned.Dot`

```lua
VectorAligned.Dot(a: VectorAligned, b: VectorAligned|Vector): number
```

Returns the dot product of X, Y and Z of two vectors.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned\|Vector` | The second vector. |


  

### `VectorAligned.Dot2D`

```lua
VectorAligned.Dot2D(a: VectorAligned, b: VectorAligned|Vector): number
```

Returns the dot product of X and Y of two vectors.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned\|Vector` | The second vector. |


  

### `VectorAligned.Cross`

```lua
VectorAligned.Cross(a: VectorAligned, b: VectorAligned|Vector): VectorAligned
```

Returns the cross product of X, Y and Z of two vectors. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned\|Vector` | The second vector. |


  

### `VectorAligned.Abs`

```lua
VectorAligned.Abs(vec: VectorAligned): VectorAligned
```

Returns a copy of the vector with the absolute value of all four components.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to read. |


  

### `VectorAligned.Min`

```lua
VectorAligned.Min(a: VectorAligned, b: VectorAligned|Vector): VectorAligned
```

Returns a vector that has the smaller value of each of the four components of `a` and `b`. A `Vector` is treated as having `w = 0`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned\|Vector` | The second vector. |


  

### `VectorAligned.Max`

```lua
VectorAligned.Max(a: VectorAligned, b: VectorAligned|Vector): VectorAligned
```

Returns a vector that has the larger value of each of the four components of `a` and `b`. A `Vector` is treated as having `w = 0`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned\|Vector` | The second vector. |


  

### `VectorAligned.AsVector`

```lua
VectorAligned.AsVector(vec: VectorAligned): Vector
```

Returns a new `Vector` with the X, Y and Z components of this vector.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to convert. |


  

### `VectorAligned.AsVector3D`

```lua
VectorAligned.AsVector3D(vec: VectorAligned): Vector
```

Returns a new `Vector` with the X, Y and Z components of this vector. This is the same function as `AsVector`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to convert. |


  

### `VectorAligned.LargestComponentValue`

```lua
VectorAligned.LargestComponentValue(vec: VectorAligned): number
```

Returns the largest absolute value of X, Y and Z. The `w` component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to read. |


  

### `VectorAligned.SmallestComponentValue`

```lua
VectorAligned.SmallestComponentValue(vec: VectorAligned): number
```

Returns the smallest absolute value of X, Y and Z. The `w` component is ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to read. |


  

### `VectorAligned.IsZero`

```lua
VectorAligned.IsZero(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if X, Y and Z are each greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.IsZero2D`

```lua
VectorAligned.IsZero2D(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if X and Y are each greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.IsZero4D`

```lua
VectorAligned.IsZero4D(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if all four components are each greater than `-tolerance` and less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.EqualsZero`

```lua
VectorAligned.EqualsZero(vec: VectorAligned): boolean
```

Returns `true` if X, Y and Z are exactly 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |


  

### `VectorAligned.EqualsZero2D`

```lua
VectorAligned.EqualsZero2D(vec: VectorAligned): boolean
```

Returns `true` if X and Y are exactly 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |


  

### `VectorAligned.EqualsZero4D`

```lua
VectorAligned.EqualsZero4D(vec: VectorAligned): boolean
```

Returns `true` if all four components are exactly 0.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |


  

### `VectorAligned.IsEqual2D`

```lua
VectorAligned.IsEqual2D(a: VectorAligned, b: VectorAligned): boolean
```

Returns `true` if X and Y of the two vectors are exactly equal.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned` | The second vector. |


  

### `VectorAligned.IsEqual4D`

```lua
VectorAligned.IsEqual4D(a: VectorAligned, b: VectorAligned): boolean
```

Returns `true` if all four components of the two vectors are exactly equal.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned` | The second vector. |


  

### `VectorAligned.IsApproximatelyEqual`

```lua
VectorAligned.IsApproximatelyEqual(a: VectorAligned, b: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if the difference between X, Y and Z of the two vectors is less than `tolerance` for each component.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned` | The second vector. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.IsApproximatelyEqual2D`

```lua
VectorAligned.IsApproximatelyEqual2D(a: VectorAligned, b: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if the difference between X and Y of the two vectors is less than `tolerance` for each component.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned` | The second vector. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.IsApproximatelyEqual4D`

```lua
VectorAligned.IsApproximatelyEqual4D(a: VectorAligned, b: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if the difference between all four components of the two vectors is less than `tolerance` for each component.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `VectorAligned` | The first vector. |
| b | `VectorAligned` | The second vector. |
| tolerance? | `number` | The tolerance for each component. The default is 0.01. |


  

### `VectorAligned.IsApproximatelyZero`

```lua
VectorAligned.IsApproximatelyZero(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if X, Y and Z are each greater than `-tolerance` and less than `tolerance`. This is the same as `IsZero` with a smaller default tolerance.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.0001. |


  

### `VectorAligned.IsApproximatelyZero2D`

```lua
VectorAligned.IsApproximatelyZero2D(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if X and Y are each greater than `-tolerance` and less than `tolerance`. This is the same as `IsZero2D` with a smaller default tolerance.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.0001. |


  

### `VectorAligned.IsApproximatelyZero4D`

```lua
VectorAligned.IsApproximatelyZero4D(vec: VectorAligned[, tolerance: number]): boolean
```

Returns `true` if all four components are each greater than `-tolerance` and less than `tolerance`. This is the same as `IsZero4D` with a smaller default tolerance.


| Parameter | Type | Description |
| --- | --- | --- |
| vec | `VectorAligned` | The vector to check. |
| tolerance? | `number` | The tolerance for each component. The default is 0.0001. |
