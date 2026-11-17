> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Matrix 4x4


## VMatrix — cdata


A 4x4 matrix of floats stored row by row. The projection matrix and the view projection matrix
of the view setup use this type. The first three rows have the same layout as a `matrix3x4_t`.

Read or write elements with `vm.m[row][col]`. Indices start at zero.

```cpp lines=false
typedef struct VMatrix {
    float m[4][4];
} VMatrix;
```

The `==` and `~=` operators compare every element exactly. `tostring` returns all sixteen
elements.

The `*` operator with a `Vector` on the right works in the same way as `VMul4x3`. With a
`VPlane` on the right, it works in the same way as `TransformPlane`. With a matrix on the right,
it works in the same way as `MatrixMul`. The `+`, `-` and unary `-` operators work on each
element.


  

### `VMatrix.m`

The elements, stored as 4 rows of 4 numbers. Indices start at zero.


  

### `VMatrix * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VMatrix` |  |


  

### `VMatrix * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `VMatrix * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VPlane` |  |


  

### `VMatrix + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VMatrix` |  |


  

### `VMatrix - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VMatrix` |  |


  

<a id="vmatrix"></a>
### `-VMatrix`


<a id="vmatrix-1"></a>

## VMatrix  — ctype · callable


The constructor without arguments creates an identity matrix. A `matrix3x4_t` is copied into
the first three rows, and the last row is set to `(0, 0, 0, 1)`. Any other argument type throws
an error.


  

<a id="vmatrix"></a>
### `VMatrix()`

```lua
VMatrix(): VMatrix
```

Creates an identity matrix.


  

### `VMatrix(m00, m01, m02, m03, m10, m11, m12, m13, m20, m21, m22, m23, m30, m31, m32, m33)`

```lua
VMatrix(m00: number, m01: number, m02: number, m03: number, m10: number, m11: number, m12: number, m13: number, m20: number, m21: number, m22: number, m23: number, m30: number, m31: number, m32: number, m33: number): VMatrix
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
| m30 | `number` |  |
| m31 | `number` |  |
| m32 | `number` |  |
| m33 | `number` |  |


  

### `VMatrix(forward, left, up)`

```lua
VMatrix(forward: Vector, left: Vector, up: Vector): VMatrix
```

Sets the first three columns to the axes. The translation is zero.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `VMatrix(matrix)`

```lua
VMatrix(matrix: matrix3x4_t|matrix3x4a_t): VMatrix
```


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `VMatrix(self)`

```lua
VMatrix(self: VMatrix): VMatrix
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `VMatrix` |  |


  

### `VMatrix.Init`

```lua
VMatrix.Init(vm: VMatrix, m00: number, m01: number, m02: number, m03: number, m10: number, m11: number, m12: number, m13: number, m20: number, m21: number, m22: number, m23: number, m30: number, m31: number, m32: number, m33: number)
```

Sets all 16 elements in place. Pass the elements row by row.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
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
| m30 | `number` |  |
| m31 | `number` |  |
| m32 | `number` |  |
| m33 | `number` |  |


  

### `VMatrix.Init`

```lua
VMatrix.Init(vm: VMatrix, matrix: matrix3x4_t|matrix3x4a_t)
```

Sets the matrix in place from a 3x4 matrix. The first three rows are copied, and the last row is set to `(0, 0, 0, 1)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| matrix | `matrix3x4_t\|matrix3x4a_t` | The matrix to copy from. |


  

### `VMatrix.InitFLU`

```lua
VMatrix.InitFLU(vm: VMatrix, forward: Vector, left: Vector, up: Vector, origin: Vector)
```

Sets the matrix in place from the forward, left and up axes and an origin. The last row is set to `(0, 0, 0, 1)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| forward | `Vector` | The first column, which is the X axis. |
| left | `Vector` | The second column, which is the Y axis. |
| up | `Vector` | The third column, which is the Z axis. |
| origin | `Vector` | The fourth column, which is the translation. |


  

### `VMatrix.Identity`

```lua
VMatrix.Identity(vm: VMatrix)
```

Sets the matrix to the identity matrix in place.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |


  

### `VMatrix.Copy`

```lua
VMatrix.Copy(src: VMatrix, dst: VMatrix)
```

Copies all 16 elements of `src` into `dst`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `VMatrix` | The matrix to copy from. |
| dst | `VMatrix` | The matrix to copy into. |


  

### `VMatrix.SetupMatrixOrgAngles`

```lua
VMatrix.SetupMatrixOrgAngles(vm: VMatrix, origin: Vector, angles: QAngle)
```

