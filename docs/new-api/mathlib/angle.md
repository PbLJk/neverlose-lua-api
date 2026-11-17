> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Angle


## QAngle — cdata


An angle with pitch, yaw and roll in degrees. A positive pitch looks down. A positive yaw
turns to the left. The roll tilts the view to the side.

The `+` and `-` operators add and subtract two angles. The `*` and `/` operators take a
number or an angle. With a number, every component is multiplied or divided by it. With an
angle, each component is multiplied or divided by the matching component. The unary `-`
operator returns a negated copy. The `==` operator compares every component and returns
`false` when the other value is not a `QAngle`.

```cpp lines=false
typedef struct QAngle {
    float x, y, z;
} QAngle;
```


  

### `QAngle.x`

The pitch. A positive value looks down and a negative value looks up.


  

### `QAngle.y`

The yaw. A positive value turns left and a negative value turns right.


  

### `QAngle.z`

The roll. It tilts the view to the side.


  

### `QAngle + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QAngle` |  |


  

### `QAngle - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QAngle` |  |


  

### `QAngle * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QAngle\|number` |  |


  

### `QAngle / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `QAngle\|number` |  |


  

<a id="qangle"></a>
### `-QAngle`


<a id="qangle-1"></a>

## QAngle  — ctype · callable


Call `QAngle(pitch, yaw, roll)` to create an angle. A component that is not given is set
to 0. Call `QAngle(other)` to make a copy of another angle.

The constant angles below cannot be changed.


  

### `QAngle(pitch, yaw, roll)`

```lua
QAngle([pitch: number, yaw: number, roll: number]): QAngle
```


| Parameter | Type | Description |
| --- | --- | --- |
| pitch? | `number` |  |
| yaw? | `number` |  |
| roll? | `number` |  |


  

### `QAngle(self)`

