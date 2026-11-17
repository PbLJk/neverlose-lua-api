> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Math Library

## mathlib — object type

Functions for angles, vectors, rotations, transforms and geometry. When a function returns
several results, they are returned as separate Lua values in the order shown in its signature.

The math types are `Vector`, `Vector2D`, `Vector4D`, `VectorAligned`, `QAngle`, `RadianEuler`,
`DegreeEuler`, `RotationVector`, `Quaternion`, `matrix3x4_t`, `matrix3x4a_t`, `VMatrix`,
`CTransform`, `AABB_t`, `Rect_t`, `VPlane` and `Color`. They follow the rules below.

**Constructors.** If you call a constructor without arguments, `matrix3x4_t`, `matrix3x4a_t`,
`VMatrix`, `CTransform` and `CTransformUnaligned` are set to the identity. `Color()` is black
with an alpha of 255. All other types are filled with zeros. This means that `Quaternion()` has
four zero components and is not the identity rotation, and `AABB_t()` is a box with zero mins and
maxs. Use `AABB_t.Invalid()` to get an empty box. If you pass another value of the same type, the
constructor copies it. If you pass numbers, they fill the components in order and the other
components are set to zero. `Color(r, g, b)` sets the alpha to 255.

**Changing a value or returning a new one.** A method that is described as working "in place"
changes the value it is called on and returns it. A method with a past participle name returns a
new value and does not change the original. For example, `Normalize` changes the vector and
`Normalized` returns a new vector. The same is true for `Scale` and `Scaled`.

`Copy(src, dst)` copies the first argument into the second argument. This means that
`a:Copy(b)` writes the value of `a` into `b`.

**Views.** Methods with names that start with `As` return a copy of the value. There are three
exceptions. `Vector:AsVector2D`, `Vector4D:AsVector3D` and `Vector4D:AsVector2D` return views
that share memory with the original value. Changes to a view also change the original value.

**Fallback values.** `Vector:NormalizedSafe(fallback)` returns the fallback object itself when the
length of the vector is zero. `VectorAligned:NormalizedSafe` returns a copy of the fallback.

**Units.** `QAngle` and `DegreeEuler` use degrees. `RadianEuler` and `RotationVector` use
radians. Quaternion functions give the unit for each parameter.

**Equality.** The default tolerance of `CTransform:IsEqualTo` is 0.00001. The default tolerance
for the rotation is twice the position tolerance. The default tolerances of
`mathlib.TransformsAreEqual` are 0.01 for the position and 0.1 for the rotation.


  

### `mathlib.AngleNormalize`

```lua
mathlib.AngleNormalize(degrees: number): number
```

Wraps an angle in degrees into the range from -180 up to, but not including, 180.


| Parameter | Type | Description |
| --- | --- | --- |
| degrees | `number` | The angle in degrees. |


  

### `mathlib.AngleNormalizePositive`

```lua
mathlib.AngleNormalizePositive(degrees: number): number
```

Wraps an angle in degrees into the range from 0 up to, but not including, 360.


| Parameter | Type | Description |
| --- | --- | --- |
| degrees | `number` | The angle in degrees. |


  

### `mathlib.AngleMod`

```lua
mathlib.AngleMod(degrees: number): number
```

The same function as `AngleNormalizePositive`.


| Parameter | Type | Description |
| --- | --- | --- |
| degrees | `number` | The angle in degrees. |


  

### `mathlib.AngleDiff`

```lua
mathlib.AngleDiff(dest: number, src: number): number
```

Returns the shortest signed difference in degrees from `src` to `dest`. The result is in the range from -180 up to, but not including, 180.


| Parameter | Type | Description |
| --- | --- | --- |
| dest | `number` | The destination angle in degrees. |
| src | `number` | The source angle in degrees. |


  

### `mathlib.UTIL_VecToYaw`

```lua
mathlib.UTIL_VecToYaw(forward: Vector): number
```

Returns the yaw of a forward vector in degrees, in the range from 0 up to, but not including, 360. Returns 0 for a vertical vector.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |


  

### `mathlib.InterpolateAngles`

```lua
mathlib.InterpolateAngles(a: QAngle, b: QAngle, t: number): QAngle
```

Interpolates between two sets of angles. The angles are converted to quaternions first, so the result is correct when the angles cross 180 degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `QAngle` | The start angles. |
| b | `QAngle` | The end angles. |
| t | `number` | The interpolation factor. |


  

### `mathlib.QAngleFromForwardVector`

```lua
mathlib.QAngleFromForwardVector(forward: Vector[, pseudo_up: Vector]): QAngle
```

Returns the angles that look along a forward vector.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |
| pseudo_up? | `Vector` | The up direction that is used to calculate the roll. |


    
Without `pseudo_up`, the pitch and yaw are in the range from 0 up to, but not including, 360,
and the roll is zero. With `pseudo_up`, the roll is also calculated, and the result is the same
as the result of `Vector.ToAngle`.


  

  

### `mathlib.QAngleToVectorsFLU`

```lua
mathlib.QAngleToVectorsFLU(angles: QAngle): Vector, Vector, Vector
```

Returns the forward, left and up vectors of a set of angles. The same function as `QAngle.GetLeftVectors`.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` | The angles to convert. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.TransformAnglesToLocalSpace`

```lua
mathlib.TransformAnglesToLocalSpace(angles: QAngle, parent: matrix3x4_t|matrix3x4a_t|CTransform): QAngle
```

Converts angles in world space to angles that are relative to a parent transform.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` | The angles in world space. |
| parent | `matrix3x4_t\|matrix3x4a_t\|CTransform` | The transform from the parent space to world space. |


  

### `mathlib.TransformAnglesToWorldSpace`

```lua
mathlib.TransformAnglesToWorldSpace(angles: QAngle, parent: matrix3x4_t|matrix3x4a_t|CTransform): QAngle
```

Converts angles that are relative to a parent transform to angles in world space.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` | The angles relative to the parent. |
| parent | `matrix3x4_t\|matrix3x4a_t\|CTransform` | The transform from the parent space to world space. |


  

### `mathlib.VectorLerp`

```lua
mathlib.VectorLerp(a: T, b: T, t: number): T
```

Linearly interpolates between two vectors. For `VectorAligned` values, use `mathlib.Lerp(t, a, b)`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` | The start value. |
| b | `T` | The end value. |
| t | `number` | The interpolation factor. |


  

### `mathlib.InterpolateVectors`

```lua
mathlib.InterpolateVectors(a: T, b: T, t: number): T
```

The same function as `VectorLerp`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` | The start value. |
| b | `T` | The end value. |
| t | `number` | The interpolation factor. |


  

### `mathlib.VectorVectorsFLU`

```lua
mathlib.VectorVectorsFLU(forward: Vector): Vector, Vector
```

Returns the left and up vectors for a forward direction. The same function as `Vector.GetLeftVectors`.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |


| Return | Type | Description |
| --- | --- | --- |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.VectorYawRotate`

```lua
mathlib.VectorYawRotate(v: T, yaw: number): T
```

Rotates a vector around the Z axis. The result has the same type as `v`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `T` | The vector to rotate. |
| yaw | `number` | The rotation in degrees. |


  

### `mathlib.VectorPerpendicularToVector`

```lua
mathlib.VectorPerpendicularToVector(v: Vector): Vector
```

Returns a unit vector that is perpendicular to a unit vector. The result changes smoothly as the input gets close to straight up.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector` | The direction, with a length of 1. |


  

