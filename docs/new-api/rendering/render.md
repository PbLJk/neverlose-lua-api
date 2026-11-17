> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Render


<a id="render-1"></a>

## render  — global table


Draws shapes, images and text on the screen.

Call the drawing functions only inside the `render` event. If you call one anywhere else, it
throws an error. Coordinates are in screen pixels. The point `Vector2D(0, 0)` is the top left
corner of the screen.


  

### `render.DrawLine`

```lua
render.DrawLine(startpos: Vector2D, endpos: Vector2D, color: Color[, thickness: number])
```

Draws a straight line between two points.


| Parameter | Type | Description |
| --- | --- | --- |
| startpos | `Vector2D` | The start point. |
| endpos | `Vector2D` | The end point. |
| color | `Color` | The colour of the line. |
| thickness? | `number` | The thickness of the line in pixels. Defaults to `1`. |


  

### `render.DrawBezier`

```lua
render.DrawBezier(a: Vector2D, b: Vector2D, c: Vector2D, d: Vector2D, color: Color, thickness: number[, segments: integer])
```

Draws a cubic Bézier curve through four control points. The curve starts at `a` and ends at `d`.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Vector2D` | The first control point, where the curve starts. |
| b | `Vector2D` | The second control point. |
| c | `Vector2D` | The third control point. |
| d | `Vector2D` | The fourth control point, where the curve ends. |
| color | `Color` | The colour of the curve. |
| thickness | `number` | The thickness of the curve in pixels. |
| segments? | `integer` | The number of straight line segments used to draw the curve. Pass `0` or `nil` to choose the number automatically. A value above `512` is treated as `512`, and a value below `0` is treated as `0`. Defaults to `0`. |


  

### `render.DrawRect`

```lua
render.DrawRect(position: Vector2D, size: Vector2D, color: Color[, rounding: render.Rounding])
```

Draws a filled rectangle from `position` to `position + size`.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| color | `Color` | The fill colour. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |


  

### `render.DrawRectOutline`

```lua
render.DrawRectOutline(position: Vector2D, size: Vector2D, color: Color[, thickness: number], rounding: render.Rounding)
```

Draws the outline of a rectangle from `position` to `position + size`.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| color | `Color` | The colour of the outline. |
| thickness? | `number` | The thickness of the outline in pixels. Defaults to `1`. |
| rounding | `render.Rounding` | The corner radius in pixels. |


  

### `render.DrawRectShadow`

```lua
render.DrawRectShadow(position: Vector2D, size: Vector2D, color: Color[, rounding: render.Rounding, shadow_size: number, offset: Vector2D])
```

Draws a soft shadow around a rectangle. The rectangle itself is not drawn.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner of the rectangle. |
| size | `Vector2D` | The width and height in pixels. |
| color | `Color` | The colour of the shadow. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |
| shadow_size? | `number` | The blur radius of the shadow in pixels. Defaults to `0`. |
| offset? | `Vector2D` | How far the shadow is moved from the rectangle. Defaults to `Vector2D(0, 0)`. |


  

### `render.DrawRectGradient`

```lua
render.DrawRectGradient(position: Vector2D, size: Vector2D, top_left: Color, top_right: Color, bottom_left: Color, bottom_right: Color[, rounding: render.Rounding])
```

Draws a filled rectangle with a different colour at each corner. The colours blend smoothly across the rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| top_left | `Color` | The colour at the top left corner. |
| top_right | `Color` | The colour at the top right corner. |
| bottom_left | `Color` | The colour at the bottom left corner. |
| bottom_right | `Color` | The colour at the bottom right corner. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |


  

### `render.DrawRectGlow`

```lua
render.DrawRectGlow(position: Vector2D, size: Vector2D, color: Color[, rounding: render.Rounding])
```

Draws a glow along the border of a rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| color | `Color` | The colour of the glow. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |


    
This function uses one radius for all four corners. If you pass an array for `rounding`, only
its first value is used.


  

  

### `render.DrawWindow`

```lua
render.DrawWindow(position: Vector2D, size: Vector2D[, rounding: render.Rounding, shadow: number, alpha: number])
```

Draws a transparent window background with a frosted look and a shadow. It looks the same as the windows of the cheat menu.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |
| shadow? | `number` | The size of the shadow. Defaults to `10` multiplied by the DPI scale of the menu. |
| alpha? | `number` | The opacity of the background, from `0` to `1`. Defaults to `1`. |


    
This function uses one radius for all four corners. If you pass an array for `rounding`, only
its first value is used.


  

  

### `render.DrawWindowShadow`

```lua
render.DrawWindowShadow(position: Vector2D, size: Vector2D[, rounding: render.Rounding])
```

Draws the shadow that the windows of the menu use, for a rectangle with the given position and size. The colour, size and offset of the shadow come from the current menu style.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |


    
This function uses one radius for all four corners. If you pass an array for `rounding`, only
its first value is used.


  

  

### `render.DrawCircle`

```lua
render.DrawCircle(center: Vector2D, color: Color, radius: number[, start_degrees: number, percentage: number])
```

Draws a filled circle. Pass `percentage` to draw only a part of the circle, like a slice of a pie.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| color | `Color` | The fill colour. |
| radius | `number` | The radius in pixels. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to draw, from `0` to `1`. Defaults to `1`. |


  

### `render.DrawCircleOutline`

```lua
render.DrawCircleOutline(center: Vector2D, color: Color, radius: number[, start_degrees: number, percentage: number, thickness: number])
```

Draws the outline of a circle. Pass `percentage` to draw only a part of the circle, like a slice of a pie.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| color | `Color` | The colour of the outline. |
| radius | `number` | The radius in pixels. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to draw, from `0` to `1`. Defaults to `1`. |
| thickness? | `number` | The thickness of the outline in pixels. Defaults to `1`. |


  

### `render.DrawCircleGradient`

```lua
render.DrawCircleGradient(center: Vector2D, outer: Color, inner: Color, radius: number[, gradient: number, start_degrees: number, percentage: number])
```

Draws a filled circle whose colour changes from `outer` at the edge to `inner` at the center.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| outer | `Color` | The colour at the edge. |
| inner | `Color` | The colour at the center. |
| radius | `number` | The radius in pixels. |
| gradient? | `number` | How strongly the two colours blend. Defaults to `1`. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to draw, from `0` to `1`. Defaults to `1`. |


  

### `render.DrawEllipse`

```lua
render.DrawEllipse(center: Vector2D, color: Color, radius_major: number, radius_minor: number[, rotation: number])
```

Draws a filled ellipse.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| color | `Color` | The fill colour. |
| radius_major | `number` | The radius along the direction of `rotation`, in pixels. |
| radius_minor | `number` | The radius at a right angle to `rotation`, in pixels. |
| rotation? | `number` | The angle of the major axis in degrees. Defaults to `0`. |


  

### `render.DrawEllipseOutline`

```lua
render.DrawEllipseOutline(center: Vector2D, color: Color, radius_major: number, radius_minor: number[, rotation: number, thickness: number])
```

Draws the outline of an ellipse.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| color | `Color` | The colour of the outline. |
| radius_major | `number` | The radius along the direction of `rotation`, in pixels. |
| radius_minor | `number` | The radius at a right angle to `rotation`, in pixels. |
| rotation? | `number` | The angle of the major axis in degrees. Defaults to `0`. |
| thickness? | `number` | The thickness of the outline in pixels. Defaults to `1`. |


  

### `render.DrawEllipseGradient`

```lua
render.DrawEllipseGradient(center: Vector2D, outer: Color, inner: Color, radius_major: number, radius_minor: number[, rotation: number, gradient: number])
```

Draws a filled ellipse whose colour changes from `outer` at the edge to `inner` at the center.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| outer | `Color` | The colour at the edge. |
| inner | `Color` | The colour at the center. |
| radius_major | `number` | The radius along the direction of `rotation`, in pixels. |
| radius_minor | `number` | The radius at a right angle to `rotation`, in pixels. |
| rotation? | `number` | The angle of the major axis in degrees. Defaults to `0`. |
| gradient? | `number` | How strongly the two colours blend. Defaults to `1`. |


  

### `render.DrawCircleBlur`

```lua
render.DrawCircleBlur(center: Vector2D, alpha: number, radius: number[, start_degrees: number, percentage: number])
```

Blurs everything behind a circular area of the screen.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point. |
| alpha | `number` | The opacity of the blur, from `0` to `1`. |
| radius | `number` | The radius in pixels. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to blur, from `0` to `1`. Defaults to `1`. |


  

### `render.DrawCircleShadow`

```lua
render.DrawCircleShadow(center: Vector2D, color: Color, radius: number, size: number[, start_degrees: number, percentage: number, offset: Vector2D])
```

Draws a soft shadow around a circle. The circle itself is not drawn.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center point of the circle. |
| color | `Color` | The colour of the shadow. |
| radius | `number` | The radius of the circle in pixels. |
| size | `number` | The blur radius of the shadow in pixels. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to use, from `0` to `1`. Defaults to `1`. |
| offset? | `Vector2D` | How far the shadow is moved from the circle. Defaults to `Vector2D(0, 0)`. |


  

### `render.DrawTriangle`

```lua
render.DrawTriangle(p1: Vector2D, p2: Vector2D, p3: Vector2D, color: Color)
```

Draws a filled triangle.


| Parameter | Type | Description |
| --- | --- | --- |
| p1 | `Vector2D` | The first corner. |
| p2 | `Vector2D` | The second corner. |
| p3 | `Vector2D` | The third corner. |
| color | `Color` | The fill colour. |


  

### `render.DrawTriangleOutline`

```lua
render.DrawTriangleOutline(p1: Vector2D, p2: Vector2D, p3: Vector2D, color: Color[, thickness: number])
```

Draws the outline of a triangle.


| Parameter | Type | Description |
| --- | --- | --- |
| p1 | `Vector2D` | The first corner. |
| p2 | `Vector2D` | The second corner. |
| p3 | `Vector2D` | The third corner. |
| color | `Color` | The colour of the outline. |
| thickness? | `number` | The thickness of the outline in pixels. Defaults to `1`. |


  

### `render.DrawPoly`

```lua
render.DrawPoly(points: Vector2D[], color: Color)
```

Draws a filled convex polygon. List the corners in order around the edge of the polygon.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector2D[]` | The corners of the polygon in order. You can pass at most 16000 points. More points throw an error. |
| color | `Color` | The fill colour. |


  

