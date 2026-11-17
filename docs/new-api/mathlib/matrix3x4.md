> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Matrix 3x4


## matrix3x4\_t — cdata


A 3x4 affine matrix stored row by row. The first three columns hold the rotation. They are the
forward, left and up axes. The fourth column holds the origin.

`matrix3x4a_t` is the form aligned to 16 bytes, with the same layout and the same methods. Bone
and attachment transforms use that form.

Read or write elements with `m.m_flMatVal[row][col]`. Indices start at zero. Call
`matrix3x4_t()` or `matrix3x4a_t()` to create a new identity matrix.

```cpp lines=false
typedef struct matrix3x4_t {
    float m_flMatVal[3][4];
} matrix3x4_t;
```

The `==` and `~=` operators compare every element exactly. `tostring` returns all twelve
elements.

The `*` operator with a matrix on the right returns the product, which applies the right matrix
first. With a `Vector` on the right, it transforms the vector as a point, in the same way as
`TransformVector`. The `+` and `-` operators work on each element. The results of the operators
have the type of the left operand.


  

### `matrix3x4_t.m_flMatVal`

The elements, stored as 3 rows of 4 numbers. Indices start at zero.


  

### `matrix3x4_t * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `matrix3x4_t * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `matrix3x4_t + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `matrix3x4_t - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


<a id="matrix3x4_t-1"></a>

## matrix3x4_t  — ctype · callable


The constructor without arguments creates an identity matrix. If a position is not given, the
origin is set to zero. Any other argument type throws an error.


  

<a id="matrix3x4_t"></a>
### `matrix3x4_t()`

```lua
matrix3x4_t(): matrix3x4_t
```

Creates an identity matrix.


  

### `matrix3x4_t(m00, m01, m02, m03, m10, m11, m12, m13, m20, m21, m22, m23)`

```lua
matrix3x4_t(m00: number, m01: number, m02: number, m03: number, m10: number, m11: number, m12: number, m13: number, m20: number, m21: number, m22: number, m23: number): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| m00 | `number` |  |
| m01 | `number` |  |
| m02 | `number` |  |
| m03 | `number` |  |
| m10 | `number` |  |
| m11 | `number` |  |
| m12 | `number` |  |
| m13 | `number` |  |
| m20 | `number` |  |
| m21 | `number` |  |
| m22 | `number` |  |
| m23 | `number` |  |


  

### `matrix3x4_t(x_axis, y_axis, z_axis, origin)`

```lua
matrix3x4_t(x_axis: Vector, y_axis: Vector, z_axis: Vector, origin: Vector): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| x_axis | `Vector` |  |
| y_axis | `Vector` |  |
| z_axis | `Vector` |  |
| origin | `Vector` |  |


  

### `matrix3x4_t(q, position)`

```lua
matrix3x4_t(q: Quaternion|QuaternionStorage[, position: Vector]): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |
| position? | `Vector` |  |


  

### `matrix3x4_t(angles, position)`

```lua
matrix3x4_t(angles: QAngle[, position: Vector]): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |
| position? | `Vector` |  |


  

### `matrix3x4_t(transform)`

```lua
matrix3x4_t(transform: CTransform): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| transform | `CTransform` |  |


  

### `matrix3x4_t(m)`

```lua
matrix3x4_t(m: matrix3x4_t|matrix3x4a_t): matrix3x4_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `matrix3x4_t.Copy`

```lua
matrix3x4_t.Copy(src: matrix3x4_t|matrix3x4a_t, dst: matrix3x4_t|matrix3x4a_t)
```

Copies every element of `src` into `dst`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `matrix3x4_t\|matrix3x4a_t` | The matrix to copy from. |
| dst | `matrix3x4_t\|matrix3x4a_t` | The matrix to copy into. |


  

### `matrix3x4_t.Init`

```lua
matrix3x4_t.Init(m: matrix3x4_t|matrix3x4a_t, m00: number, m01: number, m02: number, m03: number, m10: number, m11: number, m12: number, m13: number, m20: number, m21: number, m22: number, m23: number)
```

Sets all twelve elements in place. Pass the elements row by row.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| m00 | `number` |  |
| m01 | `number` |  |
| m02 | `number` |  |
| m03 | `number` |  |
| m10 | `number` |  |
| m11 | `number` |  |
| m12 | `number` |  |
| m13 | `number` |  |
| m20 | `number` |  |
| m21 | `number` |  |
| m22 | `number` |  |
| m23 | `number` |  |


  

