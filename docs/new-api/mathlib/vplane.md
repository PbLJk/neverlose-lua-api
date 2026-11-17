> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Plane


## VPlane — cdata


A plane, stored as a normal with a length of 1 and a distance along that normal. A point
`p` is on the plane when `p:Dot(m_Normal) == m_Dist`. The side that the normal points to is
the front of the plane.

The `SECONDARYVIEWMODE_PLANAR_REFLECTION` render attribute uses a plane. Both matrix types
can transform a plane with `TransformPlane`. `mathlib` can build reflection and projection
matrices from planes.

The `==` operator compares the normal and the distance and returns `false` when the other
value is not a `VPlane`.

```cpp lines=false
typedef struct VPlane {
    Vector m_Normal;
    float m_Dist;
} VPlane;
```


  

### `VPlane.m_Dist`

The distance from the origin to the plane, measured along the normal.


  

### `VPlane.m_Normal`

The normal of the plane. It should have a length of 1.


<a id="vplane-1"></a>

## VPlane  — ctype · callable


Call `VPlane()` to create a plane with every field set to 0. Call `VPlane(normal, dist)` to
set the normal and the distance. The normal is stored as given. Call `VPlane(normal, point)`
to create a plane through a point. The normal is normalized first. Call `VPlane(a, b, c)` to
create a plane through three points in clockwise order. Call `VPlane(other)` to make a copy
of another plane.

Any other arguments throw an error.


  

<a id="vplane"></a>
### `VPlane()`

```lua
VPlane(): VPlane
```

A plane with every field set to 0.


  

### `VPlane(normal, dist)`

```lua
VPlane(normal: Vector|VectorAligned, dist: number): VPlane
```


| Parameter | Type | Description |
| --- | --- | --- |
| normal | `Vector\|VectorAligned` |  |
| dist | `number` |  |


  

### `VPlane(normal, point)`

```lua
VPlane(normal: Vector|VectorAligned, point: Vector|VectorAligned): VPlane
```

The normal is normalized.


| Parameter | Type | Description |
| --- | --- | --- |
| normal | `Vector\|VectorAligned` |  |
| point | `Vector\|VectorAligned` |  |


  

### `VPlane(a, b, c)`

```lua
VPlane(a: Vector|VectorAligned, b: Vector|VectorAligned, c: Vector|VectorAligned): VPlane
```

A plane through three points in clockwise order.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector\|VectorAligned` |  |
| b | `Vector\|VectorAligned` |  |
| c | `Vector\|VectorAligned` |  |


  

### `VPlane(self)`

```lua
VPlane(self: VPlane): VPlane
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `VPlane` |  |


  

### `VPlane.Init`

```lua
VPlane.Init(plane: VPlane, normal: Vector, dist: number)
```

Sets the normal and the distance of the plane. The normal is stored as given.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to change. |
| normal | `Vector` | The normal. |
| dist | `number` | The distance along the normal. |


  

### `VPlane.InitFromPointAndNormal`

```lua
VPlane.InitFromPointAndNormal(plane: VPlane, point: Vector, normal: Vector)
```

Sets the plane so that it goes through a point. The normal is normalized first.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to change. |
| point | `Vector` | A point on the plane. |
| normal | `Vector` | The normal. |


  

### `VPlane.InitFromClockwisePoints`

```lua
VPlane.InitFromClockwisePoints(plane: VPlane, a: Vector, b: Vector, c: Vector)
```

Sets the plane so that it goes through three points. The normal is the normalized cross product of `c - a` and `b - a`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to change. |
| a | `Vector` |  |
| b | `Vector` |  |
| c | `Vector` |  |


  

### `VPlane.Copy`

```lua
VPlane.Copy(src: VPlane, dst: VPlane)
```

Copies one plane into another plane.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `VPlane` | The plane to copy from. |
| dst | `VPlane` | The plane to copy into. |


  

### `VPlane.DistTo`

```lua
VPlane.DistTo(plane: VPlane, point: Vector): number
```

Returns the signed distance from a point to the plane. The distance is positive in front of the plane and negative behind it.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to measure. |


  

### `VPlane.IntersectLineSegment`

```lua
VPlane.IntersectLineSegment(plane: VPlane, start: Vector, stop: Vector): boolean, Vector?
```

Finds the point where a segment crosses the plane. If the segment crosses the plane, this function returns `true` and the point. Otherwise it returns `false` and `nil`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| start | `Vector` | The start of the segment. |
| stop | `Vector` | The end of the segment. |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| intersection | `Vector?` |  |


    
If the segment is parallel to the plane and lies on the plane, this function returns `true`
and a copy of `start`.


  

  

### `VPlane.GetPointSide`

```lua
VPlane.GetPointSide(plane: VPlane, point: Vector[, epsilon: number]): integer
```

Returns the side of the plane that a point is on, as a `SideType` value. A point is on the plane when its distance to the plane is less than `epsilon`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to check. |
| epsilon? | `number` | The distance from the plane at which a point stops counting as `SIDE_ON`. The default is 0.01. |


  