### `render.DrawPolyline`

```lua
render.DrawPolyline(points: Vector2D[], color: Color, closed: boolean, thickness: number)
```

Draws lines that connect the given points one after another.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector2D[]` | The points in order. You can pass at most 16000 points. More points throw an error. |
| color | `Color` | The colour of the lines. |
| closed | `boolean` | If `true`, a line also connects the last point to the first point. |
| thickness | `number` | The thickness of the lines in pixels. |


  

### `render.DrawPolyGradient`

```lua
render.DrawPolyGradient([center: Vector2D], points: Vector2D[], outer: Color, inner: Color[, offset: number])
```

Draws a filled convex polygon whose colour changes from `outer` at the edges to `inner` at `center`. A polygon with fewer than three points is not drawn.


| Parameter | Type | Description |
| --- | --- | --- |
| center? | `Vector2D` | The point where the colour is `inner`. Defaults to the average position of all points. |
| points | `Vector2D[]` | The corners of the polygon in order. You can pass at most 16000 points. More points throw an error. |
| outer | `Color` | The colour at the edges. |
| inner | `Color` | The colour at the center. |
| offset? | `number` | How strongly the two colours blend, from `0` to `1`. Values outside this range are clamped. Defaults to `1`. |


  

### `render.DrawPolyShadow`

```lua
render.DrawPolyShadow(points: Vector2D[], color: Color, thickness: number[, offset: Vector2D])
```

Draws a soft glow around a convex polygon. The polygon itself is not drawn. Use `render.DrawPoly` if you also want to fill it.


| Parameter | Type | Description |
| --- | --- | --- |
| points | `Vector2D[]` | The corners of the polygon in order. You can pass at most 1985 points. More points throw an error. |
| color | `Color` | The colour of the glow. It fades to transparent over `thickness`. |
| thickness | `number` | How far the glow reaches out from the polygon, in pixels. |
| offset? | `Vector2D` | How far the whole glow is moved. Defaults to `Vector2D(0, 0)`. |


  

### `render.DrawImage`

```lua
render.DrawImage(image: Image, position: Vector2D[, size: Vector2D, color: Color, mode: render.ImageMode, rounding: render.Rounding])
```

Draws an image. An image that is not loaded yet, or an empty image such as the avatar of a user who has no avatar, draws nothing.


| Parameter | Type | Description |
| --- | --- | --- |
| image | `Image` | The image to draw. |
| position | `Vector2D` | The top left corner. |
| size? | `Vector2D` | The size to draw the image at, in pixels. Defaults to the size of the image. |
| color? | `Color` | A colour that is multiplied with the image. Defaults to opaque white. |
| mode? | `render.ImageMode` | How the image fills the rectangle. Defaults to `render.ImageMode.kFill`. |
| rounding? | `render.Rounding` | The corner radius in pixels. Defaults to no rounding. |


    
If `size` is `nil`, or both of its values are `0` or less, the image is drawn at its own size.
If only one value is `0` or less, that value is calculated from the other one, so the image
keeps its proportions.


  

  

### `render.LoadImage`

```lua
render.LoadImage(bytes: string[, size: Vector2D]): Image
```

Loads an image from the bytes of an image file. The format, such as PNG, JPG, GIF or SVG, is detected from the data.


| Parameter | Type | Description |
| --- | --- | --- |
| bytes | `string` | The contents of the image file. |
| size? | `Vector2D` | The size in pixels to load the image at. Defaults to the size of the image. |


    
Throws an error if the data is shorter than three bytes, or if a value of `size` is not above
`0` and at most `16384`. A GIF is always loaded at its own size.


  

  

### `render.LoadImageRGBA`

```lua
render.LoadImageRGBA(bytes: string, size: Vector2D): Image
```

Loads an image from raw RGBA pixel data that is not compressed.


| Parameter | Type | Description |
| --- | --- | --- |
| bytes | `string` | The raw RGBA pixel data, with 4 bytes for each pixel. |
| size | `Vector2D` | The width and height of the image in pixels. |


    
Each value of `size` must be above `0` and at most `16384`. The data must contain at least
`size.x * size.y * 4` bytes. Otherwise this function throws an error.


  

  

### `render.LoadImageFromFile`

```lua
render.LoadImageFromFile(file: string[, size: Vector2D]): Image
```

Loads an image from a file in the folder of the script. Throws an error if the file does not exist or is empty.


| Parameter | Type | Description |
| --- | --- | --- |
| file | `string` | The path of the file relative to the folder of the script, such as `images/badge.png`. |
| size? | `Vector2D` | The size in pixels to load the image at. Defaults to the size of the image. |


  

### `render.CreateShader`

```lua
render.CreateShader(source: string[, callback: fun(ok: boolean, err: string)]): Shader
```

Compiles a pixel shader from HLSL source with shader model 5.0.


| Parameter | Type | Description |
| --- | --- | --- |
| source | `string` | The HLSL source that defines `main`. |
| callback? | `fun(ok: boolean, err: string)` | Called once when the compile finishes. If the compile failed, `err` is the error message. Throws an error if this is not a function or `nil`. |


    
This function returns at once, and the shader compiles in the background. When it finishes,
`callback` is called and the shader can be drawn. Shaders compile in the order they were
requested, so a shader can wait for others to finish first. If you release the shader, or the
script unloads, before its compile starts, the compile is cancelled.

The source must define `float4 main(PSInput i) : SV_Target`. It returns **linear** RGB with
**straight** alpha. A `Color` is in sRGB, so convert it with `nl_srgb_to_linear` first. The
result is clamped to the range from `0` to `1`, and a pixel with a NaN value is not drawn.

The following names are already declared for the shader. Do not declare them yourself.

```hlsl
struct PSInput { float4 pos : SV_POSITION; float4 col : COLOR0; float2 uv : TEXCOORD0; };
// uv runs 0..1 across the drawn rectangle; pos is the pixel on screen.
float2 nl_resolution;  // screen size in pixels
float2 nl_mouse;       // cursor position
float2 nl_pos;         // rectangle position and size, as passed to render.DrawShader
float2 nl_size;
float4 nl_rounding;    // corner radii in pixels: top-left, top-right, bottom-right, bottom-left
float  nl_time;        // seconds since the shader was created
float  nl_delta;       // seconds since the last frame
uint   nl_frame;       // frame counter
float4 nl_params[16];  // the `params` numbers, four to an element: params[1] is nl_params[0].x
Texture2D nl_image;    // the `image` option
Texture2D nl_backdrop; // a blurred copy of what is under the draw
SamplerState nl_linear_clamp, nl_linear_wrap;
float3 nl_srgb_to_linear(float3 c);  float3 nl_linear_to_srgb(float3 c);
float4 nl_vertex_color(PSInput i);   // the `color` option, linear
float2 nl_local_px(PSInput i);       // position inside the rectangle in pixels
float2 nl_screen_uv(PSInput i);      // position on screen, 0..1
float4 nl_sample_image(PSInput i);   // nl_image at uv
float4 nl_sample_backdrop(PSInput i); // nl_backdrop under this pixel
```

The shader can use only these resources. A global variable must be `static`, because the
script has no constant buffer of its own. Pass values to the shader through `params` instead.
`#include` is not available.