```lua
QAngle(self: QAngle): QAngle
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `QAngle` |  |


  

### `QAngle.vInvalid`

An angle with every component set to `FLT_MAX`, the largest 32 bit float.


  

### `QAngle.vZero`

The angle `(0, 0, 0)`.


  

### `QAngle.Copy`

```lua
QAngle.Copy(src: QAngle, dst: QAngle)
```

Copies the components of one angle into another angle.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `QAngle` | The angle to copy from. |
| dst | `QAngle` | The angle to copy into. |


  

### `QAngle.Pitch`

```lua
QAngle.Pitch(ang: QAngle): number
```

Returns the pitch, which is the X component.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to read. |


  

### `QAngle.Yaw`

```lua
QAngle.Yaw(ang: QAngle): number
```

Returns the yaw, which is the Y component.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to read. |


  

### `QAngle.Roll`

```lua
QAngle.Roll(ang: QAngle): number
```

Returns the roll, which is the Z component.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to read. |


  

### `QAngle.Init`

```lua
QAngle.Init(ang: QAngle[, x: number, y: number, z: number])
```

Sets the components of the angle. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to change. |
| x? | `number` | The pitch in degrees. |
| y? | `number` | The yaw in degrees. |
| z? | `number` | The roll in degrees. |


  

### `QAngle.Normalize`

```lua
QAngle.Normalize(ang: QAngle)
```

Wraps each component of the angle into the range from -180 to 180. The value -180 is included and the value 180 is not, so 180 becomes -180.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to normalize. |


  

### `QAngle.Normalize`

```lua
QAngle.Normalize(ang: number): number
```

Wraps one value in degrees into the range from -180 to 180 and returns it. The value -180 is included and the value 180 is not, so 180 becomes -180.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `number` | The value in degrees to normalize. |


  

### `QAngle.Normalized`

```lua
QAngle.Normalized(ang: QAngle): QAngle
```

Returns a copy of the angle with each component wrapped into the range from -180 to 180. The value -180 is included and the value 180 is not.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to normalize. |


  

### `QAngle.Unpack`

```lua
QAngle.Unpack(ang: QAngle): number, number, number
```

Returns the pitch, yaw and roll of the angle.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to unpack. |


  

### `QAngle.GetForward`

```lua
QAngle.GetForward(ang: QAngle): Vector
```

Returns the forward direction of the angle as a vector with a length of 1. Only the pitch and the yaw are used.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


  

### `QAngle.GetLeftVectors`

```lua
QAngle.GetLeftVectors(ang: QAngle): Vector, Vector, Vector
```

Returns the forward, left and up directions of the angle. Each vector has a length of 1.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `QAngle.Length`

```lua
QAngle.Length(ang: QAngle): number
```

Returns the length of the angle. This is the square root of the sum of the squares of the pitch, the yaw and the roll.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to measure. |


  

### `QAngle.LengthSqr`

```lua
QAngle.LengthSqr(ang: QAngle): number
```

Returns the squared length of the angle. This is the sum of the squares of the pitch, the yaw and the roll.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to measure. |


  

### `QAngle.Negate`

```lua
QAngle.Negate(ang: QAngle)
```

Negates every component of the angle.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to negate. |


  

### `QAngle.IsValid`

```lua
QAngle.IsValid(ang: QAngle): boolean
```

Returns `true` if every component is a finite number. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to check. |


  

### `QAngle.Invalidate`

```lua
QAngle.Invalidate(ang: QAngle)
```

Sets every component of the angle to NaN.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to change. |


  

### `QAngle.NormalizePositive`

```lua
QAngle.NormalizePositive(ang: QAngle)
```

Wraps each component of the angle into the range from 0 to 360. The value 0 is included and the value 360 is not.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to normalize. |


  

### `QAngle.Clamp`

```lua
QAngle.Clamp(ang: QAngle)
```

Clamps each component of the angle to the range that the engine uses. The pitch is clamped from -89 to 89, the yaw from -180 to 180 and the roll from -90 to 90. The angle is not wrapped first, so normalize it before you clamp it.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to clamp. |


  

### `QAngle.IsEqual`

```lua
QAngle.IsEqual(ang: QAngle, other: QAngle, tolerance: number): boolean
```

Returns `true` if the difference between each component of the two angles is at most `tolerance`. Each difference is wrapped into the range from -180 to 180 first, so 179 and -179 are 2 degrees apart.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The first angle. |
| other | `QAngle` | The second angle. |
| tolerance | `number` | The largest allowed difference in degrees. |


  

### `QAngle.GetRightVectors`

```lua
QAngle.GetRightVectors(ang: QAngle): Vector, Vector, Vector
```

Returns the forward, right and up directions of the angle. Each vector has a length of 1. The right direction is the negated left direction from `GetLeftVectors`.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| right | `Vector` |  |
| up | `Vector` |  |


  

### `QAngle.GetLeftVectorsTranspose`

```lua
QAngle.GetLeftVectorsTranspose(ang: QAngle): Vector, Vector, Vector
```

Returns the rows of the rotation matrix of the angle. `GetLeftVectors` returns the columns of the same matrix. This is the transposed forward, left and up.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| left | `Vector` |  |
| up | `Vector` |  |


  

### `QAngle.GetRightVectorsTranspose`

```lua
QAngle.GetRightVectorsTranspose(ang: QAngle): Vector, Vector, Vector
```

Returns the rows of the rotation matrix of the angle, with the second row negated. This is the transposed forward, right and up.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


| Return | Type | Description |
| --- | --- | --- |
| forward | `Vector` |  |
| right | `Vector` |  |
| up | `Vector` |  |


  

### `QAngle.RotateVector`

```lua
QAngle.RotateVector(ang: QAngle, v: Vector): Vector
```

Rotates a vector by the rotation of the angle. The X component of the vector moves along the forward direction, Y moves along the left direction and Z moves along the up direction.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The rotation to apply. |
| v | `Vector` | The vector to rotate. |


  

### `QAngle.ToMatrix`

```lua
QAngle.ToMatrix(ang: QAngle): matrix3x4_t
```

Returns the rotation matrix of the angle. The origin of the matrix is `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


  

### `QAngle.ToQuaternion`

```lua
QAngle.ToQuaternion(ang: QAngle): Quaternion
```

Converts the angle to a `Quaternion`, which is aligned to 16 bytes.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |


  

### `QAngle.ToQuaternionStorage`

```lua
QAngle.ToQuaternionStorage(ang: QAngle): QuaternionStorage
```

Converts the angle to a `QuaternionStorage`, which is not aligned.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `QAngle` | The angle to convert. |
