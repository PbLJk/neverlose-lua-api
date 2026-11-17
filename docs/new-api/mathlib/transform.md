> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Transform


## CTransform — cdata


A position, a rotation stored as a quaternion and a uniform scale, in 32 bytes aligned to 16
bytes. The scale is stored in the `w` component of `m_vPositionWScale`. Use `GetOrigin` and
`GetScale` to read the position and the scale.

Trace results, `CGameSceneNode.m_nodeToWorld` and the fields of `CMsgTransform` messages use
this type.

```cpp lines=false
typedef struct __declspec(align(16)) CTransform {
    VectorAligned m_vPositionWScale;
    Quaternion m_orientation;
} CTransform;
```

The `==` and `~=` operators compare every component exactly. `tostring` returns the position,
the orientation and the scale. Call `CTransform()` to create a new identity transform.

The `*` operator with a transform on the right combines the two transforms. The right transform
is applied first. If the orientation of the right transform is closer to the negated orientation
of the left transform, it is negated before the multiplication. The orientation of the result is
normalized. If its length is zero, it is set to the identity rotation. The scale of the result is
the product of the two scales. With a vector on the right, the `*` operator transforms the vector
as a point, in the same way as `TransformVector`.


  

### `CTransform.m_orientation`

The rotation.


  

### `CTransform.m_vPositionWScale`

The position in `x`, `y` and `z`, and the uniform scale in `w`.


  

### `CTransform * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `CTransform` |  |


  

### `CTransform * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector` |  |


  

### `CTransform * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `VectorAligned` |  |


<a id="ctransform-1"></a>

## CTransform  — ctype · callable


The constructor without arguments creates an identity transform. When you pass a position, a
`QAngle` orientation is converted to a quaternion, and the scale is 1 if it is not given. When
you pass a matrix, the scale is the length of the longest of its first three columns. Any other
argument type throws an error.


  

<a id="ctransform"></a>
### `CTransform()`

```lua
CTransform(): CTransform
```

Creates an identity transform.


  

### `CTransform(position, orientation, scale)`