Names that start with `nl_`, and the name `PSInput`, belong to the code around the source. If
the source declares one of them, the compile fails.

The compile also fails if the shader has more than 8192 instructions, if nested
`[unroll(n)]` loops unroll to more than 1024 iterations in total, or if the source is larger
than 1 MB after its macros are expanded. The error message then gives the reason.

Throws an error if the source is empty or larger than 64 KB, if the script already has 32
shaders, or if 256 shaders exist across all scripts.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/render:0:fc6d1ac9bf26"
local plasma = render.CreateShader([[
float4 main(PSInput i) : SV_Target
{
    float2 p = nl_local_px(i) / 40.0;
    float v = sin(p.x + nl_time) + sin(p.y + nl_time * 1.3) + sin(p.x + p.y + nl_time * 0.7);
    float3 c = 0.5 + 0.5 * cos(v + float3(0.0, 2.0, 4.0));
    return float4(c, nl_params[0].x);
}
]], function(ok, err) if not ok then print(err) end end)

events.render:Set(function()
    render.DrawShader(plasma, Vector2D(100, 100), Vector2D(300, 150), { params = { 0.9 }, rounding = 12 })
end)
```


  

  

### `render.DrawShader`

```lua
render.DrawShader(shader: Shader, position: Vector2D, size: Vector2D[, options: render.ShaderOptions])
```

Draws a rectangle in which every pixel is calculated by `shader`. A shader that is still compiling, or that failed, draws nothing. Throws an error if the shader was released or belongs to another script.


| Parameter | Type | Description |
| --- | --- | --- |
| shader | `Shader` | A shader from `render.CreateShader`. |
| position | `Vector2D` | The top left corner. |
| size | `Vector2D` | The width and height in pixels. |
| options? | `render.ShaderOptions` | Values for the shader. Throws an error if this is not a table or `nil`. |


    
Rotation from `render.PushRotation` and clip rectangles apply in the same way as for other
drawing functions.

Inside a `render.PushTransform` block, the rectangle is drawn on the plane. Then `uv`,
`nl_local_px` and the rounding follow the plane, and `nl_pos` and `nl_size` are the rectangle
on the plane as you passed it. `nl_mouse`, `nl_screen_uv` and `nl_backdrop` stay in screen
space. The backdrop under such a rectangle is not blurred, so do not read it there.

A script can draw at most 512 shaders in each frame. At most 16 of them can read
`nl_backdrop`, because each of these blurs the area under it first. A draw over either limit
throws an error.


  

  

### `render.PushSmoothing`

```lua
render.PushSmoothing(smoothing: number)
```

Sets the amount of smoothing, also called antialiasing, for everything drawn until the matching `render.PopSmoothing` call.


| Parameter | Type | Description |
| --- | --- | --- |
| smoothing | `number` | The amount of smoothing. |


    
If a smoothing, blur, clip rectangle or clip shader is still pushed when your `render` callback
returns, it is removed for you and a script error is shown.


  

  

### `render.PopSmoothing`

```lua
render.PopSmoothing()
```

Removes the smoothing set by `render.PushSmoothing`.


  

### `render.PushBlur`

```lua
render.PushBlur([strength: number, is_static: boolean])
```

Starts a blur area. Everything drawn until the matching `render.PopBlur` call is drawn over a blurred copy of the background.


| Parameter | Type | Description |
| --- | --- | --- |
| strength? | `number` | The strength of the blur. Defaults to `1`. |
| is_static? | `boolean` | If `true`, the blur is calculated once instead of every frame. Defaults to `true`. |


  

### `render.PopBlur`

```lua
render.PopBlur()
```

Ends the blur area started by `render.PushBlur`. If no blur area is started, this function does nothing.


  

### `render.PushClipRect`

```lua
render.PushClipRect(position: Vector2D, size: Vector2D[, intersect: boolean])
```

Starts a clip rectangle. Everything drawn until the matching `render.PopClipRect` call is cut to this rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner of the clip rectangle. |
| size | `Vector2D` | The width and height of the clip rectangle. |
| intersect? | `boolean` | If `true`, the new rectangle is limited to the area of the current clip rectangle. If `false`, it replaces the current clip rectangle. Defaults to `false`. |


  

### `render.PopClipRect`

```lua
render.PopClipRect()
```

Ends the clip rectangle started by `render.PushClipRect`.


  

### `render.PushShadow`

```lua
render.PushShadow()
```

Starts recording shapes for a shadow. The matching `render.PopShadow` call draws a shadow for the recorded shapes.


  

### `render.PopShadow`

```lua
render.PopShadow(color: Color, size: number[, offset: Vector2D])
```

Ends the recording started by `render.PushShadow` and draws a soft shadow for the recorded shapes.


| Parameter | Type | Description |
| --- | --- | --- |
| color | `Color` | The colour of the shadow. |
| size | `number` | The blur radius of the shadow in pixels. |
| offset? | `Vector2D` | How far the shadow is moved. Defaults to `Vector2D(0, 0)`. |


  

### `render.PushClipShader`

```lua
render.PushClipShader()
```

Starts a clip shader area. The shapes drawn until the matching `render.PopClipShaderRect` or `render.PopClipShaderCircle` call are cut to the shape given to that call.


    
If the area is still open when your `render` callback returns, it is closed for you and
everything drawn inside it is thrown away.


  

  

### `render.PopClipShaderRect`

```lua
render.PopClipShaderRect(position: Vector2D, size: Vector2D[, color: Color, rounding: render.Rounding])
```

Ends the clip shader area started by `render.PushClipShader` and cuts the shapes drawn inside it to a rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The top left corner of the clip rectangle. |
| size | `Vector2D` | The width and height of the clip rectangle. |
| color? | `Color` | A colour that is applied to the shapes inside the area. Defaults to opaque white. |
| rounding? | `render.Rounding` | The corner radius of the clip rectangle in pixels. Defaults to no rounding. |


  

### `render.PopClipShaderCircle`

```lua
render.PopClipShaderCircle(center: Vector2D, radius: number[, start_degrees: number, percentage: number])
```

Ends the clip shader area started by `render.PushClipShader` and cuts the shapes drawn inside it to a circle or to a part of a circle.


| Parameter | Type | Description |
| --- | --- | --- |
| center | `Vector2D` | The center of the clip circle. |
| radius | `number` | The radius in pixels. |
| start_degrees? | `number` | The angle in degrees where the arc starts. Defaults to `0`. |
| percentage? | `number` | How much of the full circle to keep, from `0` to `1`. Defaults to `1`. |


  

### `render.PushComplexShadow`

```lua
render.PushComplexShadow()
```

Starts recording shapes for a detailed shadow. The matching `render.PopComplexShadow` call draws a high quality shadow that follows the exact outline of the recorded shapes.


    
Recordings cannot be nested. If you start one inside another, its shapes become part of the
outer recording and do not get a shadow of their own.


  

  

### `render.PopComplexShadow`

```lua
render.PopComplexShadow(color: Color[, only_shadow: boolean, bottom_right_or_top_left: boolean])
```

Ends the recording started by `render.PushComplexShadow` and draws the shadow.


| Parameter | Type | Description |
| --- | --- | --- |
| color | `Color` | The colour of the shadow. |
| only_shadow? | `boolean` | If `true`, only the shadow is drawn and the recorded shapes are not. Defaults to `false`. |
| bottom_right_or_top_left? | `boolean` | The direction of the shadow. Pass `true` to move it to the bottom right, or `false` to move it to the top left. Pass `nil` to not move it. Defaults to `nil`. |


  

### `render.PushRotation`

```lua
render.PushRotation(ang: number[, center: Vector2D])
```

Starts a rotation. Everything drawn until the matching `render.PopRotation` call is rotated by `ang`.


| Parameter | Type | Description |
| --- | --- | --- |
| ang | `number` | The rotation angle in degrees. |
| center? | `Vector2D` | The point to rotate around. Defaults to the center of the area that contains all shapes drawn after this call. |


    
Only one rotation can be active at a time. If you call this function again before
`render.PopRotation`, the new rotation replaces the old one.


  

  

### `render.PopRotation`

```lua
render.PopRotation()
```

Applies and ends the rotation started by `render.PushRotation`. Throws an error if `render.PushRotation` was not called earlier in the same frame.


  

### `render.LoadFont`

```lua
render.LoadFont(builtin: render.EspFont): Font
```

Loads one of the ESP fonts. The size, effect and hinting of these fonts come from the ESP settings. If you pass them, they are ignored.


| Parameter | Type | Description |
| --- | --- | --- |
| builtin | `render.EspFont` | The ESP font to load. |


  

### `render.LoadFont`

```lua
render.LoadFont(name: string, size: number[, effect: render.FontEffect, hinting: render.FontHinting]): Font
```

Loads a font at a given size. Pass the name of a font family, or the path of a font file in the folder of the script. Font files can be `.ttf`, `.otf` or `.ttc` files.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the font family, or the path of a font file relative to the folder of the script. |
| size | `number` | The font size in pixels, above `0` and at most `512`. |
| effect? | `render.FontEffect` | The outline or shadow effect. Defaults to `render.FontEffect.kNone`. |
| hinting? | `render.FontHinting` | The hinting of the font. Defaults to `render.FontHinting.DirectWriteNatural`. |


    
A name can be the name of a font installed on the system or of a font that comes with the
cheat. An unknown name throws an error. In the first moments after the game starts, the list of
installed fonts is still being read. During this time any name is accepted, and the font stays
not `loaded` until the list is ready. If the name is unknown, a script error is shown at that
point and the `failed` field of the font becomes `true`.

A name that contains `/` or `\`, or that ends in `.ttf`, `.otf` or `.ttc`, is a path. The path
is relative to the folder of the script, in the same way as for `render.LoadImageFromFile`. You
can also pass a path that `cloud.ReadResource` returned for a file of the script. An absolute
path works only when it points inside the folder of the script. Any other path throws the same
error as a missing file.

The file is read and checked when you call this function. Throws an error if the file is not a
usable scalable font, or if it is larger than 32 MB. A `.ttc` file loads its first face. Each
file is read only once. Loading it again at any size uses the same data until the script
reloads, so you can call this function from a `render` callback without a large cost.

Throws an error if `size` is not above `0` and at most `512`, or if `effect` or `hinting` is not
a value of its enum.


  

  

### `render.DrawText`

```lua
render.DrawText(position: Vector2D, color: Color, font: Font[, flags: string, ...: any])
```

Draws text. The values after `flags` are converted to strings with `tostring` and joined to make the text. If the font is not loaded yet, nothing is drawn.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The position of the text. The flags decide how the text is aligned to it. |
| color | `Color` | The colour of the text. |
| font | `Font` | The font to draw with. |
| flags? | `string` | Any combination of `c` to center, `r` to align right and `d` to apply DPI scaling. |
| ...? | `any` | The values to draw as text. |


    
`flags` is a string of letters. Use `c` to center the text on `position`, `r` to align the
right edge of the text to `position`, and `d` to apply DPI scaling. If you pass both `c` and
`r`, the text is centered.

Text is placed on whole pixels. A font with `render.FontHinting.Msdf` keeps the exact position,
so its text can move smoothly.


  

  

### `render.DrawTextEx`

```lua
render.DrawTextEx(position: Vector2D, color: Color, font: Font, size: number[, flags: string, ...: any])
```

Draws text at `size` pixels instead of the size of the font. In all other ways it works like `render.DrawText`.


| Parameter | Type | Description |
| --- | --- | --- |
| position | `Vector2D` | The position of the text. The flags decide how the text is aligned to it. |
| color | `Color` | The colour of the text. |
| font | `Font` | The font to draw with. |
| size | `number` | The size to draw the text at, in pixels. |
| flags? | `string` | Any combination of `c` to center, `r` to align right and `d` to apply DPI scaling. |
| ...? | `any` | The values to draw as text. |


    
With a `render.FontHinting.Msdf` font, the text stays sharp at any size and the space between
the letters stays exact. So you can animate the size without loading more fonts. Other fonts
are stretched and become blurry at sizes other than their own size. An outline or drop shadow
is scaled with the text.

Throws an error if `size` is not above `0` and at most `512`.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/render:1:8bcdbd9fb8f1"
local font = render.LoadFont("Calibri", 24, render.FontEffect.kOutline, render.FontHinting.Msdf)

events.render:Set(function()
    render.DrawTextEx(Vector2D(200, 200), Color(255, 255, 255), font, 48, "c", "Hello")
end)
```


  

  