Sets the matrix in place to a rotation from `angles` and a translation from `origin`. The last row is set to `(0, 0, 0, 1)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| origin | `Vector` | The translation. |
| angles | `QAngle` | The rotation. |


  

### `VMatrix.GetForward`

```lua
VMatrix.GetForward(vm: VMatrix): Vector
```

Returns the first column of the first three rows, which is the forward axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetLeft`

```lua
VMatrix.GetLeft(vm: VMatrix): Vector
```

Returns the second column of the first three rows, which is the left axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetUp`

```lua
VMatrix.GetUp(vm: VMatrix): Vector
```

Returns the third column of the first three rows, which is the up axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetTranslation`

```lua
VMatrix.GetTranslation(vm: VMatrix): Vector
```

Returns the fourth column of the first three rows, which is the translation.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetOrigin`

```lua
VMatrix.GetOrigin(vm: VMatrix): Vector
```

Returns the translation. This is the same function as `GetTranslation`, with the name that `matrix3x4_t` uses.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetBasisVectors`

```lua
VMatrix.GetBasisVectors(vm: VMatrix): Vector, Vector, Vector
```

Returns the forward, left and up axes, which are the first three columns of the first three rows.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `VMatrix.GetScale`

```lua
VMatrix.GetScale(vm: VMatrix): Vector
```

Returns the lengths of the forward, left and up axes in `x`, `y` and `z`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.SetForward`

```lua
VMatrix.SetForward(vm: VMatrix, forward: Vector)
```

Sets the first column of the first three rows, which is the forward axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| forward | `Vector` | The new values of the column. |


  

### `VMatrix.SetLeft`

```lua
VMatrix.SetLeft(vm: VMatrix, left: Vector)
```

Sets the second column of the first three rows, which is the left axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| left | `Vector` | The new values of the column. |


  

### `VMatrix.SetUp`

```lua
VMatrix.SetUp(vm: VMatrix, up: Vector)
```

Sets the third column of the first three rows, which is the up axis.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| up | `Vector` | The new values of the column. |


  

### `VMatrix.SetBasisVectors`

```lua
VMatrix.SetBasisVectors(vm: VMatrix, forward: Vector, left: Vector, up: Vector)
```

Sets the first three columns of the first three rows to the forward, left and up axes.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| forward | `Vector` | The X axis. |
| left | `Vector` | The Y axis. |
| up | `Vector` | The Z axis. |


  

### `VMatrix.SetTranslation`

```lua
VMatrix.SetTranslation(vm: VMatrix, translation: Vector)
```

Sets the fourth column of the first three rows, which is the translation.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| translation | `Vector` | The new translation. |


  

### `VMatrix.PreTranslate`

```lua
VMatrix.PreTranslate(vm: VMatrix, translation: Vector)
```

Applies a translation in the input space of the matrix. The translation column is set to `vm:VMul4x3(translation)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| translation | `Vector` | The offset in the input space of the matrix. |


  

### `VMatrix.PostTranslate`

```lua
VMatrix.PostTranslate(vm: VMatrix, translation: Vector)
```

Applies a translation in the output space of the matrix. The offset is added to the translation column.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| translation | `Vector` | The offset in the output space of the matrix. |


  

### `VMatrix.Scale`

```lua
VMatrix.Scale(vm: VMatrix, scale: Vector): VMatrix
```

Returns a new matrix with the first three columns scaled. The first column of every row is multiplied by `scale.x`, the second column by `scale.y` and the third column by `scale.z`. The first three elements of the fourth column do not change.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |
| scale | `Vector` | The scale for the first three columns. |


    
This function is meant for affine matrices. The bottom right element of the result is always
set to 1.


  

  

### `VMatrix.ScaleUpper3x3Matrix`

```lua
VMatrix.ScaleUpper3x3Matrix(vm: VMatrix, scale: number)
```

Multiplies the first three columns of the first three rows by a number in place.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| scale | `number` | The number to multiply by. |


  

### `VMatrix.NormalizeBasisVectors`

```lua
VMatrix.NormalizeBasisVectors(vm: VMatrix): VMatrix
```

Returns a copy in which the forward, left and up axes have a length of 1. An axis with a length of zero does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.As3x4`

```lua
VMatrix.As3x4(vm: VMatrix): matrix3x4_t
```

Returns a reference to the first three rows as a `matrix3x4_t`. Changes to the returned value change the original matrix. Keep the original matrix alive while you use the reference. Use `Set3x4` to get a separate copy.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to view. |


  

### `VMatrix.CopyFrom3x4`

```lua
VMatrix.CopyFrom3x4(vm: VMatrix, matrix: matrix3x4_t|matrix3x4a_t)
```

Copies a 3x4 matrix into the first three rows in place. The last row is set to `(0, 0, 0, 1)`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to change. |
| matrix | `matrix3x4_t\|matrix3x4a_t` | The matrix to copy from. |


  

### `VMatrix.Set3x4`

```lua
VMatrix.Set3x4(vm: VMatrix): matrix3x4_t
```

Copies the first three rows into a new `matrix3x4_t` and returns it.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.IsRotationMatrix`