```lua
CTransform(position: Vector|VectorAligned, orientation: Quaternion|QuaternionStorage|QAngle[, scale: number]): CTransform
```


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector\|VectorAligned` |  |
| orientation | `Quaternion\|QuaternionStorage\|QAngle` |  |
| scale? | `number` |  |


  

### `CTransform(m)`

```lua
CTransform(m: matrix3x4_t|matrix3x4a_t): CTransform
```


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `CTransform(transform)`

```lua
CTransform(transform: CTransform|CTransformUnaligned): CTransform
```


| Parameter | Type | Description |
| --- | --- | --- |
| transform | `CTransform\|CTransformUnaligned` |  |


  

### `CTransform.Copy`

```lua
CTransform.Copy(src: CTransform, dst: CTransform)
```

Copies the position, the scale and the orientation of `src` into `dst`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `CTransform` | The transform to copy from. |
| dst | `CTransform` | The transform to copy into. |


  

### `CTransform.IsValid`

```lua
CTransform.IsValid(t: CTransform): boolean
```

Returns true if no component of the position or the orientation is NaN or infinite. The scale is not checked. Call `GetScale` if you need to check the scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to check. |


  

### `CTransform.IsEqualTo`

```lua
CTransform.IsEqualTo(a: CTransform, b: CTransform[, tolerance: number, rotation_tolerance: number]): boolean
```

Returns true if the two transforms are equal within the given tolerances.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `CTransform` | The first transform. |
| b | `CTransform` | The second transform. |
| tolerance? | `number` | The allowed difference for the position and the scale. The default is `1e-5`. |
| rotation_tolerance? | `number` | The allowed difference for the orientation. The default is twice `tolerance`. |


    
Each position component may differ by at most `tolerance`. The scale and the orientation
components are compared relative to their size. The scale uses `tolerance` and the orientation
uses `rotation_tolerance`. If both values are smaller than about `3.8e-6`, they always count as
equal. An orientation also matches its negated quaternion, because both give the same rotation.


  

  

### `CTransform.SetToIdentity`

```lua
CTransform.SetToIdentity(t: CTransform)
```

Sets the transform to the identity. The position is zero, the rotation is the identity rotation and the scale is 1.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |


  

### `CTransform.InitFromQAngles`

```lua
CTransform.InitFromQAngles(t: CTransform, angles: QAngle[, position: Vector, scale: number])
```

Sets the transform in place from a `QAngle`, a position and a scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| angles | `QAngle` | The rotation. |
| position? | `Vector` | The position. The default is a zero vector. |
| scale? | `number` | The uniform scale. The default is 1. |


  

### `CTransform.InitFromQuaternion`

```lua
CTransform.InitFromQuaternion(t: CTransform, q: Quaternion|QuaternionStorage[, position: Vector, scale: number])
```

Sets the transform in place from a quaternion, a position and a scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| q | `Quaternion\|QuaternionStorage` | The rotation. |
| position? | `Vector` | The position. The default is a zero vector. |
| scale? | `number` | The uniform scale. The default is 1. |


  

### `CTransform.InitFromMatrix`

```lua
CTransform.InitFromMatrix(t: CTransform, m: matrix3x4_t|matrix3x4a_t)
```

Sets the transform in place from a matrix. The first three columns are normalized before the rotation is computed. The scale is the length of the longest of these columns.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| m | `matrix3x4_t\|matrix3x4a_t` | The matrix to read. |


  

### `CTransform.InitFromRotationAboutAxis`

```lua
CTransform.InitFromRotationAboutAxis(t: CTransform, axis: Vector, degrees: number[, position: Vector, scale: number])
```

Sets the transform in place to a rotation by a number of degrees around an axis, with a position and a scale. The axis must have a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| axis | `Vector` | The rotation axis. |
| degrees | `number` | The rotation angle in degrees. |
| position? | `Vector` | The position. The default is a zero vector. |
| scale? | `number` | The uniform scale. The default is 1. |


  

### `CTransform.InitFLU`

```lua
CTransform.InitFLU(t: CTransform, forward: Vector, left: Vector, up: Vector, origin: Vector)
```

Sets the transform in place from the forward, left and up axes and a position. The scale is set to 1. The axes must have a length of 1 and be at right angles to each other.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| forward | `Vector` | The forward axis. |
| left | `Vector` | The left axis. |
| up | `Vector` | The up axis. |
| origin | `Vector` | The position. |


  

### `CTransform.InitFromForwardVector`

```lua
CTransform.InitFromForwardVector(t: CTransform, forward: Vector, origin: Vector[, scale: number])
```

Sets the transform in place so that its forward axis points along `forward`. The up axis is chosen to be as close as possible to the world up axis `Vector(0, 0, 1)`. If `forward` points straight up, `Vector(-1, 0, 0)` is used in place of the world up axis. If it points straight down, `Vector(1, 0, 0)` is used.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| forward | `Vector` | The forward direction. It does not need to have a length of 1. |
| origin | `Vector` | The position. |
| scale? | `number` | The uniform scale. The default is 1. |


  

### `CTransform.GetOrigin`

```lua
CTransform.GetOrigin(t: CTransform): Vector
```

Returns a copy of the position as a `Vector`. The scale is not included.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.SetOrigin`

```lua
CTransform.SetOrigin(t: CTransform, origin: Vector|VectorAligned)
```

Sets the position. The scale does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| origin | `Vector\|VectorAligned` | The new position. |


  

### `CTransform.ShiftOrigin`

```lua
CTransform.ShiftOrigin(t: CTransform, offset: Vector|VectorAligned)
```

Adds an offset to the position. The scale does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| offset | `Vector\|VectorAligned` | The offset to add. |


  

### `CTransform.GetScale`

```lua
CTransform.GetScale(t: CTransform): number
```