### `render.MeasureText`

```lua
render.MeasureText(font: Font[, flags: string, ...: any]): Vector2D
```

Returns the size in pixels that the text would have if it was drawn with `render.DrawText`. Takes the same `flags` and values as `render.DrawText`. Only the `d` flag changes the result.


| Parameter | Type | Description |
| --- | --- | --- |
| font | `Font` | The font to measure with. |
| flags? | `string` | Any combination of `c` to center, `r` to align right and `d` to apply DPI scaling. |
| ...? | `any` | The values to measure as text. |


    
Returns `Vector2D(0, 0)` if the text is empty or the font is not loaded yet.


  

  

### `render.MeasureTextEx`

```lua
render.MeasureTextEx(font: Font, size: number[, flags: string, ...: any]): Vector2D
```

Returns the size in pixels that the text would have if it was drawn with `render.DrawTextEx` at `size`. Returns `Vector2D(0, 0)` if the text is empty or the font is not loaded yet.


| Parameter | Type | Description |
| --- | --- | --- |
| font | `Font` | The font to measure with. |
| size | `number` | The size to measure the text at, in pixels. |
| flags? | `string` | Any combination of `c` to center, `r` to align right and `d` to apply DPI scaling. |
| ...? | `any` | The values to measure as text. |


    
Throws an error if `size` is not above `0` and at most `512`.


  

  