### `mathlib.VectorOrthoNormalToVector`

```lua
mathlib.VectorOrthoNormalToVector(up: Vector, forward: Vector): Vector
```

Removes the part of `up` that points along `forward`, and normalizes the result. If the two vectors are parallel, the function returns the result of `VectorPerpendicularToVector(forward)`.


| Parameter | Type | Description |
| --- | --- | --- |
| up | `Vector` | The up direction to adjust. |
| forward | `Vector` | The direction, with a length of 1. |


  

### `mathlib.CalcClosestPointOnLineSegment`

```lua
mathlib.CalcClosestPointOnLineSegment(p: Vector, a: Vector, b: Vector): Vector, number
```

Returns the point on the line segment from `a` to `b` that is closest to `p`. The second result is the position of that point along the segment, clamped to the range from 0 to 1.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `Vector` | The point to project. |
| a | `Vector` | The start of the segment. |
| b | `Vector` | The end of the segment. |


| Return | Type | Description |
| --- | --- | --- |
| closest | `Vector` |  |
| t | `number` |  |


  

### `mathlib.CalcClosestPointToLineT`

```lua
mathlib.CalcClosestPointToLineT(p: Vector, a: Vector, b: Vector): number, Vector
```

Returns the position along the line through `a` and `b` of the point that is closest to `p`. The value is 0 at `a` and 1 at `b`, and it is not clamped. The second result is the vector `b - a`. If `a` and `b` are almost at the same position, the position is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `Vector` | The point to project. |
| a | `Vector` | A point on the line. |
| b | `Vector` | A second point on the line. |


| Return | Type | Description |
| --- | --- | --- |
| t | `number` |  |
| direction | `Vector` |  |


  

### `mathlib.PointWithinViewAngle`

```lua
mathlib.PointWithinViewAngle(src: Vector, target: Vector, look: Vector, cos_half_fov: number): boolean
```

Returns true if `target` is inside the view cone of a camera.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector` | The position of the camera. |
| target | `Vector` | The point to test. |
| look | `Vector` | The forward direction of the camera, with a length of 1. |
| cos_half_fov | `number` | The cosine of half the field of view, `cos(field_of_view / 2)`. |


  

### `mathlib.Approach`

```lua
mathlib.Approach(target: T, value: T, speed: number): T
```

Moves `value` toward `target` by a distance of no more than `speed`. If `target` is closer than `speed`, the function returns `target`. Numbers move along the number line. Vectors move along the straight line between the two points.


| Parameter | Type | Description |
| --- | --- | --- |
| target | `T` | The destination. |
| value | `T` | The current value. |
| speed | `number` | The largest distance to move. |


  

### `mathlib.RemapVal`

```lua
mathlib.RemapVal(val: number, a: number, b: number, c: number, d: number): number
```

Maps `val` from the range `a` to `b` to the range `c` to `d`. The result is not clamped. If `a` equals `b`, the function returns `d` when `val` is greater than or equal to `b`, and `c` otherwise.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `number` |  |
| a | `number` |  |
| b | `number` |  |
| c | `number` |  |
| d | `number` |  |


  

### `mathlib.RemapValClamped`

```lua
mathlib.RemapValClamped(val: number, a: number, b: number, c: number, d: number): number
```

Maps `val` from the range `a` to `b` to the range `c` to `d`. The result is clamped to the range `c` to `d`. If `a` equals `b`, the function returns `d` when `val` is greater than or equal to `b`, and `c` otherwise.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `number` |  |
| a | `number` |  |
| b | `number` |  |
| c | `number` |  |
| d | `number` |  |


  

### `mathlib.RemapIntVal`

```lua
mathlib.RemapIntVal(val: integer, a: integer, b: integer, c: integer, d: integer): integer
```

Maps an integer from the range `a` to `b` to the range `c` to `d`. The distance from `c` is truncated toward zero before it is added to `c`. The result is not clamped.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `integer` |  |
| a | `integer` |  |
| b | `integer` |  |
| c | `integer` |  |
| d | `integer` |  |


  

### `mathlib.RemapIntValClamped`

```lua
mathlib.RemapIntValClamped(val: integer, a: integer, b: integer, c: integer, d: integer): integer
```

The same as `RemapIntVal`, but the result is clamped to the range `c` to `d`.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `integer` |  |
| a | `integer` |  |
| b | `integer` |  |
| c | `integer` |  |
| d | `integer` |  |


  

### `mathlib.SimpleSpline`

```lua
mathlib.SimpleSpline(t: number): number
```

Returns the Hermite ease curve `t * t * (3 - 2 * t)`.


| Parameter | Type | Description |
| --- | --- | --- |
| t | `number` | A value from 0 to 1. |


  

### `mathlib.SimpleSplineRemapVal`

```lua
mathlib.SimpleSplineRemapVal(val: number, a: number, b: number, c: number, d: number): number
```

The same as `RemapVal`, but the position in the input range is eased with `SimpleSpline`.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `number` |  |
| a | `number` |  |
| b | `number` |  |
| c | `number` |  |
| d | `number` |  |


  

### `mathlib.SimpleSplineRemapValClamped`

```lua
mathlib.SimpleSplineRemapValClamped(val: number, a: number, b: number, c: number, d: number): number
```

The same as `SimpleSplineRemapVal`, but the result is clamped to the range `c` to `d`.


| Parameter | Type | Description |
| --- | --- | --- |
| val | `number` |  |
| a | `number` |  |
| b | `number` |  |
| c | `number` |  |
| d | `number` |  |


  

### `mathlib.FLerp`

```lua
mathlib.FLerp(f1: number, f2: number, i1: number, i2: number, x: number): number
```

Returns the value at `x` of the line that goes through the points `(i1, f1)` and `(i2, f2)`.


| Parameter | Type | Description |
| --- | --- | --- |
| f1 | `number` |  |
| f2 | `number` |  |
| i1 | `number` |  |
| i2 | `number` |  |
| x | `number` |  |


  

### `mathlib.Lerp`

```lua
mathlib.Lerp(percent: number, a: T, b: T): T
```

Linear interpolation that returns `a + (b - a) * percent`. The interpolation factor is the first argument. Works with numbers and with all types that support `+`, `-` and multiplication by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| percent | `number` | The interpolation factor. |
| a | `T` | The start value. |
| b | `T` | The end value. |


  

### `mathlib.Snap`

```lua
mathlib.Snap(value: T, step: number): T
```

Rounds a value to the nearest multiple of `step`. Vectors are rounded one component at a time.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `T` | The value to round. |
| step | `number` | The size of the grid. |


  

### `mathlib.Sign`

```lua
mathlib.Sign(x: number): integer
```

Returns 1 for zero and positive values, and -1 for negative values.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |


  

### `mathlib.WrapInt`

```lua
mathlib.WrapInt(x: integer, limit: integer): integer
```

Wraps an integer into the range from 0 up to, but not including, `limit`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` |  |
| limit | `integer` |  |


  

### `mathlib.Clamp`

```lua
mathlib.Clamp(value: T, min: T, max: T): T
```