```lua
VMatrix.IsRotationMatrix(vm: VMatrix): boolean
```

Returns true if the first three elements of each of the first three rows form vectors with a length of 1 that are at right angles to each other. The allowed difference is 0.01.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to check. |


  

### `VMatrix.IsIdentity`

```lua
VMatrix.IsIdentity(vm: VMatrix): boolean
```

Returns true if every element is exactly equal to the same element of the identity matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to check. |


  

### `VMatrix.IsValid`

```lua
VMatrix.IsValid(vm: VMatrix): boolean
```

Returns true if no element is NaN or infinite.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to check. |


  

### `VMatrix.V3Mul`

```lua
VMatrix.V3Mul(vm: VMatrix, v: Vector): Vector
```

Multiplies a point by the full 4x4 matrix, with the `w` component of the point set to 1. Then the result is divided by its `w` component. This is the perspective divide.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The point. |


  

### `VMatrix.V4Mul`

```lua
VMatrix.V4Mul(vm: VMatrix, v: Vector4D): Vector4D
```

Multiplies a vector with four components by the full 4x4 matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector4D` | The vector to transform. |


  

### `VMatrix.ApplyRotation`

```lua
VMatrix.ApplyRotation(vm: VMatrix, v: Vector): Vector
```

Multiplies a direction by the 3x3 rotation part. The translation is not added. This is the same function as `VMul3x3`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The direction to rotate. |


  

### `VMatrix.VMul3x3`

```lua
VMatrix.VMul3x3(vm: VMatrix, v: Vector): Vector
```

Multiplies a direction by the 3x3 rotation part. The translation is not added.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The direction to rotate. |


  

### `VMatrix.VMul3x3Transpose`

```lua
VMatrix.VMul3x3Transpose(vm: VMatrix, v: Vector): Vector
```

Multiplies a direction by the transposed 3x3 rotation part. For a pure rotation matrix, this is the inverse rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The direction to rotate back. |


  

### `VMatrix.VMul4x3`

```lua
VMatrix.VMul4x3(vm: VMatrix, v: Vector): Vector
```

Multiplies a point by the first three rows, and adds the translation. The last row is not used. This is the same as the `*` operator with a `Vector`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The point to transform. |


  

### `VMatrix.VMul4x3Transpose`

```lua
VMatrix.VMul4x3Transpose(vm: VMatrix, v: Vector): Vector
```

Applies the inverse of a matrix that contains only a rotation and a translation. The translation is subtracted, and then the point is multiplied by the transposed 3x3 rotation part.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| v | `Vector` | The point to transform back. |


  

### `VMatrix.MatrixMul`

```lua
VMatrix.MatrixMul(vm: VMatrix, other: VMatrix): VMatrix
```

Returns the product `vm * other`. When the result is applied to a point, `other` is applied first. This is the same as the `*` operator with a matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The left operand. |
| other | `VMatrix` | The right operand, which is applied first. |


  

### `VMatrix.TransformPlane`

```lua
VMatrix.TransformPlane(vm: VMatrix, plane: VPlane): VPlane
```

Transforms a plane by the rotation and the translation. This is the same as the `*` operator with a `VPlane`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to apply. |
| plane | `VPlane` | The plane to transform. |


  

### `VMatrix.InverseGeneral`

```lua
VMatrix.InverseGeneral(vm: VMatrix): boolean, VMatrix
```

Returns the inverse of any matrix. The first return value is true on success.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to invert. |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| inverse | `VMatrix` |  |


    
If the matrix cannot be inverted, or is too close to a matrix that cannot be inverted, the
function returns false and an identity matrix. This happens when no pivot element larger than
`1e-6` can be found.


  

  

### `VMatrix.InverseTR`

```lua
VMatrix.InverseTR(vm: VMatrix): VMatrix
```

Returns the inverse of a matrix that contains only a rotation and a translation. This is faster than `InverseGeneral`. The result is wrong if the matrix contains scale or projection.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to invert. |


  

### `VMatrix.Transpose`

```lua
VMatrix.Transpose(vm: VMatrix): VMatrix
```

Returns the transposed matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.Transpose3x3`

```lua
VMatrix.Transpose3x3(vm: VMatrix): VMatrix
```

Returns a copy with only the 3x3 rotation part transposed. The other elements do not change.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` | The matrix to read. |


  

### `VMatrix.GetIdentityMatrix`

```lua
VMatrix.GetIdentityMatrix(): VMatrix
```

Returns a new identity matrix. Each call returns a new copy.
