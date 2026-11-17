> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Quaternion


<a id="quaternion-1"></a>

## Quaternion  — cdata


A quaternion with the imaginary part in `x`, `y` and `z` and the real part in `w`. Use unit
quaternions, which have a length of 1, for rotations.

`Quaternion` is aligned to 16 bytes and is the form used by `CTransform`. `QuaternionStorage`
is the unaligned form with the same layout and the same methods. The constructor of each type
accepts the other type, so you can convert between them.

```cpp lines=false
typedef struct __declspec(align(16)) Quaternion {
    float x, y, z, w;
} Quaternion;
```


  

### `Quaternion.w`

The real part.


  

### `Quaternion.x`

The x component of the imaginary part.


  

### `Quaternion.y`

The y component of the imaginary part.


  

### `Quaternion.z`

The z component of the imaginary part.


  

### `Quaternion + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Quaternion` |  |


  

### `Quaternion - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Quaternion` |  |


  

### `Quaternion * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Quaternion\|QuaternionStorage` |  |


  

### `Quaternion * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `number` |  |


  

### `Quaternion * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `Quaternion * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned` |  |


  

### `Quaternion / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `number` |  |


  

### `-Quaternion`


<a id="quaternion-2"></a>

## Quaternion  — ctype · callable


The constructor without arguments sets every component to zero. Use `qIdentity` or
`Quaternion(0, 0, 0, 1)` for the identity rotation.

When you pass numbers, missing components are set to 0. A `QAngle`, `RadianEuler` or
`DegreeEuler` is converted to the same rotation. Any other argument type throws an error.


  

### `Quaternion()`

```lua
Quaternion(): Quaternion
```

Sets every component to zero.


  

### `Quaternion(x, y, z, w)`

```lua
Quaternion(x: number[, y: number, z: number, w: number]): Quaternion
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |
| w? | `number` |  |


  

### `Quaternion(imaginary, real)`

```lua
Quaternion(imaginary: Vector|VectorAligned, real: number): Quaternion
```


| Parameter | Type | Description |
| --- | --- | --- |
| imaginary | `Vector\|VectorAligned` |  |
| real | `number` |  |


  

### `Quaternion(angles)`

```lua
Quaternion(angles: QAngle): Quaternion
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `Quaternion(angles)`

```lua
Quaternion(angles: RadianEuler|DegreeEuler): Quaternion
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `RadianEuler\|DegreeEuler` |  |


  

### `Quaternion(q)`

```lua
Quaternion(q: Quaternion|QuaternionStorage): Quaternion
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


  

### `Quaternion.qIdentity`

The identity rotation `(0, 0, 0, 1)`. It is read only.


  

### `Quaternion.qZero`

A quaternion with every component set to zero. It is read only.


  

### `Quaternion.FromAxisAngle`

```lua
Quaternion.FromAxisAngle(axis: Vector, degrees: number): Quaternion
```

Creates a quaternion that rotates by the given number of degrees around an axis. The axis must have a length of 1, because it is not normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The rotation axis. |
| degrees | `number` | The rotation angle in degrees. |


  

### `Quaternion.FromQAngle`

```lua
Quaternion.FromQAngle(angles: QAngle): Quaternion
```

Creates a quaternion from a `QAngle`. This is the same as calling the constructor with a `QAngle`.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` | The pitch, yaw and roll in degrees. |


  

### `Quaternion.Unpack`

```lua
Quaternion.Unpack(q: Quaternion): number, number, number, number
```

Returns the `x`, `y`, `z` and `w` components.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |
| w | `number` |  |


  

### `Quaternion.Copy`

```lua
Quaternion.Copy(src: Quaternion, dst: Quaternion)
```

Copies the components of `src` into `dst`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Quaternion` | The quaternion to copy from. |
| dst | `Quaternion` | The quaternion to copy into. |


  

### `Quaternion.Init`

```lua
Quaternion.Init(q: Quaternion[, x: number|Vector|VectorAligned, y: number, z: number, w: number])
```