Clamps a number between two numbers. For vectors, each component is clamped between the same components of `min` and `max`.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `T` | The value to clamp. |
| min | `T` | The lower limit. |
| max | `T` | The upper limit. |


  

### `mathlib.SmoothDamp`

```lua
mathlib.SmoothDamp(current: number, target: number, velocity: number, smooth_time: number, dt: number): number, number
```

Moves a value toward `target` with a critically damped spring.


| Parameter | Type | Description |
| --- | --- | --- |
| current | `number` | The current value. |
| target | `number` | The destination. |
| velocity | `number` | The current velocity. |
| smooth_time | `number` | The approximate time in seconds to reach the target. |
| dt | `number` | The frame time in seconds. |


| Return | Type | Description |
| --- | --- | --- |
| value | `number` |  |
| velocity | `number` |  |


    
Numbers are passed by value, so the new velocity is returned as the second result. Save it and
pass it to the next call. If `smooth_time` is 0 or less, the function returns `target` and the
old velocity. If `dt` is 0 or less, the function returns `current` and the old velocity.


  

  

### `mathlib.SmoothDamp`

```lua
mathlib.SmoothDamp(current: T, target: T, velocity: T, smooth_time: number, dt: number): T
```

The vector version of `SmoothDamp`. The function changes `velocity` in place and returns the new value as a new object.


| Parameter | Type | Description |
| --- | --- | --- |
| current | `T` | The current value. |
| target | `T` | The destination. |
| velocity | `T` | The current velocity. The function writes the new velocity into it. |
| smooth_time | `number` | The approximate time in seconds to reach the target. |
| dt | `number` | The frame time in seconds. |


    
If `smooth_time` is 0 or less, the function returns a copy of `target`. If `dt` is 0 or less, the
function returns a copy of `current`. In both cases `velocity` does not change.


  

  

### `mathlib.SmoothDamp`

```lua
mathlib.SmoothDamp(current: T, target: T, velocity: RotationVector, smooth_time: number, dt: number): T
```

The quaternion version of `SmoothDamp`. The angular velocity is a `RotationVector` in degrees per second, and the function changes it in place. The returned orientation is normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| current | `T` | The current orientation. |
| target | `T` | The destination orientation. |
| velocity | `RotationVector` | The current angular velocity. The function writes the new velocity into it. |
| smooth_time | `number` | The approximate time in seconds to reach the target. |
| dt | `number` | The frame time in seconds. |


  

### `mathlib.CalcAngularVelocity`

```lua
mathlib.CalcAngularVelocity(q_end: Quaternion|QAngle, q_begin: Quaternion|QAngle, dt: number): RotationVector
```

Estimates the angular velocity between two orientations, in degrees per second. Accepts two quaternions or two `QAngle` values.


| Parameter | Type | Description |
| --- | --- | --- |
| q_end | `Quaternion\|QAngle` | The later orientation. |
| q_begin | `Quaternion\|QAngle` | The earlier orientation. |
| dt | `number` | The time between the two orientations. If it is 0, 1 is used. |


    
The estimate is accurate for small changes in rotation. Use it with consecutive orientations,
because large changes give less accurate results.


  

  

### `mathlib.CalcAngularVelocityForForwardDirectionRotation`

```lua
mathlib.CalcAngularVelocityForForwardDirectionRotation(v_end: Vector, v_start: Vector, dt: number[, max_speed: number]): RotationVector
```

Estimates the angular velocity between two directions, in degrees per second. The result can be limited to a maximum speed.


| Parameter | Type | Description |
| --- | --- | --- |
| v_end | `Vector` | The later direction. |
| v_start | `Vector` | The earlier direction. |
| dt | `number` | The time between the two directions. If it is 0, 1 is used. |
| max_speed? | `number` | The maximum speed in degrees per second. If it is `nil`, 0 or negative, the speed is not limited. |


    
The axis is the cross product of the two normalized directions, and the angle is the arcsine of
the length of the cross product. Because of this, a turn of more than 90 degrees gives a smaller
angle, and two opposite directions give zero. Use it with small changes between consecutive
directions.


  

  

### `mathlib.Grassia`

```lua
mathlib.Grassia(v: Vector): QuaternionStorage
```

Converts a rotation vector in radians to a unit quaternion. The direction of the vector is the rotation axis, and its length is the rotation angle.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector` | The rotation axis multiplied by the angle in radians. |


  

### `mathlib.GrassiaExp`

```lua
mathlib.GrassiaExp(v: Vector): Quaternion
```

The same as `Grassia`, but the result is an aligned `Quaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector` | The rotation axis multiplied by the angle in radians. |


  

### `mathlib.Bias`

```lua
mathlib.Bias(x: number, amount: number): number
```

Perlin bias. Pushes a value from 0 to 1 toward 0 or toward 1. `x` is clamped to the range from 0 to 1.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| amount | `number` | The strength of the bias. 0.5 returns `x` unchanged. |


  

### `mathlib.Gain`

```lua
mathlib.Gain(x: number, amount: number): number
```

Perlin gain, built from `Bias`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| amount | `number` | The strength of the gain. 0.5 returns `x` unchanged. |


  

### `mathlib.Bias_Perlin`

```lua
mathlib.Bias_Perlin(x: number, amount: number): number
```

Bias that uses a power curve. `x` and `amount` are clamped to the range from 0 to 1.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| amount | `number` |  |


  

### `mathlib.Gain_Perlin`

```lua
mathlib.Gain_Perlin(x: number, amount: number): number
```

Gain built from `Bias_Perlin`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| amount | `number` |  |


  

### `mathlib.SmoothCurve`

```lua
mathlib.SmoothCurve(x: number): number
```

Returns the smooth curve `(1 - cos(x * pi)) / 2`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | A value from 0 to 1. |


  

### `mathlib.AngleQuaternion`

```lua
mathlib.AngleQuaternion(angles: QAngle|RadianEuler|DegreeEuler): Quaternion
```

Returns a quaternion from angles. The same as the `Quaternion` constructor.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle\|RadianEuler\|DegreeEuler` | The rotation. |


  

### `mathlib.AxisAngleQuaternion`

```lua
mathlib.AxisAngleQuaternion(axis: Vector, degrees: number): Quaternion
```

Returns a quaternion that rotates around a unit axis by an angle in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The axis, with a length of 1. |
| degrees | `number` | The angle in degrees. |


  

### `mathlib.AxisAngleRadiansQuaternion`

```lua
mathlib.AxisAngleRadiansQuaternion(axis: Vector, radians: number): Quaternion
```

Returns a quaternion that rotates around a unit axis by an angle in radians.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The axis, with a length of 1. |
| radians | `number` | The angle in radians. |


  

### `mathlib.BasisToQuaternionFLU`

```lua
mathlib.BasisToQuaternionFLU(forward: Vector, left: Vector, up: Vector): Quaternion
```

Returns a quaternion from three orthonormal vectors that point forward, left and up.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.QuaternionSlerp`

```lua
mathlib.QuaternionSlerp(p: T, q: T, t: number): T
```

An approximation of spherical interpolation along the shorter arc. The result has the same quaternion type as `p`.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` | The start orientation. |
| q | `T` | The end orientation. |
| t | `number` | The interpolation factor. |


  