### `matrix3x4_t.InitXYZ`

```lua
matrix3x4_t.InitXYZ(m: matrix3x4_t|matrix3x4a_t, x_axis: Vector, y_axis: Vector, z_axis: Vector, origin: Vector)
```

Sets the matrix in place from three axis columns and an origin column.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| x_axis | `Vector` | The first column. |
| y_axis | `Vector` | The second column. |
| z_axis | `Vector` | The third column. |
| origin | `Vector` | The fourth column, which is the origin. |


  

### `matrix3x4_t.InitFLU`

```lua
matrix3x4_t.InitFLU(m: matrix3x4_t|matrix3x4a_t, forward: Vector, left: Vector, up: Vector, origin: Vector)
```

Sets the matrix in place from the forward, left and up axes and an origin. This is the same as `InitXYZ`, because the forward, left and up axes are the X, Y and Z axes.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| forward | `Vector` | The forward axis. |
| left | `Vector` | The left axis. |
| up | `Vector` | The up axis. |
| origin | `Vector` | The fourth column, which is the origin. |


  

### `matrix3x4_t.InitFromQAngles`

```lua
matrix3x4_t.InitFromQAngles(m: matrix3x4_t|matrix3x4a_t, angles: QAngle[, position: Vector])
```

Sets the rotation in place from a `QAngle` and sets the origin to `position`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| angles | `QAngle` | The rotation. |
| position? | `Vector` | The origin. The default is a zero vector. |


  

### `matrix3x4_t.InitFromRadianEuler`

```lua
matrix3x4_t.InitFromRadianEuler(m: matrix3x4_t|matrix3x4a_t, angles: RadianEuler[, position: Vector])
```

Sets the rotation in place from a `RadianEuler` and sets the origin to `position`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| angles | `RadianEuler` | The rotation in radians. `x` is the roll, `y` is the pitch and `z` is the yaw. |
| position? | `Vector` | The origin. The default is a zero vector. |


  

### `matrix3x4_t.InitFromQuaternion`

```lua
matrix3x4_t.InitFromQuaternion(m: matrix3x4_t|matrix3x4a_t, q: Quaternion|QuaternionStorage[, position: Vector])
```

Sets the rotation in place from a quaternion and sets the origin to `position`. The quaternion must have a length of 1 to give a pure rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| q | `Quaternion\|QuaternionStorage` | The rotation. |
| position? | `Vector` | The origin. The default is a zero vector. |


  

### `matrix3x4_t.InitFromCTransform`

```lua
matrix3x4_t.InitFromCTransform(m: matrix3x4_t|matrix3x4a_t, transform: CTransform)
```

Sets the matrix in place from a transform. The rotation part is multiplied by the uniform scale of the transform, and the origin is set to the position of the transform.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| transform | `CTransform` | The transform to read. |


  

### `matrix3x4_t.InitFromDiagonal`

```lua
matrix3x4_t.InitFromDiagonal(m: matrix3x4_t|matrix3x4a_t, diagonal: Vector)
```

Sets the matrix in place to a scale matrix. The diagonal elements are set to the components of `diagonal`, and every other element is set to zero.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| diagonal | `Vector` | The scale on each axis. |


  

### `matrix3x4_t.SetToZero`

```lua
matrix3x4_t.SetToZero(m: matrix3x4_t|matrix3x4a_t)
```

Sets every element to zero.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |


  

### `matrix3x4_t.SetToIdentity`

```lua
matrix3x4_t.SetToIdentity(m: matrix3x4_t|matrix3x4a_t)
```

Sets the matrix to the identity matrix with a zero origin.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |


  

### `matrix3x4_t.Invalidate`

```lua
matrix3x4_t.Invalidate(m: matrix3x4_t|matrix3x4a_t)
```

Sets every element to NaN. After this call, `IsValid` returns false.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |


  

### `matrix3x4_t.IsValid`

```lua
matrix3x4_t.IsValid(m: matrix3x4_t|matrix3x4a_t): boolean
```

Returns true if no element is NaN or infinite.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to check. |


  

### `matrix3x4_t.GetOrigin`

```lua
matrix3x4_t.GetOrigin(m: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the fourth column, which is the origin.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.SetOrigin`