Returns the uniform scale, which is stored in the `w` component of `m_vPositionWScale`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.SetScale`

```lua
CTransform.SetScale(t: CTransform, scale: number)
```

Sets the uniform scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| scale | `number` | The new scale. |


  

### `CTransform.SetPosition`

```lua
CTransform.SetPosition(t: CTransform, position: Vector|VectorAligned)
```

Sets the position. The scale does not change. This is the same function as `SetOrigin`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| position | `Vector\|VectorAligned` | The new position. |


  

### `CTransform.SetPositionAndScale`

```lua
CTransform.SetPositionAndScale(t: CTransform, position: Vector|VectorAligned[, scale: number])
```

Sets the position and the scale together. If you pass only a `VectorAligned`, its `w` component is used as the scale. If you pass only a `Vector`, an error is thrown.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| position | `Vector\|VectorAligned` | The new position. |
| scale? | `number` | The new scale. It is required unless `position` is a `VectorAligned`. |


  

### `CTransform.GetPositionAndScale`

```lua
CTransform.GetPositionAndScale(t: CTransform): VectorAligned
```

Returns a reference to `m_vPositionWScale`, which holds the position and the scale. Changes to the returned value change this transform. Keep the transform alive while you use the reference.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.GetOrientation`

```lua
CTransform.GetOrientation(t: CTransform): Quaternion
```

Returns a reference to the orientation. Changes to the returned value change this transform. Keep the transform alive while you use the reference.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.SetOrientation`

```lua
CTransform.SetOrientation(t: CTransform, q: Quaternion|QuaternionStorage)
```

Sets the orientation.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| q | `Quaternion\|QuaternionStorage` | The new rotation. |


  

### `CTransform.SetAngles`

```lua
CTransform.SetAngles(t: CTransform, angles: QAngle)
```

Sets the orientation from a `QAngle`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to change. |
| angles | `QAngle` | The new rotation. |


  

### `CTransform.ToQuaternion`

```lua
CTransform.ToQuaternion(t: CTransform): Quaternion
```

Returns a copy of the orientation as a `Quaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.ToQAngle`

```lua
CTransform.ToQAngle(t: CTransform): QAngle
```

Returns the orientation as a `QAngle` in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.ToMatrix`

```lua
CTransform.ToMatrix(t: CTransform): matrix3x4_t
```

Converts the transform to a matrix. The rotation part is multiplied by the scale, and the fourth column is the position.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.Unscaled`

```lua
CTransform.Unscaled(t: CTransform): CTransform
```

Returns a copy of the transform with the scale set to 1.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.GetForward`

```lua
CTransform.GetForward(t: CTransform): Vector
```

Returns the positive X axis rotated by the orientation. This is the forward direction. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.GetLeft`

```lua
CTransform.GetLeft(t: CTransform): Vector
```

Returns the positive Y axis rotated by the orientation. This is the left direction. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.GetUp`

```lua
CTransform.GetUp(t: CTransform): Vector
```

Returns the positive Z axis rotated by the orientation. This is the up direction. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


  

### `CTransform.GetBasisVectorsFLU`

```lua
CTransform.GetBasisVectorsFLU(t: CTransform): Vector, Vector, Vector
```

Returns the forward, left and up axes rotated by the orientation. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to read. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `CTransform.TransformVector`

```lua
CTransform.TransformVector(t: CTransform, vec: Vector): Vector
```

Transforms a point from local space into the parent space of the transform. The point is rotated, multiplied by the scale, and then the position is added.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `Vector` | The point in local space. |


  

### `CTransform.TransformVector`

```lua
CTransform.TransformVector(t: CTransform, vec: VectorAligned): VectorAligned
```

Transforms a `VectorAligned` point from local space into the parent space of the transform. The point is rotated, multiplied by the scale, and then the position is added. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `VectorAligned` | The point in local space. |


  

### `CTransform.RotateVector`

```lua
CTransform.RotateVector(t: CTransform, vec: Vector): Vector
```

Rotates a direction by the orientation. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `Vector` | The direction in local space. |


  

### `CTransform.RotateVector`

```lua
CTransform.RotateVector(t: CTransform, vec: VectorAligned): VectorAligned
```

Rotates a `VectorAligned` direction by the orientation. The scale is not applied. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `VectorAligned` | The direction in local space. |


  