### `mathlib.QuaternionBlend`

```lua
mathlib.QuaternionBlend(p: T, q: T, t: number): T
```

Aligns `q` to `p` with `QuaternionAlign`, interpolates linearly and normalizes the result.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` | The start orientation. |
| q | `T` | The end orientation. |
| t | `number` | The interpolation factor. |


  

### `mathlib.QuaternionBlendNoAlign`

```lua
mathlib.QuaternionBlendNoAlign(p: T, q: T, t: number): T
```

Interpolates linearly and normalizes the result. Unlike `QuaternionBlend`, this function does not align `q` to `p` first.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` | The start orientation. |
| q | `T` | The end orientation. |
| t | `number` | The interpolation factor. |


  

### `mathlib.QuaternionAlign`

```lua
mathlib.QuaternionAlign(p: T, q: T): T
```

Returns `q` or `-q`, whichever is closer to `p`. Both represent the same rotation.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` | The reference quaternion. |
| q | `T` | The quaternion to align. |


  

### `mathlib.QuaternionMult`

```lua
mathlib.QuaternionMult(p: Quaternion, q: Quaternion): Quaternion
```

Returns the Hamilton product. The same as `p * q`.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `Quaternion` | The left operand. |
| q | `Quaternion` | The right operand. This rotation is applied first. |


  

### `mathlib.QuaternionDiff`

```lua
mathlib.QuaternionDiff(q_to: Quaternion, q_from: Quaternion): Quaternion
```

Returns the rotation that turns `q_from` into `q_to`. This is `q_to` multiplied by the conjugate of `q_from`, with the conjugate aligned to `q_to`. The result is normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| q_to | `Quaternion` |  |
| q_from | `Quaternion` |  |


  

### `mathlib.QuaternionAngleDiff`

```lua
mathlib.QuaternionAngleDiff(p: Quaternion, q: Quaternion): number
```

Returns the angle between two orientations in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `Quaternion` |  |
| q | `Quaternion` |  |


  

### `mathlib.QuaternionAxisAngle`

```lua
mathlib.QuaternionAxisAngle(q: Quaternion): Vector, number
```

Returns the rotation axis of a quaternion and the rotation angle in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` |  |


| Return | Type | Description |
| --- | --- | --- |
| axis | `Vector` |  |
| degrees | `number` |  |


  

### `mathlib.QuaternionLookAt`

```lua
mathlib.QuaternionLookAt(forward: Vector, reference_up: Vector): Quaternion
```

Returns an orientation that looks along `forward`, with its up direction as close as possible to `reference_up`.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |
| reference_up | `Vector` | The up direction. The part that points along `forward` is removed. |


  

### `mathlib.QuaternionFromForwardVector`

```lua
mathlib.QuaternionFromForwardVector(forward: Vector): Quaternion
```

Returns an orientation that looks along `forward`, with the world Z axis as the up direction. If `forward` is vertical, the X axis is used as the up direction.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |


  

### `mathlib.QuaternionIdentityBlend`

```lua
mathlib.QuaternionIdentityBlend(p: T, t: number): T
```

Blends a quaternion toward the identity. When `t` is 0, the result is `p`. When `t` is 1, the result is the identity.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` |  |
| t | `number` |  |


  

### `mathlib.QuaternionLn`

```lua
mathlib.QuaternionLn(p: T): T
```

Returns the quaternion logarithm.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` |  |


  

### `mathlib.QuaternionExp`

```lua
mathlib.QuaternionExp(p: T): T
```

Returns the quaternion exponential. This is the inverse of `QuaternionLn`.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` |  |


  

### `mathlib.QuaternionAverageExponential`

```lua
mathlib.QuaternionAverageExponential(list: T[][, weights: number[]]): T
```

Returns the weighted average of a list of quaternions. The average is calculated in log space.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `T[]` | The quaternions to average. There must be at least one. |
| weights? | `number[]` | The weights. Each weight is 1 by default. |


    
`list` is a Lua array of quaternions. `weights` is an optional Lua array of numbers, with one
weight for each quaternion. If `list` is empty, the function throws an error.


  

  

### `mathlib.BuildRotateBetweenVectorsQuaternion`

```lua
mathlib.BuildRotateBetweenVectorsQuaternion(from: Vector, to: Vector): Quaternion
```

Returns the rotation that turns one unit vector into another. If the vectors point in opposite directions, the result is a half turn around an axis that is perpendicular to `from`.


| Parameter | Type | Description |
| --- | --- | --- |
| from | `Vector` | The start direction, with a length of 1. |
| to | `Vector` | The end direction, with a length of 1. |


  

### `mathlib.ShortestArc`

```lua
mathlib.ShortestArc(v1: Vector, v2: Vector): Quaternion
```

The same function as `BuildRotateBetweenVectorsQuaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| v1 | `Vector` | The start direction, with a length of 1. |
| v2 | `Vector` | The end direction, with a length of 1. |


  

### `mathlib.SplineQuaternions`

```lua
mathlib.SplineQuaternions(a: T, b: T, t: number): T
```

Interpolates between two quaternions along a smooth rotation path. The result has the same quaternion type as `a`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |
| t | `number` |  |


  

### `mathlib.Exp`

```lua
mathlib.Exp(v: Vector): Quaternion
```

The exponential map for an axis and angle in radians. `Exp(v)` returns a rotation around `v` by twice the length of `v`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector` |  |


  

### `mathlib.Log`

```lua
mathlib.Log(q: Quaternion): Vector
```

The inverse of `Exp`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion` |  |


  

### `mathlib.AngleMatrix`

```lua
mathlib.AngleMatrix(angles: QAngle|RadianEuler[, position: Vector, scale: number|Vector]): matrix3x4_t
```

Returns a rotation matrix from angles. You can also give a position and a scale. A number scales all axes by the same amount. A `Vector` scales each axis by its own component.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle\|RadianEuler` |  |
| position? | `Vector` |  |
| scale? | `number\|Vector` |  |


  

### `mathlib.AngleIMatrix`

```lua
mathlib.AngleIMatrix(angles: QAngle|RadianEuler[, position: Vector]): matrix3x4_t
```

Returns the inverse of the matrix that `AngleMatrix` returns.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle\|RadianEuler` |  |
| position? | `Vector` |  |


  

### `mathlib.MatrixAngles`

```lua
mathlib.MatrixAngles(matrix: matrix3x4_t|matrix3x4a_t): QAngle, Vector, number
```

Returns the angles, the position and the scale of a matrix. The scale is the length of the X basis column.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


| Return | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |
| position | `Vector` |  |
| scale | `number` |  |


  

### `mathlib.QuaternionMatrix`

```lua
mathlib.QuaternionMatrix(q: Quaternion|QuaternionStorage[, position: Vector, scale: number|Vector]): matrix3x4_t|matrix3x4a_t
```

Returns a rotation matrix from a quaternion. You can also give a position and a scale. A number scales all axes by the same amount. A `Vector` scales each axis by its own component. The result is always a `matrix3x4_t`.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |
| position? | `Vector` |  |
| scale? | `number\|Vector` |  |


  

### `mathlib.MatrixQuaternion`

```lua
mathlib.MatrixQuaternion(matrix: matrix3x4_t|matrix3x4a_t): Quaternion, Vector, number
```