### `render.LoadImageFromFile`

```lua
render.LoadImageFromFile(file: string[, size: Vector2D]): Image
```

Loads an image from a file. This version adds the formats and the search order of the game to the loader of the framework. The file is searched for in this order.


| Parameter | Type | Description |
| --- | --- | --- |
| file | `string` | The relative path to the image file. |
| size? | `Vector2D` | The size to rasterize the image to. Defaults to the original size of the image. |


    
1. A path that ends with `.vsvg_c` or `.vtex_c` is loaded as a compiled game texture.
2. Other paths are first searched for in the files of the running script.
3. Then the path is searched for in the working directory of the game.
4. Then the path is searched for in the search paths of the engine file system.

For steps 2 to 4, the path must be relative. An absolute path, a path with a drive letter, or a
path that uses `..` to leave the working directory throws an error. If the file is not found,
an error is thrown.

The resources that are available depend on the game content that is installed. Load images
outside the render event.


  

  

### `render.PushTransform`

```lua
render.PushTransform(transform: CTransform)
```

Starts drawing on a plane in the world. Everything that is drawn before `render.PopTransform` is placed on the plane of `transform` instead of on the screen. The screen position `(x, y)` of a shape is used as a position on the plane. The shape is placed at `origin + left * x - up * y` and then projected to the screen.


