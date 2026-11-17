> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Euler Angles


## RadianEuler — cdata


Euler angles in radians. Each component is a rotation around one axis. `x` rotates around
the X axis, which is the roll. `y` rotates around the Y axis, which is the pitch. `z` rotates
around the Z axis, which is the yaw.

A `QAngle` stores the same rotation in degrees and in a different order, which is pitch,
yaw and roll. When you convert to a `QAngle`, both the units and the order change. Animation
and particle schema fields use this type.

The `==` operator compares every component and returns `false` when the other value is not
a `RadianEuler`.

```cpp lines=false
typedef struct RadianEuler {
    float x, y, z;
} RadianEuler;
```


  

### `RadianEuler.x`

The rotation around the X axis in radians. This is the roll.


  

### `RadianEuler.y`

The rotation around the Y axis in radians. This is the pitch.


  

### `RadianEuler.z`

The rotation around the Z axis in radians. This is the yaw.


<a id="radianeuler-1"></a>

## RadianEuler  — ctype · callable


Call `RadianEuler()` to create angles with every component set to 0. Call
`RadianEuler(x, y, z)` to set the components. A component that is not given is set to 0.

You can also pass a `QAngle`, a `Quaternion`, a `QuaternionStorage` or a `DegreeEuler` to
convert the same rotation. Pass another `RadianEuler` to make a copy. Any other first
argument throws an error.


  

<a id="radianeuler"></a>
### `RadianEuler()`

```lua
RadianEuler(): RadianEuler
```

Angles with every component set to 0.


  

### `RadianEuler(x, y, z)`

```lua
RadianEuler(x: number[, y: number, z: number]): RadianEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |


  

### `RadianEuler(angles)`

```lua
RadianEuler(angles: QAngle): RadianEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `RadianEuler(q)`

```lua
RadianEuler(q: Quaternion|QuaternionStorage): RadianEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


  

### `RadianEuler(angles)`

```lua
RadianEuler(angles: DegreeEuler): RadianEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `DegreeEuler` |  |


  

### `RadianEuler(self)`

```lua
RadianEuler(self: RadianEuler): RadianEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `RadianEuler` |  |


  

### `RadianEuler.Unpack`

```lua
RadianEuler.Unpack(e: RadianEuler): number, number, number
```

Returns the X, Y and Z components.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |


  

### `RadianEuler.Copy`

```lua
RadianEuler.Copy(src: RadianEuler, dst: RadianEuler)
```

Copies the components of one value into another value.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `RadianEuler` | The value to copy from. |
| dst | `RadianEuler` | The value to copy into. |


  

### `RadianEuler.Init`

```lua
RadianEuler.Init(e: RadianEuler[, x: number, y: number, z: number])
```

Sets the components. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The value to change. |
| x? | `number` | The rotation around the X axis in radians. |
| y? | `number` | The rotation around the Y axis in radians. |
| z? | `number` | The rotation around the Z axis in radians. |


  

### `RadianEuler.IsValid`

```lua
RadianEuler.IsValid(e: RadianEuler): boolean
```

Returns `true` if every component is a finite number. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The value to check. |


  

### `RadianEuler.Invalidate`

```lua
RadianEuler.Invalidate(e: RadianEuler)
```

Sets every component to NaN.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The value to change. |


  

### `RadianEuler.ToQAngle`

```lua
RadianEuler.ToQAngle(e: RadianEuler): QAngle
```

Converts the angles to a `QAngle` in degrees. The pitch comes from `y`, the yaw comes from `z` and the roll comes from `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to convert. |


  

### `RadianEuler.ToQuaternion`

```lua
RadianEuler.ToQuaternion(e: RadianEuler): Quaternion
```