### `VPlane.GetPointSideExact`

```lua
VPlane.GetPointSideExact(plane: VPlane, point: Vector): integer
```

Returns `SIDE_FRONT` if the point is in front of the plane. Otherwise it returns `SIDE_BACK`. A point that is exactly on the plane returns `SIDE_BACK`. This function never returns `SIDE_ON`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to check. |


  

### `VPlane.BoxOnPlaneSide`

```lua
VPlane.BoxOnPlaneSide(plane: VPlane, mins: Vector, maxs: Vector): integer
```

Returns the side of the plane that a box is on, as a `SideType` value. If the box is completely in front of the plane, it returns `SIDE_FRONT`. If it is completely behind the plane, it returns `SIDE_BACK`. If the plane cuts through the box, it returns `SIDE_ON`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


  

### `VPlane.BoxOnPlaneSide`

```lua
VPlane.BoxOnPlaneSide(plane: VPlane, bounds: AABB_t): integer
```

Returns the side of the plane that a box is on. This is the same as the version with `mins` and `maxs`, with the box given as one `AABB_t`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| bounds | `AABB_t` | The box to check. |


  

### `VPlane.PointInFront`

```lua
VPlane.PointInFront(plane: VPlane, point: Vector): boolean
```

Returns `true` if the point is in front of the plane. A point that is exactly on the plane returns `false`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to check. |


  

### `VPlane.ReflectPoint`

```lua
VPlane.ReflectPoint(plane: VPlane, point: Vector)
```

Moves a point to its mirror position on the other side of the plane. The point that you pass is changed.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to reflect. |


  

### `VPlane.ReflectDirection`

```lua
VPlane.ReflectDirection(plane: VPlane, dir: Vector)
```

Mirrors a direction across the plane. The direction that you pass is changed.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| dir | `Vector` | The direction to reflect. |


  

### `VPlane.ConvertToPlaneEquation`

```lua
VPlane.ConvertToPlaneEquation(plane: VPlane): Vector4D
```

Returns the plane as the equation `Ax + By + Cz + D = 0`. The X, Y and Z components of the result are the normal, and the W component is `-m_Dist`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |


  

### `VPlane.Flip`

```lua
VPlane.Flip(plane: VPlane): VPlane
```

Returns a new plane in the same position that faces the other way. Both the normal and the distance are negated.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |


  

### `VPlane.GetPointOnPlane`

```lua
VPlane.GetPointOnPlane(plane: VPlane): Vector
```

Returns the point of the plane that is nearest to the origin. This is `m_Normal * m_Dist`.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |


  

### `VPlane.SnapPointToPlane`

```lua
VPlane.SnapPointToPlane(plane: VPlane, point: Vector): Vector
```

Moves a point along the normal until it is on the plane, and returns the new point.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to move. |


  

### `VPlane.CalculateClosestPointOnPlane`

```lua
VPlane.CalculateClosestPointOnPlane(plane: VPlane, point: Vector): Vector
```

Returns the point of the plane that is nearest to the given point.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to read. |
| point | `Vector` | The point to project. |


  

### `VPlane.IntersectWithPlane`

```lua
VPlane.IntersectWithPlane(plane: VPlane, other: VPlane): boolean, Vector?, Vector?
```

Finds the line where two planes meet. This function returns `true` and two points on that line. If the planes are parallel, it returns `false` and `nil` for both points.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The first plane. |
| other | `VPlane` | The second plane. |


| Return | Type | Description |
| --- | --- | --- |
| ok | `boolean` |  |
| point1 | `Vector?` |  |
| point2 | `Vector?` |  |


    
The second point is the first point plus the cross product of the two normals.


  

  

### `VPlane.IsZero`

```lua
VPlane.IsZero(plane: VPlane): boolean
```

Returns `true` if the distance is exactly 0 and each component of the normal is between -1e-9 and 1e-9.


| Parameter | Type | Description |
| --- | --- | --- |
| plane | `VPlane` | The plane to check. |


## SideType — enum

The side of a plane that a point or a box is on.


### `SideType`


| Name | Value | Description |
| --- | --- | --- |
| SIDE_FRONT | 0 | In front of the plane, on the side that the normal points to. |
| SIDE_BACK | 1 | Behind the plane. |
| SIDE_ON | 2 | On the plane. |


## Frustum\_t — cdata


A view frustum with up to eight planes. The normals of the planes point into the frustum.
The planes are stored in two `fourplanes_t` groups, with four planes in each group. Each
plane uses one lane of the SIMD arrays in its group.

The `m_frustumStruct` field of the view setup has this type.
`mathlib.FrustumPlanesFromMatrix` builds a frustum from a clip to world matrix.

A lane that is not used has a normal of `(0, 0, 0)` and a distance of `-FLT_MAX`, so it never
culls anything.