Returns the quaternion, the position and the scale of a matrix. The scale is the length of the X basis column.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


| Return | Type | Description |
| --- | --- | --- |
| q | `Quaternion` |  |
| position | `Vector` |  |
| scale | `number` |  |


  

### `mathlib.MatrixPosition`

```lua
mathlib.MatrixPosition(matrix: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the origin column of a matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `mathlib.PositionMatrix`

```lua
mathlib.PositionMatrix(position: Vector): matrix3x4_t
```

Returns a matrix with no rotation and the given origin.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector` |  |


  

### `mathlib.MatrixBuildRotationAboutAxis`

```lua
mathlib.MatrixBuildRotationAboutAxis(axis: Vector, degrees: number): matrix3x4_t
```

Returns a matrix that rotates around a unit axis by an angle in degrees. Pass the result to `VMatrix(...)` to get a 4x4 matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The axis, with a length of 1. |
| degrees | `number` |  |


  

### `mathlib.ConcatTransforms`

```lua
mathlib.ConcatTransforms(a: T, b: T): T
```

Returns `a * b`. The right operand `b` is applied first.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |


  

### `mathlib.ConcatRotations`

```lua
mathlib.ConcatRotations(a: T, b: T): T
```

Returns `a * b` with the origin set to zero.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |


  

### `mathlib.MatrixInvert`

```lua
mathlib.MatrixInvert(matrix: T): T
```

Returns the inverse of a matrix that has a rotation, a translation and the same scale on all axes. The scale is taken from the X basis column.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


  

### `mathlib.MatrixInvertTR`

```lua
mathlib.MatrixInvertTR(matrix: T): T
```

Returns the inverse of a matrix that has only a rotation and a translation. The same as `matrix3x4_t.InverseTR`.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


  

### `mathlib.MatrixInvertGeneral`

```lua
mathlib.MatrixInvertGeneral(matrix: T): boolean, T
```

Returns the inverse of any 3x4 matrix. If the matrix cannot be inverted, the first result is false and the second result is the identity matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| inverse | `T` |  |


  

### `mathlib.MatrixTranspose`

```lua
mathlib.MatrixTranspose(matrix: T): T
```

Returns the transposed rotation with the origin set to zero. The same as `matrix3x4_t.Transposed`.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


  

### `mathlib.MatrixNormalize`

```lua
mathlib.MatrixNormalize(matrix: T): Vector, T
```

Returns the scale of each basis column, and then the matrix with basis columns of length 1. The origin does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


| Return | Type | Description |
| --- | --- | --- |
| scale | `Vector` |  |
| normalized | `T` |  |


  

### `mathlib.MatrixOrthogonalize`

```lua
mathlib.MatrixOrthogonalize(matrix: T): T
```

Makes the basis columns orthonormal with the Gram-Schmidt process. The origin does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `T` |  |


  

### `mathlib.ComputeMatrixScale`

```lua
mathlib.ComputeMatrixScale(matrix: matrix3x4_t|matrix3x4a_t): Vector
```

Returns the lengths of the three basis columns.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `mathlib.ComputeMatrixMaxScale`

```lua
mathlib.ComputeMatrixMaxScale(matrix: matrix3x4_t|matrix3x4a_t): number
```

Returns the length of the longest basis column.


| Parameter | Type | Description |
| --- | --- | --- |
| matrix | `matrix3x4_t\|matrix3x4a_t` |  |


  

### `mathlib.TransformSlerp`

```lua
mathlib.TransformSlerp(p: CTransform, q: CTransform, t: number): CTransform
```

Interpolates between two transforms. The orientation is interpolated with `QuaternionSlerp`. The position and the scale are interpolated linearly.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `CTransform` |  |
| q | `CTransform` |  |
| t | `number` |  |


  

### `mathlib.Slerp`

```lua
mathlib.Slerp(p: CTransform, q: CTransform, t: number): CTransform
```

The same function as `TransformSlerp`.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `CTransform` |  |
| q | `CTransform` |  |
| t | `number` |  |


  

### `mathlib.TransformLerp`

```lua
mathlib.TransformLerp(p: CTransform, q: CTransform, t: number): CTransform
```

Interpolates between two transforms. The function aligns the signs of the two quaternions, blends them linearly and normalizes the result. The position and the scale are interpolated linearly.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `CTransform` |  |
| q | `CTransform` |  |
| t | `number` |  |


    
If the blended quaternion has a length of zero, the identity is used. `t` is not clamped.


  

  

### `mathlib.TransformDeltaNoScale`

```lua
mathlib.TransformDeltaNoScale(from: CTransform, to: CTransform): CTransform
```

Returns the change from one transform to another, without the scale. The orientation is the orientation of `to` multiplied by the inverse orientation of `from`. The origin is the vector from the origin of `from` to the origin of `to`, rotated by the inverse orientation of `from`. The scale is 1.


| Parameter | Type | Description |
| --- | --- | --- |
| from | `CTransform` |  |
| to | `CTransform` |  |


  

### `mathlib.TransformsAreEqual`

```lua
mathlib.TransformsAreEqual(a: CTransform, b: CTransform[, position_tolerance: number, rotation_tolerance: number]): boolean
```

Returns true if two transforms are equal within a tolerance. The positions are compared with an absolute tolerance. The scales and orientations are compared with a tolerance on the mantissa, in the same way as `FloatsAreEqual`. A quaternion and its negative are treated as equal.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `CTransform` |  |
| b | `CTransform` |  |
| position_tolerance? | `number` | The default is 0.01. |
| rotation_tolerance? | `number` | The default is 0.1. |


  

### `mathlib.AxisAngleTransform`

```lua
mathlib.AxisAngleTransform(axis: Vector, degrees: number): CTransform
```

Returns a transform that rotates around a unit axis by an angle in degrees. The position is the origin and the scale is 1.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The axis, with a length of 1. |
| degrees | `number` |  |


  

### `mathlib.SetupMatrixIdentity`

```lua
mathlib.SetupMatrixIdentity(): VMatrix
```

Returns a new identity `VMatrix`.


  

### `mathlib.MatrixSetIdentity`

```lua
mathlib.MatrixSetIdentity(): VMatrix
```

Returns a new identity `VMatrix`. The same function as `SetupMatrixIdentity`.


  

### `mathlib.MatrixInverseGeneral`

```lua
mathlib.MatrixInverseGeneral(vm: VMatrix): boolean, VMatrix
```

Returns the inverse of a 4x4 matrix. If the matrix cannot be inverted, or is too close to that for single precision numbers, the first result is false and the second result is the identity matrix. Use `MatrixInvertGeneral` for 3x4 matrices.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| inverse | `VMatrix` |  |


  

### `mathlib.SetupMatrixScale`

```lua
mathlib.SetupMatrixScale(scale: Vector): VMatrix
```

Returns a scale matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| scale | `Vector` | The scale on each axis. |


  

### `mathlib.SetupMatrixTranslation`

```lua
mathlib.SetupMatrixTranslation(translation: Vector): VMatrix
```

Returns a translation matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| translation | `Vector` |  |


  

### `mathlib.SetupMatrixAxisRot`

```lua
mathlib.SetupMatrixAxisRot(axis: Vector, degrees: number): VMatrix
```