Sets the components in place. Pass four numbers, or pass a vector for the imaginary part and a number for the real part. When you pass numbers, missing numbers are set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to change. |
| x? | `number\|Vector\|VectorAligned` | The x component, or a vector with the imaginary part. |
| y? | `number` | The y component, or the real part when `x` is a vector. |
| z? | `number` | The z component. |
| w? | `number` | The w component, which is the real part. |


  

### `Quaternion.IsValid`

```lua
Quaternion.IsValid(q: Quaternion): boolean
```

Returns true if none of the four components is NaN or infinite.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to check. |


  

### `Quaternion.Invalidate`

```lua
Quaternion.Invalidate(q: Quaternion)
```

Sets every component to NaN. After this call, `IsValid` returns false.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to change. |


  

### `Quaternion.ImaginaryPart`

```lua
Quaternion.ImaginaryPart(q: Quaternion): Vector
```

Returns the imaginary part `x`, `y` and `z` as a new `Vector`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to read. |


  

### `Quaternion.RealPart`

```lua
Quaternion.RealPart(q: Quaternion): number
```

Returns the real part `w`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to read. |


  

### `Quaternion.Length`

```lua
Quaternion.Length(q: Quaternion): number
```

Returns the length of the quaternion, using all four components.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to measure. |


  

### `Quaternion.LengthSqr`

```lua
Quaternion.LengthSqr(q: Quaternion): number
```

Returns the squared length of the quaternion, using all four components.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to measure. |


  

### `Quaternion.Dot`

```lua
Quaternion.Dot(a: Quaternion, b: Quaternion): number
```

Returns the dot product of the two quaternions, using all four components.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Quaternion` | The first quaternion. |
| b | `Quaternion` | The second quaternion. |


  

### `Quaternion.Normalize`

```lua
Quaternion.Normalize(q: Quaternion): number
```

Scales the quaternion in place so that its length is 1, and returns the length it had before. If the length is zero, the quaternion is set to the identity rotation and the function returns 0.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to normalize. |


  

### `Quaternion.Normalized`

```lua
Quaternion.Normalized(q: Quaternion): Quaternion
```

Returns a copy of the quaternion with a length of 1. If the length is zero, the copy is the identity rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to normalize. |


  

### `Quaternion.IsNormalized`

```lua
Quaternion.IsNormalized(q: Quaternion[, tolerance: number]): boolean
```

Returns true if the length differs from 1 by less than `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to check. |
| tolerance? | `number` | The allowed difference. The default is `1e-6`. |


  

### `Quaternion.Conjugate`

```lua
Quaternion.Conjugate(q: Quaternion): Quaternion
```

Returns the conjugate, which is the quaternion with the imaginary part negated. For a unit quaternion, the conjugate is also the inverse.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to read. |


  

### `Quaternion.Inverse`

```lua
Quaternion.Inverse(q: Quaternion): Quaternion
```

Returns the inverse, which is the conjugate divided by the squared length. This works for a quaternion of any length. If the length is zero, the function returns the identity rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to read. |


  

### `Quaternion.RotateVector`

```lua
Quaternion.RotateVector(q: Quaternion, vec: Vector): Vector
```

Rotates a vector by the quaternion. The quaternion must have a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| vec | `Vector` | The vector to rotate. |


  

### `Quaternion.RotateVector`

```lua
Quaternion.RotateVector(q: Quaternion, vec: VectorAligned): VectorAligned
```

Rotates a `VectorAligned` by the quaternion. The quaternion must have a length of 1. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| vec | `VectorAligned` | The vector to rotate. |


  

### `Quaternion.RotateVectorByInverse`

```lua
Quaternion.RotateVectorByInverse(q: Quaternion, vec: Vector): Vector
```

Rotates a vector by the inverse of the rotation. The quaternion must have a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| vec | `Vector` | The vector to rotate. |


  

