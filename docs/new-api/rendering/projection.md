> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Projection


<a id="projection-1"></a>

## projection  — global table


Converts positions in the world to positions on the screen. The functions use the current
projection of the engine and the current render size.

Pixel coordinates start at the top left corner of the screen, and y increases downward. The
functions that take world positions use the first split screen slot, which is slot `0`.

All functions except `Matrix` return new values that you can keep and change. If a function
can return **nil**, it returns **nil** when the engine data that it needs is not available.

Call these functions from a render callback, when the render size is valid. Functions that take
world positions also need an active camera.


  

<a id="projectionellipse"></a>
### `projection.Ellipse`


  

<a id="projectionrect"></a>
### `projection.Rect`


  

### `projection.Matrix`

```lua
projection.Matrix([slot: integer]): VMatrix?
```

Returns a reference to the projection matrix of the engine for a split screen slot. You can change the matrix through the reference. When the engine updates the matrix, the values that you read change too. Throws an error if the slot is out of range. Returns **nil** if the projection matrices are not available.


| Parameter | Type | Description |
| --- | --- | --- |
| slot? | `integer` | An integer from `0` to `3`. The default is `0`. |


    


**Warning:** 
If you write to the reference, you change the projection matrix of the engine, and this changes
the rendering. Use the reference only while the engine memory is valid. Use `VMatrix(matrix)`
to make a separate copy.


  

  

### `projection.WorldToClip`

```lua
projection.WorldToClip(pos: Vector): Vector4D?
```

Converts a world position to homogeneous clip coordinates. The result is not divided by w.


| Parameter | Type | Description |
| --- | --- | --- |
| pos | `Vector` | The position in the world. |


  

### `projection.ClipToScreen`

```lua
projection.ClipToScreen(clip: Vector4D): Vector2D?
```

Converts homogeneous clip coordinates to pixels. x and y are divided by w. If w is less than `0.0001`, `0.0001` is used in its place.


| Parameter | Type | Description |
| --- | --- | --- |
| clip | `Vector4D` | The homogeneous clip coordinates. |


    
z is ignored. Points outside the viewport and points with a w of zero or less are also
converted. This function uses only the current render size. It returns **nil** only if the
render size is not available.


  

  

### `projection.WorldToScreen`

```lua
projection.WorldToScreen(pos: Vector): Vector2D?
```

Converts a world position to pixels. Returns **nil** if clip w is `0.0001` or less.


| Parameter | Type | Description |
| --- | --- | --- |
| pos | `Vector` | The position in the world. |


    
Points outside the viewport are also converted, and clip z is not checked. To find out whether
the point is on the screen, compare the result with `engine.GetScreenSize`.


  

  

### `projection.WorldToScreenRounded`

```lua
projection.WorldToScreenRounded(pos: Vector): Vector2D?
```

The same as `WorldToScreen`, but each pixel coordinate is rounded down. Negative values are also rounded down.


| Parameter | Type | Description |
| --- | --- | --- |
| pos | `Vector` | The position in the world. |


  

### `projection.Ellipsoid`

```lua
projection.Ellipsoid(center: Vector, radii: Vector): ProjectionRect?
```

Returns the bounds on the screen of the outline of an ellipsoid. The axes of the ellipsoid are aligned with the axes of the world.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector` | The center in world space. |
| radii | `Vector` | The radii in world space along the x, y and z axes. |


    
Returns **nil** if the outline is not finite or is not in front of the camera. This includes
shapes that cross the plane of the camera. The bounds can go past the edges of the viewport.


  

  

### `projection.EllipsoidClipped`

```lua
projection.EllipsoidClipped(center: Vector, radii: Vector): ProjectionRect?
```

The same as `Ellipsoid`, with one difference. If the outline is not finite or is not in front of the camera, this function returns the bounds of the part of the ellipsoid where clip w is greater than `0.0001`. It returns **nil** only if no such part exists. The bounds are not limited to the viewport.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector` | The center in world space. |
| radii | `Vector` | The radii in world space along the x, y and z axes. |


  

### `projection.Sphere`

```lua
projection.Sphere(center: Vector, radius: number): ProjectionRect?
```