Returns a matrix that rotates around a unit axis by an angle in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| axis | `Vector` | The axis, with a length of 1. |
| degrees | `number` |  |


  

### `mathlib.SetupMatrixAxisToAxisRot`

```lua
mathlib.SetupMatrixAxisToAxisRot(from: Vector, to: Vector): VMatrix
```

Returns a matrix that rotates one unit vector onto another. If the vectors are parallel, the function returns the identity matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| from | `Vector` | The start direction, with a length of 1. |
| to | `Vector` | The end direction, with a length of 1. |


  

### `mathlib.SetupMatrixAngles`

```lua
mathlib.SetupMatrixAngles(angles: QAngle): VMatrix
```

Returns a rotation matrix from angles.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `mathlib.SetupMatrixOrgAngles`

```lua
mathlib.SetupMatrixOrgAngles(origin: Vector, angles: QAngle): VMatrix
```

Returns a matrix with a rotation from angles and a translation to an origin.


| Parameter | Type | Description |
| --- | --- | --- |
| origin | `Vector` |  |
| angles | `QAngle` |  |


  

### `mathlib.MatrixFromAngles`

```lua
mathlib.MatrixFromAngles(angles: QAngle): VMatrix
```

The same function as `SetupMatrixAngles`.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `mathlib.MatrixToAngles`

```lua
mathlib.MatrixToAngles(vm: VMatrix): QAngle
```

Returns the angles of the upper 3x3 part of a `VMatrix`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |


  

### `mathlib.MatrixBuildPerspective`

```lua
mathlib.MatrixBuildPerspective(fov_x: number, fov_y: number, z_near: number, z_far: number): VMatrix
```

Returns a perspective projection matrix that looks along +Z.


| Parameter | Type | Description |
| --- | --- | --- |
| fov_x | `number` | The horizontal field of view in degrees. |
| fov_y | `number` | The vertical field of view in degrees. |
| z_near | `number` | The distance to the near plane. Must be positive. |
| z_far | `number` | The distance to the far plane. Must be positive. |


    
After `V3Mul`, points inside the view frustum are mapped to the range from 0 to 1 on each axis.
The +X and +Y directions of the view space map toward 0. The near plane maps to z = 0 and the far
plane maps to z = 1.


  

  

### `mathlib.AlmostEqual`

```lua
mathlib.AlmostEqual(a: T, b: T[, max_ulps: integer]): boolean
```

Compares two numbers or two vectors by their distance in units in the last place of their 32 bit float representation. Returns false if a value is NaN. Values with different signs are equal only if they are exactly equal.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |
| max_ulps? | `integer` | The largest allowed distance in units in the last place. The default is 10. |


  

### `mathlib.FloatsAreEqual`

```lua
mathlib.FloatsAreEqual(a: number, b: number, tolerance: number): boolean
```

Compares the mantissas of two numbers after their exponents are aligned. The tolerance is looser for numbers close to zero.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `number` |  |
| b | `number` |  |
| tolerance | `number` |  |


  

### `mathlib.FloatsAreWithinTolerance`

```lua
mathlib.FloatsAreWithinTolerance(a: number, b: number, tolerance: number): boolean
```

Returns true if `|a - b| <= tolerance`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `number` |  |
| b | `number` |  |
| tolerance | `number` |  |


  

### `mathlib.CloseEnough`

```lua
mathlib.CloseEnough(a: number, b: number[, epsilon: number]): boolean
```

Returns true if `|a - b| <= epsilon`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `number` |  |
| b | `number` |  |
| epsilon? | `number` | The default is 0.001. |


  

### `mathlib.QuaternionsAreEqual`

```lua
mathlib.QuaternionsAreEqual(a: Quaternion|QuaternionStorage, b: Quaternion|QuaternionStorage, tolerance: number): boolean
```

Compares the components of two quaternions with `FloatsAreEqual`. A quaternion and its negative are treated as equal.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Quaternion\|QuaternionStorage` |  |
| b | `Quaternion\|QuaternionStorage` |  |
| tolerance | `number` |  |


  

### `mathlib.MatricesAreEqual`

```lua
mathlib.MatricesAreEqual(a: T, b: T[, tolerance: number]): boolean
```

Compares two matrices element by element with an absolute tolerance. For 3x4 matrices, every element is compared. For `VMatrix` values, only the upper 3x3 part is compared.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |
| tolerance? | `number` | The default is 0.00001. |


  

### `mathlib.RotationsAreEqual`

```lua
mathlib.RotationsAreEqual(a: matrix3x4_t|matrix3x4a_t, b: matrix3x4_t|matrix3x4a_t[, tolerance: number]): boolean
```

Compares the upper 3x3 parts of two 3x4 matrices with an absolute tolerance.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `matrix3x4_t\|matrix3x4a_t` |  |
| b | `matrix3x4_t\|matrix3x4a_t` |  |
| tolerance? | `number` | The default is 0.00001. |


  

### `mathlib.GetRelativeDifferenceSqr`

```lua
mathlib.GetRelativeDifferenceSqr(a: Vector, b: Vector): number
```

Returns the squared relative difference `|a - b|² / max(1, |a|², |b|²)`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector` |  |
| b | `Vector` |  |


  

### `mathlib.GetRelativeDifference`

```lua
mathlib.GetRelativeDifference(a: T, b: T): number
```

Returns the square root of `GetRelativeDifferenceSqr`. For matrices, the function returns the largest value of the three basis columns and the origin.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `T` |  |
| b | `T` |  |


  

### `mathlib.VectorVectorsFLUPreserveScale`

```lua
mathlib.VectorVectorsFLUPreserveScale(forward: Vector): Vector, Vector
```

Returns the left and up vectors for a forward direction. Their length is the length of `forward`.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |


| Return | Type | Description |
| --- | --- | --- |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.BuildBasisFLU`

```lua
mathlib.BuildBasisFLU(dir: Vector): Vector, Vector, Vector
```

Returns the normalized direction and orthonormal left and up vectors. The left and up vectors are built from the world X axis, or from the world Y axis if the direction is almost parallel to X.


| Parameter | Type | Description |
| --- | --- | --- |
| dir | `Vector` | The direction. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.MakeOrthonormalBasis`

```lua
mathlib.MakeOrthonormalBasis(n: Vector): Vector, Vector
```

Returns two unit vectors that are orthonormal to a unit normal. The result changes smoothly for all directions of the normal.


| Parameter | Type | Description |
| --- | --- | --- |
| n | `Vector` | The normal, with a length of 1. |


| Return | Type | Description |
| --- | --- | --- |
| b1 | `Vector` |  |
| b2 | `Vector` |  |


  

### `mathlib.VectorMatrix`

```lua
mathlib.VectorMatrix(forward: Vector): matrix3x4a_t
```

Returns a rotation matrix with `forward` as its X column and the origin at zero. `forward` is not normalized. The Y and Z columns have a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| forward | `Vector` | The direction. |


  

### `mathlib.QuaternionVectorsFLU`

```lua
mathlib.QuaternionVectorsFLU(q: Quaternion|QuaternionStorage): Vector, Vector, Vector
```

Returns the forward, left and up vectors of a quaternion.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `mathlib.QuaternionScale`

```lua
mathlib.QuaternionScale(p: T, t: number): T
```