| Parameter | Type | Description |
| --- | --- | --- |
| transform | `CTransform` | The transform of the plane in world space. Its scale is the number of world units for each pixel. |


    
* The forward axis of the transform is the normal of the plane. It points at the viewer. Text
  drawn at `(0, 0)` with the `"c"` flag is centred on the origin and reads from left to right
  when you look at the plane from the front.
* The scale of the transform is the number of world units for each pixel on the plane. For
  example, with a scale of `0.1`, a font with a size of 12 pixels is about 1.2 units tall.
* Only one transform can be active at a time. Calling this function again before
  `render.PopTransform` throws an error. Use `render.PushRotation` inside the block to rotate
  shapes on the plane.

Only the corners of each shape are projected on the CPU. Circles, ellipses, rounded
rectangles, gradients, images and `render.DrawShader` find the position of each pixel on the
plane in the shader. Because of this, they keep their shape in perspective. For example, a
circle that you see at an angle looks like an ellipse. The glyphs of text and the colours of
simple shapes are interpolated across their triangles instead. At the size of a glyph, you
cannot see the difference.

Screen space effects do not follow the plane. Blur, shadows, glows, clip shaders, clip
rectangles and the `nl_backdrop` of a shader all stay in screen space. Do not use them inside
the block. A clip rectangle that was pushed before the block still clips the block on the
screen. Text that is more than 8192 pixels away from the origin of the plane is not drawn.