Converts the angles to a `Quaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to convert. |


  

### `RadianEuler.RotateVector`

```lua
RadianEuler.RotateVector(e: RadianEuler, v: Vector): Vector
```

Rotates a vector by these angles. The result is the same as `QAngle.RotateVector` with the converted angle.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The rotation to apply. |
| v | `Vector` | The vector to rotate. |


  

### `RadianEuler.Pitch`

```lua
RadianEuler.Pitch(e: RadianEuler): number
```

Returns the pitch in radians. This is the `y` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to read. |


  

### `RadianEuler.Yaw`

```lua
RadianEuler.Yaw(e: RadianEuler): number
```

Returns the yaw in radians. This is the `z` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to read. |


  

### `RadianEuler.Roll`

```lua
RadianEuler.Roll(e: RadianEuler): number
```

Returns the roll in radians. This is the `x` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `RadianEuler` | The angles to read. |


## DegreeEuler — cdata


Euler angles in degrees. The components have the same order as in `RadianEuler`. `x`
rotates around the X axis, which is the roll. `y` rotates around the Y axis, which is the
pitch. `z` rotates around the Z axis, which is the yaw.

This means that `QAngle(p, y, r)` and `DegreeEuler(r, p, y)` are the same rotation.

The `==` operator compares every component and returns `false` when the other value is not
a `DegreeEuler`.

```cpp lines=false
typedef struct DegreeEuler {
    float x, y, z;
} DegreeEuler;
```


  

### `DegreeEuler.x`

The rotation around the X axis in degrees. This is the roll.


  

### `DegreeEuler.y`

The rotation around the Y axis in degrees. This is the pitch.


  

### `DegreeEuler.z`

The rotation around the Z axis in degrees. This is the yaw.


<a id="degreeeuler-1"></a>

## DegreeEuler  — ctype · callable


Call `DegreeEuler()` to create angles with every component set to 0. Call
`DegreeEuler(x, y, z)` to set the components. A component that is not given is set to 0.

You can also pass a `QAngle`, a `Quaternion`, a `QuaternionStorage` or a `RadianEuler` to
convert the same rotation. Pass another `DegreeEuler` to make a copy. Any other first
argument throws an error.


  

<a id="degreeeuler"></a>
### `DegreeEuler()`

```lua
DegreeEuler(): DegreeEuler
```

Angles with every component set to 0.


  

### `DegreeEuler(x, y, z)`

```lua
DegreeEuler(x: number[, y: number, z: number]): DegreeEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |


  

### `DegreeEuler(angles)`

```lua
DegreeEuler(angles: QAngle): DegreeEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` |  |


  

### `DegreeEuler(q)`

```lua
DegreeEuler(q: Quaternion|QuaternionStorage): DegreeEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| q | `Quaternion\|QuaternionStorage` |  |


  

### `DegreeEuler(angles)`

```lua
DegreeEuler(angles: RadianEuler): DegreeEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `RadianEuler` |  |


  

### `DegreeEuler(self)`

```lua
DegreeEuler(self: DegreeEuler): DegreeEuler
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `DegreeEuler` |  |


  

### `DegreeEuler.Unpack`

```lua
DegreeEuler.Unpack(e: DegreeEuler): number, number, number
```

Returns the X, Y and Z components.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y | `number` |  |
| z | `number` |  |


  

### `DegreeEuler.Copy`

```lua
DegreeEuler.Copy(src: DegreeEuler, dst: DegreeEuler)
```

Copies the components of one value into another value.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `DegreeEuler` | The value to copy from. |
| dst | `DegreeEuler` | The value to copy into. |


  

### `DegreeEuler.Init`

```lua
DegreeEuler.Init(e: DegreeEuler[, x: number, y: number, z: number])
```

Sets the components. A component that is not given is set to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The value to change. |
| x? | `number` | The rotation around the X axis in degrees. |
| y? | `number` | The rotation around the Y axis in degrees. |
| z? | `number` | The rotation around the Z axis in degrees. |


  

### `DegreeEuler.IsValid`

```lua
DegreeEuler.IsValid(e: DegreeEuler): boolean
```

Returns `true` if every component is a finite number. NaN and infinity are not finite.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The value to check. |


  

### `DegreeEuler.Invalidate`

```lua
DegreeEuler.Invalidate(e: DegreeEuler)
```

Sets every component to NaN.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The value to change. |


  

### `DegreeEuler.ToQAngle`

```lua
DegreeEuler.ToQAngle(e: DegreeEuler): QAngle
```

Converts the angles to a `QAngle`. The pitch comes from `y`, the yaw comes from `z` and the roll comes from `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to convert. |


  

### `DegreeEuler.ToQuaternion`

```lua
DegreeEuler.ToQuaternion(e: DegreeEuler): Quaternion
```

Converts the angles to a `Quaternion`.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to convert. |


  

### `DegreeEuler.RotateVector`

```lua
DegreeEuler.RotateVector(e: DegreeEuler, v: Vector): Vector
```

Rotates a vector by these angles. The result is the same as `QAngle.RotateVector` with the converted angle.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The rotation to apply. |
| v | `Vector` | The vector to rotate. |


  

### `DegreeEuler.Pitch`

```lua
DegreeEuler.Pitch(e: DegreeEuler): number
```

Returns the pitch in degrees. This is the `y` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to read. |


  

### `DegreeEuler.Yaw`

```lua
DegreeEuler.Yaw(e: DegreeEuler): number
```

Returns the yaw in degrees. This is the `z` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to read. |


  

### `DegreeEuler.Roll`