Returns a fractional power of a unit quaternion. The result rotates around the same axis by `t` times the angle.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` |  |
| t | `number` |  |


  

### `mathlib.QuaternionMultAligned`

```lua
mathlib.QuaternionMultAligned(p: T, q: T): T
```

Returns `p * QuaternionAlign(p, q)`.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `T` |  |
| q | `T` |  |


  

### `mathlib.QuaternionSM`

```lua
mathlib.QuaternionSM(s: number, p: Quaternion, q: Quaternion): Quaternion
```

Returns `(p ^ s) * q`, normalized. `q` is aligned to `p ^ s` before the multiplication.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `number` |  |
| p | `Quaternion` |  |
| q | `Quaternion` |  |


  

### `mathlib.QuaternionMA`

```lua
mathlib.QuaternionMA(p: Quaternion, s: number, q: Quaternion): Quaternion
```

Returns `p * (q ^ s)`, normalized. `q ^ s` is aligned to `p` before the multiplication.


| Parameter | Type | Description |
| --- | --- | --- |
| p | `Quaternion` |  |
| s | `number` |  |
| q | `Quaternion` |  |


  

### `mathlib.CalcAngleAboutAxis`

```lua
mathlib.CalcAngleAboutAxis(src: Vector, dst: Vector, axis: Vector): number
```

Returns the signed angle in radians from `src` to `dst` around a unit axis.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector` | The start direction. |
| dst | `Vector` | The end direction. |
| axis | `Vector` | The axis, with a length of 1. |


  

### `mathlib.CalcRotationBetweenVectors`

```lua
mathlib.CalcRotationBetweenVectors(src: Vector, dst: Vector): Quaternion
```

The same function as `BuildRotateBetweenVectorsQuaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector` | The start direction, with a length of 1. |
| dst | `Vector` | The end direction, with a length of 1. |


  

### `mathlib.CalcRotationAboutAxis`

```lua
mathlib.CalcRotationAboutAxis(src: Vector, dst: Vector, axis: Vector): Quaternion
```

Returns a rotation around `axis` by the angle `CalcAngleAboutAxis(src, dst, axis)`.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Vector` | The start direction. |
| dst | `Vector` | The end direction. |
| axis | `Vector` | The axis, with a length of 1. |


  

### `mathlib.QuaternionNormalize`

```lua
mathlib.QuaternionNormalize(q: Quaternion|QuaternionStorage): number
```

Normalizes a quaternion in place and returns its old length. A quaternion with a length of zero becomes the identity, and the function returns 1.


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


  

### `mathlib.MatrixBuildRotation`

```lua
mathlib.MatrixBuildRotation(initial: Vector, final: Vector): VMatrix
```

Returns a matrix that rotates one unit vector onto another.


| Parameter | Type | Description |
| --- | --- | --- |
| initial | `Vector` | The start direction, with a length of 1. |
| final | `Vector` | The end direction, with a length of 1. |


  

### `mathlib.MatrixBuildRotateZ`

```lua
mathlib.MatrixBuildRotateZ(degrees: number): VMatrix
```

Returns a matrix that rotates around the Z axis by an angle in degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| degrees | `number` |  |


  

### `mathlib.MatrixTranslate`

```lua
mathlib.MatrixTranslate(vm: VMatrix, translation: Vector): VMatrix
```

Returns `vm` multiplied by a translation matrix, as a new matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| translation | `Vector` |  |


  

### `mathlib.MatrixRotate`

```lua
mathlib.MatrixRotate(vm: VMatrix, axis: Vector, degrees: number): VMatrix
```

Returns `vm` multiplied by a rotation around `axis`, as a new matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| axis | `Vector` | The axis, with a length of 1. |
| degrees | `number` |  |


  

### `mathlib.MatrixInverseTranspose`

```lua
mathlib.MatrixInverseTranspose(m: T): T
```

Returns the inverse transpose of a matrix. This is the matrix that transforms normals. The result has the same type as `m`.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `T` |  |


    
If the matrix cannot be inverted, the function returns the identity matrix and does not tell you
that it failed. Use `InverseGeneral` if you need to know whether the inversion worked.


  

  

### `mathlib.MatrixGetRow`

```lua
mathlib.MatrixGetRow(vm: VMatrix, row: integer): Vector
```

Returns the first three elements of a row.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| row | `integer` | The row index, from 0 to 3. |


  

### `mathlib.MatrixSetRow`

```lua
mathlib.MatrixSetRow(vm: VMatrix, row: integer, v: Vector)
```

Sets the first three elements of a row.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| row | `integer` | The row index, from 0 to 3. |
| v | `Vector` |  |


  

### `mathlib.MatrixGetColumn`

```lua
mathlib.MatrixGetColumn(vm: VMatrix, col: integer): Vector
```

Returns the first three elements of a column.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| col | `integer` | The column index, from 0 to 3. |


  

### `mathlib.MatrixSetColumn`

```lua
mathlib.MatrixSetColumn(vm: VMatrix, col: integer, v: Vector)
```

Sets the first three elements of a column.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| col | `integer` | The column index, from 0 to 3. |
| v | `Vector` |  |


  

### `mathlib.Vector3DMultiplyProjective`

```lua
mathlib.Vector3DMultiplyProjective(vm: VMatrix, v: Vector): Vector
```

Transforms a direction by a projective matrix. The direction is rotated and then divided by the projected w. The translation is not applied.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| v | `Vector` | The direction. |


  

### `mathlib.Vector3DMultiplyPositionProjective`

```lua
mathlib.Vector3DMultiplyPositionProjective(vm: VMatrix, v: Vector): Vector
```

Transforms a point by a projective matrix, with the perspective divide. The same as `VMatrix.V3Mul`.


| Parameter | Type | Description |
| --- | --- | --- |
| vm | `VMatrix` |  |
| v | `Vector` | The point. |


  

### `mathlib.ClampCycle`

```lua
mathlib.ClampCycle(cycle: number, looping: boolean): number
```

If `looping` is true, wraps the cycle into the range from 0 up to, but not including, 1. If `looping` is false, clamps the cycle to the range from 0 to 0.999.


| Parameter | Type | Description |
| --- | --- | --- |
| cycle | `number` |  |
| looping | `boolean` |  |


  

### `mathlib.Dir`

```lua
mathlib.Dir(f: number): integer
```

Returns -1 for negative values, and 1 for zero and positive values.


| Parameter | Type | Description |
| --- | --- | --- |
| f | `number` |  |


  

### `mathlib.SameSign`

```lua
mathlib.SameSign(a: number, b: number): boolean
```

Returns true if both values have the same sign. Zero counts as positive.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `number` |  |
| b | `number` |  |


  

### `mathlib.PlaneIntersection`

```lua
mathlib.PlaneIntersection(p1: VPlane, p2: VPlane, p3: VPlane): boolean, Vector?
```

Returns the point where three planes meet. If two or more of the planes are parallel, the first result is false and the second result is `nil`.


| Parameter | Type | Description |
| --- | --- | --- |
| p1 | `VPlane` |  |
| p2 | `VPlane` |  |
| p3 | `VPlane` |  |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| point | `Vector?` |  |


  

### `mathlib.SetupMatrixReflection`

```lua
mathlib.SetupMatrixReflection(plane: VPlane): VMatrix
```

Returns a matrix that reflects points across a plane.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` |  |


  