```cpp lines=false
typedef struct __declspec(align(16)) fourplanes_t {
    float nX[4], nY[4], nZ[4], dist[4];
    float xSign[4], ySign[4], zSign[4];
    float nXAbs[4], nYAbs[4], nZAbs[4];
} fourplanes_t;

typedef struct __declspec(align(16)) Frustum_t {
    fourplanes_t m_Planes[2];
} Frustum_t;
```


  

### `Frustum_t.m_Planes`

An array of 2 groups. The first index is 0.


## fourplanes\_t — object type


  

### `fourplanes_t.dist`

The distance for each of the 4 lanes.


  

### `fourplanes_t.nX`

The X component of the normal for each of the 4 lanes.


  

### `fourplanes_t.nXAbs`

The absolute value of the X component of the normal for each of the 4 lanes.


  

### `fourplanes_t.nY`

The Y component of the normal for each of the 4 lanes.


  

### `fourplanes_t.nYAbs`

The absolute value of the Y component of the normal for each of the 4 lanes.


  

### `fourplanes_t.nZ`

The Z component of the normal for each of the 4 lanes.


  

### `fourplanes_t.nZAbs`

The absolute value of the Z component of the normal for each of the 4 lanes.


  

### `fourplanes_t.xSign`

For each of the 4 lanes, all bits are set when the X component of the normal is negative.


  

### `fourplanes_t.ySign`

The same as `xSign`, for the Y component.


  

### `fourplanes_t.zSign`

The same as `xSign`, for the Z component.


<a id="frustum_t-1"></a>

## Frustum_t  — ctype · callable


Call `Frustum_t()` to create a frustum with no planes, which culls nothing. Call
`Frustum_t(planes)` with a Lua array of up to eight `VPlane` values to store them in order.
Call `Frustum_t(other)` to make a copy of another frustum. Any other argument throws an
error.


  

<a id="frustum_t"></a>
### `Frustum_t()`

```lua
Frustum_t(): Frustum_t
```

A frustum with no planes, which culls nothing.


  

### `Frustum_t(planes)`

```lua
Frustum_t(planes: VPlane[]): Frustum_t
```

A frustum with up to eight planes.


| Parameter | Type | Description |
| --- | --- | --- |
| planes | `VPlane[]` |  |


  

### `Frustum_t(self)`

```lua
Frustum_t(self: Frustum_t): Frustum_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Frustum_t` |  |


  

### `Frustum_t.SetPlane`

```lua
Frustum_t.SetPlane(frustum: Frustum_t, index: integer, plane: VPlane)
```

Stores a plane at an index and updates its sign and absolute value lanes. Indexes 0 to 3 are in the first group, and indexes 4 to 7 are in the second group.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to change. |
| index | `integer` | The index of the plane, from 0 to 7. |
| plane | `VPlane` | The plane to store. |


  

### `Frustum_t.GetPlane`

```lua
Frustum_t.GetPlane(frustum: Frustum_t, index: integer): VPlane
```

Returns the plane at an index.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to read. |
| index | `integer` | The index of the plane, from 0 to 7. |


  

### `Frustum_t.SetPlanes`

```lua
Frustum_t.SetPlanes(frustum: Frustum_t, planes: VPlane[])
```

Removes every plane, then stores the planes of a Lua array in order, starting at index 0.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to change. |
| planes | `VPlane[]` | Up to eight planes. |


  

### `Frustum_t.GetPlanes`

```lua
Frustum_t.GetPlanes(frustum: Frustum_t[, count: integer]): VPlane[]
```

Returns the first `count` planes as a Lua array.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to read. |
| count? | `integer` | The number of planes, from 0 to 8. The default is 6. |


  

### `Frustum_t.Clear`

```lua
Frustum_t.Clear(frustum: Frustum_t)
```

Removes every plane, so the frustum culls nothing.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to change. |


  

### `Frustum_t.CullPoint`

```lua
Frustum_t.CullPoint(frustum: Frustum_t, point: Vector): boolean
```

Returns `true` if the point is behind any plane of the frustum. A point that is exactly on a plane is not culled.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to read. |
| point | `Vector` | The point to test. |


  

### `Frustum_t.CullBox`

```lua
Frustum_t.CullBox(frustum: Frustum_t, mins: Vector, maxs: Vector): boolean
```

Returns `true` if the box is completely behind any plane of the frustum.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to read. |
| mins | `Vector` | The minimum corner of the box. |
| maxs | `Vector` | The maximum corner of the box. |


  

### `Frustum_t.CullBox`

```lua
Frustum_t.CullBox(frustum: Frustum_t, bounds: AABB_t): boolean
```

Returns `true` if the box is completely behind any plane of the frustum. This is the same as the version with `mins` and `maxs`, with the box given as one `AABB_t`.


| Parameter | Type | Description |
| --- | --- | --- |
| frustum | `Frustum_t` | The frustum to read. |
| bounds | `AABB_t` | The box to test. |
