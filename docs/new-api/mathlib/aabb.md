> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Bounding Box


## AABB\_t — cdata


An axis aligned bounding box. It is stored as a minimum corner and a maximum corner.

Trace shapes and hitbox bounds use this type. Schema fields of type `AABB_t` or `AABBWS_t`
are also read and written as this type.

The `TransformAABB`, `RotateAABB` and `RotateAndScaleAABB` methods of `matrix3x4_t`,
`CTransform` and the quaternion types take a minimum and a maximum corner. You can pass one
`AABB_t` instead of the two corners. In that case, the method also returns an `AABB_t`.

The `+` operator returns the smallest box that contains both boxes. The `==` operator
compares both corners and returns `false` when the other value is not an `AABB_t`.

```cpp lines=false
typedef struct AABB_t {
    Vector m_vMinBounds;
    Vector m_vMaxBounds;
} AABB_t;
```


  

### `AABB_t.m_vMaxBounds`

The maximum corner.


  

### `AABB_t.m_vMinBounds`

The minimum corner.


  

### `AABB_t + b`

The smallest box that contains both boxes.


| Parameter | Type | Description |
| --- | --- | --- |
| b | `AABB_t` |  |


<a id="aabb_t-1"></a>

## AABB_t  — ctype · callable


Call `AABB_t()` to create a box with both corners at `(0, 0, 0)`. Call `AABB_t(mins, maxs)`
with two vectors to set the corners. Call `AABB_t(points)` with a Lua array of points to
create the smallest box that contains all of them. If the array is empty, the box is
invalid, the same as `AABB_t.Invalid()`. Call `AABB_t(other)` to make a copy of another box.

Any other arguments throw an error.


  

<a id="aabb_t"></a>
### `AABB_t()`

```lua
AABB_t(): AABB_t
```

A box with both corners at `(0, 0, 0)`.


  

### `AABB_t(mins, maxs)`

```lua
AABB_t(mins: Vector|VectorAligned, maxs: Vector|VectorAligned): AABB_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| mins | `Vector\|VectorAligned` |  |
| maxs | `Vector\|VectorAligned` |  |


  

### `AABB_t(points)`

```lua
AABB_t(points: Vector[]): AABB_t
```

The smallest box that contains every point in a Lua array.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector[]` |  |


  

### `AABB_t(self)`

```lua
AABB_t(self: AABB_t): AABB_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `AABB_t` |  |


  

### `AABB_t.Invalid`

```lua
AABB_t.Invalid(): AABB_t
```

Returns a box that contains nothing. The minimum corner is set to `FLT_MAX` and the maximum corner is set to `-FLT_MAX` on every axis. When you add a point to this box, the box becomes that point.


  

### `AABB_t.Copy`

```lua
AABB_t.Copy(src: AABB_t, dst: AABB_t)
```

Copies one box into another box.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `AABB_t` | The box to copy from. |
| dst | `AABB_t` | The box to copy into. |


  

### `AABB_t.Init`

```lua
AABB_t.Init(box: AABB_t, mins: Vector, maxs: Vector)
```

Sets both corners of the box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| mins | `Vector` | The minimum corner. |
| maxs | `Vector` | The maximum corner. |


  

### `AABB_t.MakeInvalid`

```lua
AABB_t.MakeInvalid(box: AABB_t)
```

Changes the box so that it contains nothing. This is the same box as `AABB_t.Invalid()`.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |


  

### `AABB_t.IsInvalid`

```lua
AABB_t.IsInvalid(box: AABB_t): boolean
```

Returns `true` if the minimum is greater than the maximum on any axis.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to check. |


  

### `AABB_t.IsEmpty`

```lua
AABB_t.IsEmpty(box: AABB_t): boolean
```

Returns `true` if the size of the box is 0 or negative on any axis. This means the minimum is greater than or equal to the maximum on that axis.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to check. |


  

### `AABB_t.IsReasonable`

```lua
AABB_t.IsReasonable(box: AABB_t): boolean
```

Returns `true` if both corners pass `Vector.IsReasonable` with its default range of 1000000.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to check. |


  

### `AABB_t.GetCenter`

```lua
AABB_t.GetCenter(box: AABB_t): Vector
```

Returns the center of the box. This is the point halfway between the two corners.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.GetSize`

```lua
AABB_t.GetSize(box: AABB_t): Vector
```

Returns the size of the box on each axis. This is the maximum corner minus the minimum corner.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.GetBoundingRadius`

```lua
AABB_t.GetBoundingRadius(box: AABB_t): number
```

Returns the distance from the center of the box to a corner. A sphere with this radius around the center contains the whole box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.GetSurfaceArea`

```lua
AABB_t.GetSurfaceArea(box: AABB_t): number
```

Returns the total area of the six faces of the box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.GetVolume`

```lua
AABB_t.GetVolume(box: AABB_t): number
```

Returns the volume of the box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.Corner`

```lua
AABB_t.Corner(box: AABB_t, n: integer): Vector
```