### `mathlib.SetupMatrixProjection`

```lua
mathlib.SetupMatrixProjection(origin: Vector, plane: VPlane): VMatrix
```

Returns a matrix that projects points from an origin onto a plane. The result is a projective matrix, so apply it with `V3Mul`.


| Parameter | Type | Description |
| --- | --- | --- |
| origin | `Vector` | The center of the projection. |
| plane | `VPlane` | The plane to project onto. |


  

### `mathlib.MatrixTransformPlane`

```lua
mathlib.MatrixTransformPlane(m: matrix3x4_t|matrix3x4a_t|VMatrix, plane: VPlane): VPlane
```

Transforms a plane by a matrix. The same as the `TransformPlane` method of the matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t\|VMatrix` |  |
| plane | `VPlane` |  |


  

### `mathlib.MatrixITransformPlane`

```lua
mathlib.MatrixITransformPlane(m: matrix3x4_t|matrix3x4a_t, plane: VPlane): VPlane
```

Transforms a plane by the inverse of a 3x4 matrix. The same as the `TransformPlaneByInverse` method of the matrix.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `matrix3x4_t\|matrix3x4a_t` |  |
| plane | `VPlane` |  |


  

### `mathlib.FrustumPlanesFromMatrix`

```lua
mathlib.FrustumPlanesFromMatrix(clip_to_world: VMatrix): Frustum_t
```

Returns the six planes of a clip to world matrix as a `Frustum_t`. The plane normals point inward. The planes are in the order right, left, top, bottom, near and far.


| Parameter | Type | Description |
| --- | --- | --- |
| clip_to_world | `VMatrix` | The inverse of the view projection matrix. |


  

### `mathlib.BoxSurfaceArea`

```lua
mathlib.BoxSurfaceArea(mins: Vector, maxs: Vector): number
```

Returns the total area of the six faces of a box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `mathlib.ComputeVolume`

```lua
mathlib.ComputeVolume(mins: Vector, maxs: Vector): number
```

Returns the volume of an axis aligned box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |


  

### `mathlib.CalcSqrDistanceToAABB`

```lua
mathlib.CalcSqrDistanceToAABB(mins: Vector, maxs: Vector, point: Vector): number
```

Returns the squared distance from a point to a box. Returns 0 if the point is inside the box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |
| point | `Vector` |  |


  

### `mathlib.CalcDistanceToAABB`

```lua
mathlib.CalcDistanceToAABB(mins: Vector, maxs: Vector, point: Vector): number
```

Returns the distance from a point to a box. Returns 0 if the point is inside the box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |
| point | `Vector` |  |


  

### `mathlib.CalcSqrDistanceToAABB2D`

```lua
mathlib.CalcSqrDistanceToAABB2D(mins: Vector2D, maxs: Vector2D, point: Vector2D): number
```

Returns the squared distance from a 2D point to a 2D box. Returns 0 if the point is inside the box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector2D` |  |
| maxs | `Vector2D` |  |
| point | `Vector2D` |  |


  

### `mathlib.CalcDistanceToAABB2D`

```lua
mathlib.CalcDistanceToAABB2D(mins: Vector2D, maxs: Vector2D, point: Vector2D): number
```

Returns the distance from a 2D point to a 2D box. Returns 0 if the point is inside the box.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector2D` |  |
| maxs | `Vector2D` |  |
| point | `Vector2D` |  |


  

### `mathlib.ClosestPointOnAABB`

```lua
mathlib.ClosestPointOnAABB(mins: Vector, maxs: Vector, point: Vector): Vector
```

Returns the point in a box that is closest to a given point.


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector` |  |
| maxs | `Vector` |  |
| point | `Vector` |  |


  

### `mathlib.BoundsFromPointList`

```lua
mathlib.BoundsFromPointList(points: Vector[]): AABB_t
```

Returns the bounds of a Lua array of points. If the array is empty, the function returns an empty box, the same as `AABB_t.Invalid()`.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector[]` |  |


  

### `mathlib.BoundsFromPointList`

```lua
mathlib.BoundsFromPointList(xform: CTransform|matrix3x4_t|matrix3x4a_t, points: Vector[]): AABB_t
```

Returns the bounds of a Lua array of points after each point is transformed by `xform`. If the array is empty, the function returns an empty box, the same as `AABB_t.Invalid()`.


| Parameter | Type | Description |
| --- | --- | --- |
| xform | `CTransform\|matrix3x4_t\|matrix3x4a_t` |  |
| points | `Vector[]` |  |


  

### `mathlib.GetAabb`

```lua
mathlib.GetAabb(points: Vector[]): AABB_t
```

The same as `BoundsFromPointList(points)`.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector[]` |  |


  

### `mathlib.GetAabb`

```lua
mathlib.GetAabb(xform: CTransform|matrix3x4_t|matrix3x4a_t, points: Vector[]): AABB_t
```

The same as `BoundsFromPointList(xform, points)`.


| Parameter | Type | Description |
| --- | --- | --- |
| xform | `CTransform\|matrix3x4_t\|matrix3x4a_t` |  |
| points | `Vector[]` |  |


  

### `mathlib.TransformAABB`

```lua
mathlib.TransformAABB(xform: matrix3x4_t|matrix3x4a_t|CTransform, bounds: AABB_t): AABB_t
```

Transforms a box by a matrix or a transform. The same as the `TransformAABB` method of `xform`.


| Parameter | Type | Description |
| --- | --- | --- |
| xform | `matrix3x4_t\|matrix3x4a_t\|CTransform` |  |
| bounds | `AABB_t` |  |


  

### `mathlib.BezierEvaluate`

```lua
mathlib.BezierEvaluate(points: T[], t: number): T
```

Returns the point at `t` on a Bezier curve of any order. The function uses de Casteljau's algorithm. The control points are a Lua array of any vector type. The order of the curve is the number of control points minus one.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `T[]` | The control points. There must be at least one. |
| t | `number` | The position on the curve, from 0 to 1. |


  

### `mathlib.BezierTangent`

```lua
mathlib.BezierTangent(points: T[], t: number): T
```

Returns the derivative of the curve at `t`. This is the curve of one order lower through the points `order * (p[i + 1] - p[i])`. If there are fewer than two control points, the function throws an error.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `T[]` | The control points. There must be at least two. |
| t | `number` | The position on the curve, from 0 to 1. |


  

### `mathlib.GetProjectedAABBBounds`

```lua
mathlib.GetProjectedAABBBounds(proj_from_bounds: VMatrix, bounds: AABB_t): AABB_t
```

Returns the bounds of a box after it is projected by a matrix and divided by w. The bounds are in the output coordinates of the matrix. For a usual clip space projection, x and y are in the range from -1 to 1. For `MatrixBuildPerspective`, they are in the range from 0 to 1.


| Parameter | Type | Description |
| --- | --- | --- |
| proj_from_bounds | `VMatrix` | The projection from the space of the box to clip space. |
| bounds | `AABB_t` | The box to project. |


    
The near plane is at clip space z = 0. Corners behind the near plane are not used, and the edges
of the box are clipped at the near plane. If the whole box is behind the near plane, the function
returns `AABB_t.Invalid()`.