### `CTransform.RotateAndScaleVector`

```lua
CTransform.RotateAndScaleVector(t: CTransform, vec: Vector): Vector
```

Rotates a direction by the orientation and multiplies it by the scale. The position is not added.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `Vector` | The direction in local space. |


  

### `CTransform.RotateAndScaleVector`

```lua
CTransform.RotateAndScaleVector(t: CTransform, vec: VectorAligned): VectorAligned
```

Rotates a `VectorAligned` direction by the orientation and multiplies it by the scale. The position is not added. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `VectorAligned` | The direction in local space. |


  

### `CTransform.TransformVectorByInverse`

```lua
CTransform.TransformVectorByInverse(t: CTransform, vec: Vector): Vector
```

Transforms a point from the parent space into the local space of the transform. The position is subtracted, the result is rotated by the inverse orientation, and then it is divided by the scale. If the scale is zero, the result is a zero vector.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `Vector` | The point in parent space. |


  

### `CTransform.TransformVectorByInverse`

```lua
CTransform.TransformVectorByInverse(t: CTransform, vec: VectorAligned): VectorAligned
```

Transforms a `VectorAligned` point from the parent space into the local space of the transform. The position is subtracted, the result is rotated by the inverse orientation, and then it is divided by the scale. If the scale is zero, the result is a zero vector. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `VectorAligned` | The point in parent space. |


  

### `CTransform.RotateVectorByInverse`

```lua
CTransform.RotateVectorByInverse(t: CTransform, vec: Vector): Vector
```

Rotates a direction by the inverse orientation. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `Vector` | The direction in parent space. |


  

### `CTransform.RotateVectorByInverse`

```lua
CTransform.RotateVectorByInverse(t: CTransform, vec: VectorAligned): VectorAligned
```

Rotates a `VectorAligned` direction by the inverse orientation. The scale is not applied. The `w` component of the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| vec | `VectorAligned` | The direction in parent space. |


  

### `CTransform.RotateExtents`

```lua
CTransform.RotateExtents(t: CTransform, extents: Vector): Vector
```

Rotates a box that is centered on the origin, given by its half size on each axis. Returns the half size of the smallest axis aligned box that contains the rotated box. Every component of the result is zero or greater. The scale is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| extents | `Vector` | The half size of the box on each axis. |


  

### `CTransform.TransformAABB`

```lua
CTransform.TransformAABB(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Transforms an axis aligned box. The box is multiplied by the scale and rotated, and then the position is added. Returns the smallest axis aligned box that contains the result.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.TransformAABB`

```lua
CTransform.TransformAABB(t: CTransform, bounds: AABB_t): AABB_t
```

Transforms a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `CTransform.TransformAABBByInverse`

```lua
CTransform.TransformAABBByInverse(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Transforms an axis aligned box by the inverse transform. The position is subtracted, the box is divided by the scale, and then it is rotated by the inverse orientation. Returns the smallest axis aligned box that contains the result. If the scale is zero, the result is a box of zero size at the origin.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.TransformAABBByInverse`

```lua
CTransform.TransformAABBByInverse(t: CTransform, bounds: AABB_t): AABB_t
```

Transforms a box given as an `AABB_t` by the inverse transform and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `CTransform.RotateAABB`

```lua
CTransform.RotateAABB(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box by the orientation. The scale and the position are not applied. Returns the smallest axis aligned box that contains the rotated box.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.RotateAABB`