Call this function only from the `render` event, and call `render.PopTransform` in the same
event. If the block is still open when the callback returns, the block is closed and a script
error is shown. Its shapes are drawn without projection for that frame.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/render:2:6bd7517e5b6d"
local font = render.LoadFont("Verdana", 24)

events.render:Set(function()
    local origin = Vector(0, 0, 64)
    render.PushTransform(CTransform(origin, QAngle(0, 90, 0), 0.1))
    render.DrawText(Vector2D(0, 0), Color(255, 255, 255), font, "c", "hello")
    render.PopTransform()
end)
```


  

  

### `render.PopTransform`

```lua
render.PopTransform(): boolean
```

Ends the block that `render.PushTransform` started, and projects it to the screen. Calling this function without an open block throws an error.


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `false` if the block was dropped. |


    
If any vertex of the block is behind the camera, the whole block is dropped. A triangle that
reaches behind the eye cannot be projected.


  

  

<a id="render-Rounding"></a>
### `render.Rounding`

The rounding of the corners of a rectangle. Pass one number to round all four corners by the same radius. Pass an array of up to four numbers to give each corner its own radius.


  

<a id="render-ImageMode"></a>
### `render.ImageMode`

How an image fills the rectangle it is drawn in. Used by `render.DrawImage` and `group:AddImage`.


    

### `render.ImageMode`


| Name | Value | Description |
| --- | --- | --- |
| kFill | 0 | Stretch the image to fill the rectangle. |
| kRepeat | 1 | Repeat the image across the rectangle. |


  

  

<a id="render-EspFont"></a>
### `render.EspFont`

The fonts that the ESP uses.


    

### `render.EspFont`


| Name | Value | Description |
| --- | --- | --- |
| kRegular | 0 | Verdana, 9px at base DPI |
| kSmall | 1 | Small Fonts, 7px |
| kBold | 2 | Verdana Bold, 9px at base DPI |


  

  

<a id="render-FontEffect"></a>
### `render.FontEffect`

An outline or shadow that is added to every character of a font.


    

### `render.FontEffect`


| Name | Value | Description |
| --- | --- | --- |
| kNone | 0 | No effect. |
| kDropshadow | 1 | A drop shadow behind each character. |
| kOutline | 2 | An outline around each character. |


  

  

<a id="render-FontHinting"></a>
### `render.FontHinting`

The hinting of a font. Hinting decides how the outlines of the characters are fitted to the pixel grid, and so it also decides the width of the text.


    

### `render.FontHinting`


| Name | Value | Description |
| --- | --- | --- |
| None | 0 | No hinting. Characters keep their exact scaled outlines and widths. |
| DirectWriteNatural | 1 | ClearType hinting with natural DirectWrite widths. This is the default. |
| DirectWriteGdiClassic | 2 | ClearType hinting with GDI Classic widths, rounded to whole pixels. |
| DirectWriteGdiNatural | 3 | ClearType hinting on the vertical axis only, with GDI Natural widths. |
| DirectWriteAliased | 4 | Black and white hinting on both axes, with GDI Classic widths. Text has hard pixel edges. Fonts made for ClearType, such as Segoe UI, look thin and uneven with this value. |
| AutoHint | 5 | The FreeType autohinter with normal hinting. |
| AutoHintLight | 6 | The FreeType autohinter with light hinting on the vertical axis only. |
| AutoHintMono | 7 | The FreeType autohinter with strong hinting made for black and white pixels. |
| Msdf | 8 | No hinting. Characters are stored as multichannel distance fields, so text stays sharp when it is scaled or drawn inside `render.PushTransform`. At small sizes the text is a little softer than with the other values, and the font takes longer to load the first time. Colour emoji are still normal images. |


    
All values except `DirectWriteAliased` draw text with smooth grayscale edges from FreeType.

The `DirectWrite` values follow the hinting instructions of the font in the same way as
DirectWrite. The font and the size still decide whether the outlines are drawn natural,
symmetric or without hinting.

The `AutoHint` values ignore the hinting instructions of the font and use the FreeType
autohinter.


  


## Image — object type

An image that you can draw with `render.DrawImage` or show in the menu.

Images are decoded in the background after the load function returns. Until `loaded` is
`true`, `size` can be `0x0` or the size that you asked for. An SVG image and an image made from
an RGBA buffer have their size at once.

An empty image, such as the avatar of a user who has no avatar, has the size `0x0`, its `loaded`
field is `false` and its `failed` field is `true`.


  

### `Image.failed`

Whether the image will never load. This is `true` if the data could not be decoded or if there is no image at all. This field is read only.


  

### `Image.loaded`

Whether the image is decoded and can be drawn. Until it is `true`, `render.DrawImage` draws nothing. This field is read only.


  

### `Image.size`

The width and height of the image in pixels. Check `loaded` before you use this value.


## Shader — object type

A pixel shader that the script writes in HLSL. Create it with `render.CreateShader` and draw it
with `render.DrawShader`.

The shader is compiled in the background, so it is not ready at once. Until it is ready,
drawing it draws nothing.

A script can keep at most 32 shaders. A shader that failed to compile still counts toward
this limit until you release it. All shaders of a script are released when the script unloads.


  

### `Shader:IsValid`

```lua
Shader:IsValid(): boolean
```

Returns `true` if the shader still exists. Returns `false` after `Release` is called.


  

### `Shader:IsReady`

```lua
Shader:IsReady(): boolean
```

Returns `true` if the shader is compiled and can be drawn.


  

### `Shader:GetError`

```lua
Shader:GetError(): string?
```

Returns the error message if the shader failed. Line numbers in the message are counted from the first line of the source that the script passed.


    
If the shader compiled but the graphics device could not create it, the message says so.
Returns `nil` while the shader compiles and after it is created successfully.


  

  

### `Shader:Release`

```lua
Shader:Release()
```

Releases the shader now, before the script unloads. If you draw the shader after this, it throws an error. Calling this function on a shader that is already released does nothing.


## render.ShaderOptions — object type

Options for `render.DrawShader`. If a field has the wrong type, `render.DrawShader` throws an
error.


  

### `render.ShaderOptions.blur`

How strongly `nl_backdrop` is blurred. `0` gives an almost sharp copy. Must be `0` or more. Defaults to `1`.


  

### `render.ShaderOptions.color`

The vertex colour that the shader reads with `nl_vertex_color`. Defaults to opaque white.


  

### `render.ShaderOptions.image`

The image that the shader reads as `nl_image`.


  

### `render.ShaderOptions.params`

Up to 64 numbers that the shader reads as `nl_params`. Missing numbers are `0`. More than 64 numbers, or a NaN or infinite number, throw an error.


  

### `render.ShaderOptions.rounding`

The corner radius in pixels. The output of the shader is cut to these corners. Each radius is limited to half of the shorter side of the rectangle. A NaN or infinite number throws an error.


## Font — object type

A font that you can use with `render.DrawText` and `render.MeasureText`.

Fonts load in the background. While a font is not loaded, `render.DrawText` draws nothing with
it and `render.MeasureText` returns `Vector2D(0, 0)`. Check `loaded` before you draw. The
`loaded` field is `false` both while the font is loading and after it failed. Use `failed` to
tell these two cases apart, for example to switch to another font.

A font family name can match several font files. The `file` and `face` fields tell you which
file and which face were chosen.

Only `size` can be changed. Assigning to any other field does nothing.


  

### `Font.face`

The index of the face inside the font file. A `.ttc` file holds several faces, and the named styles of a variable font also use this index. This field is read only.


  

### `Font.failed`

Whether the font cannot load at its current size. This is `true` if the font name is not installed or if the size could not be loaded. Always `false` for a font from `render.EspFont`. A font file is checked when you load it, so a font loaded from a file does not fail later because the file cannot be read. This field is read only.


  

### `Font.file`

The file name of the font file that was chosen, without its folder. For a font loaded from a file, this is the file name from the path that you passed. Empty for a font from `render.EspFont` and for a font that is not loaded yet. This field is read only.


  

### `Font.loaded`

Whether the font is ready to draw. A new size is ready one frame or more after it is set. This field is read only.


  

### `Font.size`

The font size in pixels. You can assign a new size from above `0` to `512`. Other values throw an error. Assigning a new size loads the font again and resets `failed`. For a font from `render.EspFont`, an assigned size is ignored.