```lua
DegreeEuler.Roll(e: DegreeEuler): number
```

Returns the roll in degrees. This is the `x` component.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `DegreeEuler` | The angles to read. |


## RotationVector — cdata


A rotation stored as one vector. The direction of the vector is the axis of the rotation.
The length of the vector is the angle of the rotation in degrees. This is also called an
exponential map. Angular velocities use this type, for example in
`mathlib.CalcAngularVelocity` and in the quaternion version of `mathlib.SmoothDamp`.

You can call every `Vector` method on a `RotationVector`. `Normalized`, `NormalizedSafe` and
`Scaled` return a `RotationVector`. Other `Vector` methods that create a new vector return a
`Vector`.

The `+`, `-`, `*` and `/` operators take a `RotationVector` or a `Vector` on the right side
and return a `RotationVector`. The `*` and `/` operators also take a number. The unary `-`
operator returns a negated copy, and the `#` operator returns the length. The `==` operator
compares every component and returns `false` when the other value is not a
`RotationVector`.

```cpp lines=false
typedef struct RotationVector {
    float x, y, z;
} RotationVector;
```


  

### `RotationVector + b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|RotationVector` |  |


  

### `RotationVector - b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|RotationVector` |  |


  

### `RotationVector * b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|RotationVector\|number` |  |


  

### `RotationVector / b`


| Parameter | Type | Description |
| --- | --- | --- |
| b | `Vector\|RotationVector\|number` |  |


  

<a id="rotationvector"></a>
### `-RotationVector`


  

<a id="rotationvector"></a>
### `#RotationVector`


<a id="rotationvector-1"></a>

## RotationVector  — ctype · callable


Call `RotationVector()` to create a value with every component set to 0. Call
`RotationVector(x, y, z)` to set the components. A component that is not given is set to 0.
Call `RotationVector(v)` with a `Vector` or a `VectorAligned` to copy its X, Y and Z. Call
`RotationVector(other)` to make a copy of another `RotationVector`. Any other first argument
throws an error.

The constant values below cannot be changed.


  

<a id="rotationvector"></a>
### `RotationVector()`

```lua
RotationVector(): RotationVector
```


  

### `RotationVector(x, y, z)`

```lua
RotationVector(x: number[, y: number, z: number]): RotationVector
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` |  |
| y? | `number` |  |
| z? | `number` |  |


  

### `RotationVector(v)`

```lua
RotationVector(v: Vector|VectorAligned): RotationVector
```


| Parameter | Type | Description |
| --- | --- | --- |
| v | `Vector\|VectorAligned` |  |


  

### `RotationVector(self)`

```lua
RotationVector(self: RotationVector): RotationVector
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `RotationVector` |  |


  

### `RotationVector.vOne`

The value `(1, 1, 1)`.


  

### `RotationVector.vXAxis`

The value `(1, 0, 0)`.


  

### `RotationVector.vYAxis`

The value `(0, 1, 0)`.


  

### `RotationVector.vZAxis`

The value `(0, 0, 1)`.


  

### `RotationVector.vZero`

The value `(0, 0, 0)`.


  

### `RotationVector.FromVector`

```lua
RotationVector.FromVector(rv: RotationVector, v: Vector)
```

Copies the components of a vector into this value.


| Parameter | Type | Description |
| --- | --- | --- |
| rv | `RotationVector` | The value to change. |
| v | `Vector` | The vector to copy from. |


  

### `RotationVector.Copy`

```lua
RotationVector.Copy(src: RotationVector, dst: RotationVector)
```

Copies the components of one value into another value.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `RotationVector` | The value to copy from. |
| dst | `RotationVector` | The value to copy into. |


  

### `RotationVector.Normalized`

```lua
RotationVector.Normalized(rv: RotationVector): RotationVector
```

Returns a normalized copy. If the length is 0, the copy is `(0, 0, 0)`.


| Parameter | Type | Description |
| --- | --- | --- |
| rv | `RotationVector` | The value to normalize. |


  

### `RotationVector.NormalizedSafe`

```lua
RotationVector.NormalizedSafe(rv: RotationVector, fallback: Vector): RotationVector
```

Returns a normalized copy. If the length is 0, a new `RotationVector` with the components of `fallback` is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| rv | `RotationVector` | The value to normalize. |
| fallback | `Vector` | The value to use when the length is 0. |


  

### `RotationVector.Scaled`

```lua
RotationVector.Scaled(rv: RotationVector, scalar: number): RotationVector
```

Returns a copy with every component multiplied by a number.


| Parameter | Type | Description |
| --- | --- | --- |
| rv | `RotationVector` | The value to scale. |
| scalar | `number` | The number to multiply each component by. |
