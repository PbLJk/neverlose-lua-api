> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# View


## view\.ViewContext — object type

The camera of the current frame. It is passed to the `override_view` event. Read and change
`origin`, `angles` and `fov` inside that callback. Do not keep the object after the callback
returns.

Reading or writing a field that does not exist throws an error.


  

### `view.ViewContext.angles`

The view angles of the camera.


  

### `view.ViewContext.fov`

The field of view of the camera in degrees. Setting it to `0` throws an error.


  

### `view.ViewContext.origin`

The position of the camera in world space.


## view\.ViewmodelContext — object type

The root of the first person viewmodel. It is passed to the `override_viewmodel` event.

When the event fires, the bob and sway of the game and the viewmodel options of the cheat are
already applied. After the event, the game still adds aim punch, the offsets for ladders and for
lowered weapons, the blend of the iron sights, and the `viewmodel_offset_*` console variables.

During the callback, `arms` and `weapon` still hold the final transform and the attachments of
the last frame. If you change `angles`, they are normalized after the callback. Do not keep the
object after the callback returns.


  

### `view.ViewmodelContext.angles`

The angles of the viewmodel root.


  

### `view.ViewmodelContext.arms`

The HUD arms that are being set up. Read-only.


  

### `view.ViewmodelContext.origin`

The position of the viewmodel root in world space.


  

### `view.ViewmodelContext.weapon`

The HUD weapon that is attached to `arms`. Read-only.