The same as `Ellipsoid`, with the same radius on all three world axes.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector` | The center in world space. |
| radius | `number` | The radius in world space. |


  

### `projection.EllipsoidEllipse`

```lua
projection.EllipsoidEllipse(center: Vector, radii: Vector): ProjectionEllipse?
```

Returns the full ellipse that an ellipsoid makes on the screen. The axes of the ellipsoid are aligned with the axes of the world. This function returns **nil** in the same cases as `Ellipsoid`. Because of perspective, the center of the ellipse can be at a different place from `WorldToScreen(center)`.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector` | The center in world space. |
| radii | `Vector` | The radii in world space along the x, y and z axes. |


  

### `projection.SphereEllipse`

```lua
projection.SphereEllipse(center: Vector, radius: number): ProjectionEllipse?
```

The same as `EllipsoidEllipse`, with the same radius on all three world axes.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector` | The center in world space. |
| radius | `number` | The radius in world space. |


  

### `projection.Camera`

```lua
projection.Camera(): CTransform?
```

Returns the position and orientation of the camera, calculated from the current projection matrix. The returned transform has a scale of `1`. Returns **nil** if the length of a camera axis in the matrix is `0.0001` or less.


  

### `projection.ClipLineToScreen`

```lua
projection.ClipLineToScreen(start: Vector, finish: Vector): Vector2D?, Vector2D?
```

Cuts a line segment in world space to the part where clip z is `0` or greater. Then converts its end points to pixels and returns them in their original order. Returns **nil** if clip z is negative at both end points.


| Parameter | Type | Description |
| --- | --- | --- |
| start | `Vector` | The start of the line in world space. |
| finish | `Vector` | The end of the line in world space. |


| Return | Type | Description |
| --- | --- | --- |
| start_pixel | `Vector2D?` |  |
| end_pixel | `Vector2D?` |  |


    
The conversion divides by w. If w is less than `0.0001`, `0.0001` is used in its place. The end
points that are returned can be outside the viewport.


  


## ProjectionRect — cdata


A rectangle on the screen, with floating point bounds in pixels.


  

### `ProjectionRect.m_vMaxBounds`

The maximum x and y.


  

### `ProjectionRect.m_vMinBounds`

The minimum x and y.


## ProjectionEllipse — cdata


The ellipse that the outline of a shape makes on the screen, in pixels. The radii are the
lengths of the half axes.


  

### `ProjectionEllipse.center`

The center on the screen.


  

### `ProjectionEllipse.radius_major`

The length of the long half axis.


  

### `ProjectionEllipse.radius_minor`

The length of the short half axis.


  

### `ProjectionEllipse.rotation`

The rotation of the long axis in radians, in screen coordinates.


<a id="projectionrect-1"></a>

## projection.Rect  — ctype · callable


  

<a id="projectionrect"></a>
### `projection.Rect()`

```lua
projection.Rect(): ProjectionRect
```

All bounds are zero.


  

### `projection.Rect(min_bounds, max_bounds)`

```lua
projection.Rect(min_bounds: Vector2D, max_bounds: Vector2D): ProjectionRect
```


| Parameter | Type | Description |
| --- | --- | --- |
| min_bounds | `Vector2D` |  |
| max_bounds | `Vector2D` |  |


  

### `projection.Rect(rect)`

```lua
projection.Rect(rect: ProjectionRect): ProjectionRect
```

A separate copy.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `ProjectionRect` |  |


<a id="projectionellipse-1"></a>

## projection.Ellipse  — ctype · callable


  

<a id="projectionellipse"></a>
### `projection.Ellipse()`

```lua
projection.Ellipse(): ProjectionEllipse
```

All values are zero.


  

### `projection.Ellipse(center, radius_major, radius_minor, rotation)`

```lua
projection.Ellipse(center: Vector2D, radius_major: number, radius_minor: number, rotation: number): ProjectionEllipse
```


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` |  |
| radius_major | `number` |  |
| radius_minor | `number` |  |
| rotation | `number` |  |


  

### `projection.Ellipse(ellipse)`

```lua
projection.Ellipse(ellipse: ProjectionEllipse): ProjectionEllipse
```

A separate copy.


| Parameter | Type | Description |
| --- | --- | --- |
| ellipse | `ProjectionEllipse` |  |