```lua
matrix3x4_t.SetOrigin(m: matrix3x4_t|matrix3x4a_t, origin: Vector)
```

Sets the fourth column, which is the origin.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| origin | `Vector` | The new origin. |


  

### `matrix3x4_t.GetColumn`

```lua
matrix3x4_t.GetColumn(m: matrix3x4_t|matrix3x4a_t, column: integer): Vector
```

Returns a column by its index. Use the values of `MatrixAxisType_t` for the index.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |
| column | `integer` | The column index from 0 to 3. See `MatrixAxisType_t`. |


  

### `matrix3x4_t.SetColumn`

```lua
matrix3x4_t.SetColumn(m: matrix3x4_t|matrix3x4a_t, vec: Vector, column: integer)
```

Sets a column by its index. Use the values of `MatrixAxisType_t` for the index. The vector comes before the index in the argument list.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| vec | `Vector` | The new values of the column. |
| column | `integer` | The column index from 0 to 3. See `MatrixAxisType_t`. |


  

### `matrix3x4_t.GetForward`

```lua
matrix3x4_t.GetForward(m: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the first column, which is the forward axis.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.GetLeft`

```lua
matrix3x4_t.GetLeft(m: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the second column, which is the left axis.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.GetUp`

```lua
matrix3x4_t.GetUp(m: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the third column, which is the up axis.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.GetRow`

```lua
matrix3x4_t.GetRow(m: matrix3x4_t|matrix3x4a_t, row: integer): Vector
```

Returns the first three elements of a row. The fourth element of the row is left out.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |
| row | `integer` | The row index from 0 to 2. |


  

### `matrix3x4_t.SetRow`

```lua
matrix3x4_t.SetRow(m: matrix3x4_t|matrix3x4a_t, row: integer, vec: Vector)
```

Sets the first three elements of a row. The fourth element of the row does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| row | `integer` | The row index from 0 to 2. |
| vec | `Vector` | The new values of the row. |


  

### `matrix3x4_t.GetBasisVectorsFLU`

```lua
matrix3x4_t.GetBasisVectorsFLU(m: matrix3x4_t|matrix3x4a_t): Vector, Vector, Vector
```

Returns the forward, left and up axes, which are the first three columns.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `matrix3x4_t.ToQuaternion`

```lua
matrix3x4_t.ToQuaternion(m: matrix3x4_t|matrix3x4a_t): Quaternion
```

Converts the rotation part to a `Quaternion`. The first three columns must have a length of 1 and be at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.ToQAngle`

```lua
matrix3x4_t.ToQAngle(m: matrix3x4_t|matrix3x4a_t): QAngle
```

Converts the rotation part to a `QAngle` in degrees. If the forward axis points almost straight up or down, the roll is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.ToCTransform`

```lua
matrix3x4_t.ToCTransform(m: matrix3x4_t|matrix3x4a_t): CTransform
```