### `Quaternion.RotateVectorByInverse`

```lua
Quaternion.RotateVectorByInverse(q: Quaternion, vec: VectorAligned): VectorAligned
```

Rotates a `VectorAligned` by the inverse of the rotation. The quaternion must have a length of 1. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| vec | `VectorAligned` | The vector to rotate. |


  

### `Quaternion.RotateExtents`

```lua
Quaternion.RotateExtents(q: Quaternion, extents: Vector): Vector
```

Rotates a box that is centered on the origin, given by its half size on each axis. Returns the half size of the smallest axis aligned box that contains the rotated box. Every component of the result is zero or greater. The quaternion is normalized before it is used.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| extents | `Vector` | The half size of the box on each axis. |


  

### `Quaternion.RotateExtents`

```lua
Quaternion.RotateExtents(q: Quaternion, extents: VectorAligned): VectorAligned
```

Rotates a box that is centered on the origin, given by its half size on each axis. Returns the half size of the smallest axis aligned box that contains the rotated box. Every component of the result is zero or greater, and the `w` component is 0. The quaternion is normalized before it is used.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| extents | `VectorAligned` | The half size of the box on each axis. |


  

### `Quaternion.RotateAABB`

```lua
Quaternion.RotateAABB(q: Quaternion, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box around the origin. Returns the smallest axis aligned box that contains the rotated box. The quaternion must have a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `Quaternion.RotateAABB`

```lua
Quaternion.RotateAABB(q: Quaternion, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `Quaternion.RotateAABBByInverse`

```lua
Quaternion.RotateAABBByInverse(q: Quaternion, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box around the origin by the inverse of the rotation. Returns the smallest axis aligned box that contains the rotated box.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `Quaternion.RotateAABBByInverse`

```lua
Quaternion.RotateAABBByInverse(q: Quaternion, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` by the inverse of the rotation and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `Quaternion.GetForward`

```lua
Quaternion.GetForward(q: Quaternion): Vector
```

Returns the positive X axis rotated by the quaternion. This is the forward direction.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.GetLeft`

```lua
Quaternion.GetLeft(q: Quaternion): Vector
```

Returns the positive Y axis rotated by the quaternion. This is the left direction.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.GetUp`

```lua
Quaternion.GetUp(q: Quaternion): Vector
```

Returns the positive Z axis rotated by the quaternion. This is the up direction.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.GetAxis`

```lua
Quaternion.GetAxis(q: Quaternion): Vector
```

Returns the rotation axis with a length of 1. If the imaginary part is zero, for example for the identity rotation, the function returns `Vector(0, 0, 1)`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.GetAngleDegrees`

```lua
Quaternion.GetAngleDegrees(q: Quaternion): number
```

Returns the rotation angle around the axis from `GetAxis`, in degrees. The result is greater than -180 and at most 180.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.GetAxisAngle`

```lua
Quaternion.GetAxisAngle(q: Quaternion): Vector, number
```

Returns the rotation axis and the rotation angle in radians. The axis is the same as the result of `GetAxis`. The angle is between 0 and `2 * math.pi`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


| Return | Type | Description |
| --- | --- | --- |
| axis | `Vector` |  |
| radians | `number` |  |


  

### `Quaternion.SetAxisAngle`

```lua
Quaternion.SetAxisAngle(q: Quaternion, axis: Vector, radians: number)
```

Sets the quaternion in place to a rotation by an angle in radians around an axis. The axis must have a length of 1, because it is not normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The quaternion to change. |
| axis | `Vector` | The rotation axis. |
| radians | `number` | The rotation angle in radians. |


  

### `Quaternion.ToMatrix`

```lua
Quaternion.ToMatrix(q: Quaternion[, origin: Vector]): matrix3x4a_t
```

Converts the rotation to an aligned 3x4 matrix. The fourth column of the matrix is set to `origin`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |
| origin? | `Vector` | The value of the fourth column. The default is a zero vector. |


  

### `Quaternion.ToQAngle`

```lua
Quaternion.ToQAngle(q: Quaternion): QAngle
```

Converts the rotation to a `QAngle` with the pitch, yaw and roll in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.ToRadianEuler`

```lua
Quaternion.ToRadianEuler(q: Quaternion): RadianEuler
```

Converts the rotation to a `RadianEuler` in radians. `x` is the roll, `y` is the pitch and `z` is the yaw.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.ToDegreeEuler`

```lua
Quaternion.ToDegreeEuler(q: Quaternion): DegreeEuler
```

Converts the rotation to a `DegreeEuler` in degrees. `x` is the roll, `y` is the pitch and `z` is the yaw.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.ToRotationVector`

```lua
Quaternion.ToRotationVector(q: Quaternion): RotationVector
```

Converts the rotation to a rotation vector, which is the rotation axis multiplied by the rotation angle in degrees. The axis comes from `GetAxis` and the angle comes from `GetAngleDegrees`. This form is also called the exponential map.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.ToQuaternion`

```lua
Quaternion.ToQuaternion(q: Quaternion): Quaternion
```

Returns a copy as an aligned `Quaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


  

### `Quaternion.ToQuaternionStorage`

```lua
Quaternion.ToQuaternionStorage(q: Quaternion): QuaternionStorage
```

Returns a copy as an unaligned `QuaternionStorage`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` | The rotation. |


## QuaternionStorage — cdata


The unaligned form of `Quaternion` with the same layout. Schema fields and `CTransformUnaligned`
use this form.

It has every method of `Quaternion`, and the methods work in the same way. Methods and
operators that return a quaternion return a `QuaternionStorage`, except `ToQuaternion`.
`ToMatrix` returns an unaligned `matrix3x4_t`.


  

### `QuaternionStorage.w`

The real part.


  

### `QuaternionStorage.x`

The x component of the imaginary part.


  

### `QuaternionStorage.y`

The y component of the imaginary part.


  

### `QuaternionStorage.z`

The z component of the imaginary part.


  

### `QuaternionStorage + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QuaternionStorage` |  |


  

### `QuaternionStorage - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QuaternionStorage` |  |


  

### `QuaternionStorage * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Quaternion\|QuaternionStorage` |  |


  

### `QuaternionStorage * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `number` |  |


  

### `QuaternionStorage * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `QuaternionStorage * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned` |  |


  

### `QuaternionStorage / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `number` |  |


  

<a id="quaternionstorage"></a>
### `-QuaternionStorage`


<a id="quaternionstorage-1"></a>

## QuaternionStorage  — ctype · callable


  

<a id="quaternionstorage"></a>
### `QuaternionStorage()`

```lua
QuaternionStorage(): QuaternionStorage
```

Sets every component to zero.


  

### `QuaternionStorage(x, y, z, w)`

```lua
QuaternionStorage(x: number[, y: number, z: number, w: number]): QuaternionStorage
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |
| w? | `number` |  |


  

### `QuaternionStorage(imaginary, real)`

```lua
QuaternionStorage(imaginary: Vector|VectorAligned, real: number): QuaternionStorage
```


| Parameter | Type | Description |
| --- | --- | --- |
| imaginary | `Vector\|VectorAligned` |  |
| real | `number` |  |


  

### `QuaternionStorage(angles)`

```lua
QuaternionStorage(angles: QAngle): QuaternionStorage
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `QuaternionStorage(angles)`

```lua
QuaternionStorage(angles: RadianEuler|DegreeEuler): QuaternionStorage
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `RadianEuler\|DegreeEuler` |  |


  

### `QuaternionStorage(q)`

```lua
QuaternionStorage(q: Quaternion|QuaternionStorage): QuaternionStorage
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


  

### `QuaternionStorage.qIdentity`

The identity rotation `(0, 0, 0, 1)`. It is read only.


  

### `QuaternionStorage.qZero`

A quaternion with every component set to zero. It is read only.