```lua
CTransform.RotateAABB(t: CTransform, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `CTransform.RotateAABBByInverse`

```lua
CTransform.RotateAABBByInverse(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Rotates an axis aligned box by the inverse orientation. The scale and the position are not applied. Returns the smallest axis aligned box that contains the rotated box.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.RotateAABBByInverse`

```lua
CTransform.RotateAABBByInverse(t: CTransform, bounds: AABB_t): AABB_t
```

Rotates a box given as an `AABB_t` by the inverse orientation and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to rotate. |


  

### `CTransform.RotateAndScaleAABB`

```lua
CTransform.RotateAndScaleAABB(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Multiplies an axis aligned box by the scale and rotates it by the orientation. The position is not added. Returns the smallest axis aligned box that contains the result.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.RotateAndScaleAABB`

```lua
CTransform.RotateAndScaleAABB(t: CTransform, bounds: AABB_t): AABB_t
```

Scales and rotates a box given as an `AABB_t` and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `CTransform.RotateAndScaleAABBByInverse`

```lua
CTransform.RotateAndScaleAABBByInverse(t: CTransform, mins: Vector, maxs: Vector): Vector, Vector
```

Divides an axis aligned box by the scale and rotates it by the inverse orientation. The position is not used. Returns the smallest axis aligned box that contains the result. If the scale is zero, the result is a box of zero size at the origin.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


| Return | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `CTransform.RotateAndScaleAABBByInverse`

```lua
CTransform.RotateAndScaleAABBByInverse(t: CTransform, bounds: AABB_t): AABB_t
```

Divides a box given as an `AABB_t` by the scale, rotates it by the inverse orientation and returns the result as an `AABB_t`. It works in the same way as the version that takes `mins` and `maxs`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` |  |
| bounds | `AABB_t` | The box to transform. |


  

### `CTransform.Inverse`

```lua
CTransform.Inverse(t: CTransform): CTransform
```

Returns the inverse transform, including the uniform scale. The orientation of the result is the normalized conjugate of the orientation. The scale of the result is 1 divided by the scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to invert. |


    
The result is an exact inverse only if the orientation has a length of 1 and the scale is not
zero. If the scale is zero, the scale of the result is 8388608.


  

  

### `CTransform.InverseTR`

```lua
CTransform.InverseTR(t: CTransform): CTransform
```

The same function as `Inverse`. It also inverts the uniform scale.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransform` | The transform to invert. |


## CTransformUnaligned — cdata


An unaligned transform. It stores the position, the uniform scale and the `QuaternionStorage`
orientation in separate fields.

The `==` and `~=` operators compare every component exactly. `tostring` returns the position,
the orientation and the scale.


  

### `CTransformUnaligned.m_flScale`

The uniform scale.


  

### `CTransformUnaligned.m_orientation`

The rotation.


  

### `CTransformUnaligned.m_vPosition`

The position.


<a id="ctransformunaligned-1"></a>

## CTransformUnaligned  — ctype · callable


  

<a id="ctransformunaligned"></a>
### `CTransformUnaligned()`

```lua
CTransformUnaligned(): CTransformUnaligned
```

Creates an identity transform.


  

### `CTransformUnaligned(position, orientation, scale)`

```lua
CTransformUnaligned(position: Vector|VectorAligned, orientation: Quaternion|QuaternionStorage|QAngle[, scale: number]): CTransformUnaligned
```


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector\|VectorAligned` |  |
| orientation | `Quaternion\|QuaternionStorage\|QAngle` |  |
| scale? | `number` |  |


  

### `CTransformUnaligned(transform)`

```lua
CTransformUnaligned(transform: CTransform|CTransformUnaligned): CTransformUnaligned
```


| Parameter | Type | Description |
| --- | --- | --- |
| transform | `CTransform\|CTransformUnaligned` |  |


  

### `CTransformUnaligned.AsTransform`

```lua
CTransformUnaligned.AsTransform(t: CTransformUnaligned): CTransform
```

Returns a copy as an aligned `CTransform`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransformUnaligned` | The transform to convert. |


  

### `CTransformUnaligned.IsValid`

```lua
CTransformUnaligned.IsValid(t: CTransformUnaligned): boolean
```

Returns true if no component of the position, the scale or the orientation is NaN or infinite.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `CTransformUnaligned` | The transform to check. |


  

### `CTransformUnaligned.Copy`

```lua
CTransformUnaligned.Copy(src: CTransformUnaligned, dst: CTransformUnaligned)
```

Copies the position, the scale and the orientation of `src` into `dst`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `CTransformUnaligned` | The transform to copy from. |
| dst | `CTransformUnaligned` | The transform to copy into. |