Converts the matrix to a transform. The first three columns are normalized before the rotation is computed. The scale of the transform is the length of the longest of these columns.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.ScaleUpper3x3Matrix`

```lua
matrix3x4_t.ScaleUpper3x3Matrix(m: matrix3x4_t|matrix3x4a_t, scale: number)
```

Multiplies the first three columns by a number in place. The origin does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to change. |
| scale | `number` | The number to multiply by. |


  

### `matrix3x4_t.TransformVector`

```lua
matrix3x4_t.TransformVector(m: matrix3x4_t|matrix3x4a_t, vec: Vector): Vector
```

Transforms a point. The point is rotated by the first three columns, and then the origin is added.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| vec | `Vector` | The point in local space. |


  

### `matrix3x4_t.RotateVector`

```lua
matrix3x4_t.RotateVector(m: matrix3x4_t|matrix3x4a_t, vec: Vector): Vector
```

Rotates a direction by the first three columns. The origin is not added.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| vec | `Vector` | The direction in local space. |


  

### `matrix3x4_t.TransformVectorByInverse`

```lua
matrix3x4_t.TransformVectorByInverse(m: matrix3x4_t|matrix3x4a_t, vec: Vector): Vector
```

Applies the inverse transform to a point. The origin is subtracted, and then the point is rotated by the transposed rotation part. The result is correct only if the first three columns have a length of 1 and are at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| vec | `Vector` | The point in world space. |


  

### `matrix3x4_t.RotateVectorByInverse`

```lua
matrix3x4_t.RotateVectorByInverse(m: matrix3x4_t|matrix3x4a_t, vec: Vector): Vector
```

Rotates a direction by the transposed rotation part, which is the inverse rotation. The result is correct only if the first three columns have a length of 1 and are at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| vec | `Vector` | The direction in world space. |


  

### `matrix3x4_t.RotateExtents`

```lua
matrix3x4_t.RotateExtents(m: matrix3x4_t|matrix3x4a_t, extents: Vector): Vector
```

Rotates a box that is centered on the origin, given by its half size on each axis. Returns the half size of the smallest axis aligned box that contains the rotated box. Every component of the result is zero or greater.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| extents | `Vector` | The half size of the box on each axis. |


  

### `matrix3x4_t.TransformAABB`

```lua
matrix3x4_t.TransformAABB(m: matrix3x4_t|matrix3x4a_t, mins: Vector, maxs: Vector): Vector, Vector
```

Transforms an axis aligned box by the rotation and the origin. Returns the smallest axis aligned box that contains the transformed box.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `matrix3x4_t.TransformAABB`

```lua
matrix3x4_t.TransformAABB(m: matrix3x4_t|matrix3x4a_t, bounds: AABB_t): AABB_t
```

Transforms a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `matrix3x4_t.TransformAABBByInverse`

```lua
matrix3x4_t.TransformAABBByInverse(m: matrix3x4_t|matrix3x4a_t, mins: Vector, maxs: Vector): Vector, Vector
```

Transforms an axis aligned box by the inverse transform. Returns the smallest axis aligned box that contains the transformed box. The result is correct only if the first three columns have a length of 1 and are at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `matrix3x4_t.TransformAABBByInverse`

```lua
matrix3x4_t.TransformAABBByInverse(m: matrix3x4_t|matrix3x4a_t, bounds: AABB_t): AABB_t
```

Transforms a box given as an `AABB_t` by the inverse transform and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `matrix3x4_t.RotateAABB`

```lua
matrix3x4_t.RotateAABB(m: matrix3x4_t|matrix3x4a_t, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box by the rotation part. The origin is not added. Returns the smallest axis aligned box that contains the rotated box.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `matrix3x4_t.RotateAABB`

```lua
matrix3x4_t.RotateAABB(m: matrix3x4_t|matrix3x4a_t, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `matrix3x4_t.RotateAABBByInverse`

```lua
matrix3x4_t.RotateAABBByInverse(m: matrix3x4_t|matrix3x4a_t, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box by the transposed rotation part, which is the inverse rotation. The origin is not used. Returns the smallest axis aligned box that contains the rotated box.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `matrix3x4_t.RotateAABBByInverse`

```lua
matrix3x4_t.RotateAABBByInverse(m: matrix3x4_t|matrix3x4a_t, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` by the inverse rotation and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `matrix3x4_t.GetOrthogonalityError`

```lua
matrix3x4_t.GetOrthogonalityError(m: matrix3x4_t|matrix3x4a_t): number
```

Returns the sum of the absolute dot products between each pair of the first three columns. The result is 0 if the columns are at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.GetDeterminant`

```lua
matrix3x4_t.GetDeterminant(m: matrix3x4_t|matrix3x4a_t): number
```

Returns the determinant of the 3x3 rotation part.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.GetTrace`

```lua
matrix3x4_t.GetTrace(m: matrix3x4_t|matrix3x4a_t): number
```

Returns the trace of the 3x3 rotation part, which is the sum of its diagonal elements.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `matrix3x4_t.Transposed`

```lua
matrix3x4_t.Transposed(m: T): T
```

Returns a new matrix with the 3x3 rotation part transposed and the origin set to zero. The result has the same type as `m`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `T` | The matrix to read. |


  

### `matrix3x4_t.InverseTR`

```lua
matrix3x4_t.InverseTR(m: T): T
```

Returns the inverse of a matrix that contains only a rotation and a translation. The rotation part is transposed, and the origin is rotated by the transposed part and negated. The result is wrong if the matrix contains scale. The result has the same type as `m`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `T` | The matrix to invert. |


  

### `matrix3x4_t.IsEqualTo`

```lua
matrix3x4_t.IsEqualTo(a: matrix3x4_t|matrix3x4a_t, b: matrix3x4_t|matrix3x4a_t[, tolerance: number]): boolean
```

Returns true if every element of `a` differs from the same element of `b` by at most `tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `matrix3x4_t\|matrix3x4a_t` | The first matrix. |
| b | `matrix3x4_t\|matrix3x4a_t` | The second matrix. |
| tolerance? | `number` | The allowed difference. The default is `1e-5`. |


  

### `matrix3x4_t.TransformPlane`

```lua
matrix3x4_t.TransformPlane(m: matrix3x4_t|matrix3x4a_t, plane: VPlane): VPlane
```

Transforms a plane by the rotation and the origin. This works in the same way as `MatrixTransformPlane` in the engine.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| plane | `VPlane` | The plane to transform. |


  

### `matrix3x4_t.TransformPlaneByInverse`

```lua
matrix3x4_t.TransformPlaneByInverse(m: matrix3x4_t|matrix3x4a_t, plane: VPlane): VPlane
```

Transforms a plane by the inverse of the rotation and the origin. This works in the same way as `MatrixITransformPlane` in the engine.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| plane | `VPlane` | The plane to transform. |


## matrix3x4a\_t — cdata


The form of `matrix3x4_t` that is aligned to 16 bytes. It has the same layout, constructors and
methods.

The `==` and `~=` operators compare every element exactly. `tostring` returns all twelve
elements.


  

### `matrix3x4a_t.m_flMatVal`

The elements, stored as 3 rows of 4 numbers. Indices start at zero.


  

### `matrix3x4a_t * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `matrix3x4a_t * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `matrix3x4a_t + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `matrix3x4a_t - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `matrix3x4_t\|matrix3x4a_t` |  |


<a id="matrix3x4a_t-1"></a>

## matrix3x4a_t  — ctype · callable


  

<a id="matrix3x4a_t"></a>
### `matrix3x4a_t()`

```lua
matrix3x4a_t(): matrix3x4a_t
```

Creates an identity matrix.


  

### `matrix3x4a_t(m00, m01, m02, m03, m10, m11, m12, m13, m20, m21, m22, m23)`

```lua
matrix3x4a_t(m00: number, m01: number, m02: number, m03: number, m10: number, m11: number, m12: number, m13: number, m20: number, m21: number, m22: number, m23: number): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| m00 | `number` |  |
| m01 | `number` |  |
| m02 | `number` |  |
| m03 | `number` |  |
| m10 | `number` |  |
| m11 | `number` |  |
| m12 | `number` |  |
| m13 | `number` |  |
| m20 | `number` |  |
| m21 | `number` |  |
| m22 | `number` |  |
| m23 | `number` |  |


  

### `matrix3x4a_t(x_axis, y_axis, z_axis, origin)`

```lua
matrix3x4a_t(x_axis: Vector, y_axis: Vector, z_axis: Vector, origin: Vector): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| x_axis | `Vector` |  |
| y_axis | `Vector` |  |
| z_axis | `Vector` |  |
| origin | `Vector` |  |


  

### `matrix3x4a_t(q, position)`

```lua
matrix3x4a_t(q: Quaternion|QuaternionStorage[, position: Vector]): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |
| position? | `Vector` |  |


  

### `matrix3x4a_t(angles, position)`

```lua
matrix3x4a_t(angles: QAngle[, position: Vector]): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |
| position? | `Vector` |  |


  

### `matrix3x4a_t(transform)`

```lua
matrix3x4a_t(transform: CTransform): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| transform | `CTransform` |  |


  

### `matrix3x4a_t(m)`

```lua
matrix3x4a_t(m: matrix3x4_t|matrix3x4a_t): matrix3x4a_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |


## MatrixAxisType\_t — enum

Column indices for `GetColumn` and `SetColumn`.


### `MatrixAxisType_t`


| Name | Value | Description |
| --- | --- | --- |
| FORWARD_AXIS | 0 | The forward axis column, which is the X axis |
| LEFT_AXIS | 1 | The left axis column, which is the Y axis |
| UP_AXIS | 2 | The up axis column, which is the Z axis |
| X_AXIS | 0 |  |
| Y_AXIS | 1 |  |
| Z_AXIS | 2 |  |
| ORIGIN | 3 | The origin column |
| PROJECTIVE | 3 |  |