Returns one of the eight corners of the box. Each bit of `n` chooses the minimum or the maximum value on one axis. Bit 0 chooses the maximum X, bit 1 chooses the maximum Y and bit 2 chooses the maximum Z. For example, 0 is the minimum corner and 7 is the maximum corner.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |
| n | `integer` | The index of the corner, from 0 to 7. |


  

### `AABB_t.LengthOfSmallestDimension`

```lua
AABB_t.LengthOfSmallestDimension(box: AABB_t): number
```

Returns the size of the box on its shortest axis.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.LengthOfLargestDimension`

```lua
AABB_t.LengthOfLargestDimension(box: AABB_t): number
```

Returns the size of the box on its longest axis.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |


  

### `AABB_t.AddPointToBounds`

```lua
AABB_t.AddPointToBounds(box: AABB_t, point: Vector)
```

Grows the box so that it contains a point.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| point | `Vector` | The point to include. |


  

### `AABB_t.AddSphereToBounds`

```lua
AABB_t.AddSphereToBounds(box: AABB_t, center: Vector, radius: number)
```

Grows the box so that it contains a sphere.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| center | `Vector` | The center of the sphere. |
| radius | `number` | The radius of the sphere. |


  

### `AABB_t.AddAABBToBounds`

```lua
AABB_t.AddAABBToBounds(box: AABB_t, other: AABB_t)
```

Grows the box so that it contains another box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| other | `AABB_t` | The box to include. |


  

### `AABB_t.AddAABBToBounds`

```lua
AABB_t.AddAABBToBounds(box: AABB_t, mins: Vector, maxs: Vector)
```

Grows the box so that it contains the box given by a minimum and a maximum corner.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| mins | `Vector` | The minimum corner of the box to include. |
| maxs | `Vector` | The maximum corner of the box to include. |


  

### `AABB_t.IntersectWith`

```lua
AABB_t.IntersectWith(box: AABB_t, other: AABB_t)
```

Shrinks the box to the part that it shares with another box. If the boxes do not overlap, the result is an invalid box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| other | `AABB_t` | The box to intersect with. |


  

### `AABB_t.SetToPoint`

```lua
AABB_t.SetToPoint(box: AABB_t, point: Vector)
```

Moves both corners of the box to a point, so the box has a size of 0.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| point | `Vector` | The new position of both corners. |


  

### `AABB_t.EnsureMinSize`

```lua
AABB_t.EnsureMinSize(box: AABB_t, min_size: Vector)
```

Grows the box equally on both sides of its center so that its size on each axis is at least the given size. An axis that is already large enough does not change.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| min_size | `Vector` | The smallest allowed size on each axis. |


  

### `AABB_t.Move`

```lua
AABB_t.Move(box: AABB_t, delta: Vector)
```

Moves both corners of the box by an offset.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| delta | `Vector` | The offset to add. |


  

### `AABB_t.Expand`

```lua
AABB_t.Expand(box: AABB_t, amount: number|Vector)
```

Moves both corners of the box outward. The minimum corner moves down by the amount and the maximum corner moves up by the amount. A negative amount shrinks the box.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to change. |
| amount | `number\|Vector` | A number to use on every axis, or a vector with a separate amount for each axis. |


  

### `AABB_t.GetMinDistToPoint`

```lua
AABB_t.GetMinDistToPoint(box: AABB_t, point: Vector): number
```

Returns the distance from a point to the nearest point of the box. If the point is inside the box, the distance is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |
| point | `Vector` | The point to measure from. |


  

### `AABB_t.GetMinAxialDistanceToPoint`

```lua
AABB_t.GetMinAxialDistanceToPoint(box: AABB_t, point: Vector): number
```

Measures how far a point is outside the box on each axis and returns the largest of the three values. If the point is inside the box, the result is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |
| point | `Vector` | The point to measure from. |


  

### `AABB_t.DistanceTo`

```lua
AABB_t.DistanceTo(box: AABB_t, other: AABB_t): number
```

Returns the distance between the nearest points of two boxes. If the boxes overlap, the distance is 0.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The first box. |
| other | `AABB_t` | The second box. |


  

### `AABB_t.ClosestPoint`

```lua
AABB_t.ClosestPoint(box: AABB_t, point: Vector): Vector
```

Returns the point of the box that is nearest to the given point. If the point is inside the box, the same point is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |
| point | `Vector` | The point to project. |


  

### `AABB_t.Overlaps`

```lua
AABB_t.Overlaps(box: AABB_t, other: AABB_t): boolean
```

Returns `true` if the two boxes overlap. Boxes that only touch at a face, an edge or a corner also count as overlapping.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The first box. |
| other | `AABB_t` | The second box. |


  

### `AABB_t.ContainsPoint`

```lua
AABB_t.ContainsPoint(box: AABB_t, point: Vector): boolean
```

Returns `true` if the point is inside the box or on its surface.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The box to read. |
| point | `Vector` | The point to test. |


  

### `AABB_t.Contains`

```lua
AABB_t.Contains(box: AABB_t, other: AABB_t): boolean
```

Returns `true` if the other box is completely inside this box. Shared faces are allowed.


| Parameter | Type | Description |
| --- | --- | --- |
| box | `AABB_t` | The outer box. |
| other | `AABB_t` | The inner box. |
