> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Panorama


## panorama.Object — object type · callable

A handle to a Panorama value. Panorama runs JavaScript in V8, and the value can be an object,
an array or a function.

Index the handle to read a property. If the property is an object or a function, you get
another `panorama.Object`. For any other value, you get a plain Lua value. Assign to a property
of the handle to set it. Call the handle to run it as a JavaScript function.

The object of a panel, as returned by `panorama.ids.`, is also a `panorama.Object`. Its type
is the type of the panel, for example `panorama.panels.CSGOHud`.

Call a method with a dot, as in `handle.method(...)`. If you use a colon, the handle itself is
passed as the first argument. A JavaScript array is also a handle. Its first index is `0`, and
`#` returns its `length`.

A handle works while the context that it was read through exists. For a value read through
`panorama`, this is the own context of the script, which exists until the script unloads. For
a panel from `panorama.ids`, this is the context of the scripts of that panel. This means that
the handle of a HUD panel stops working when the HUD is created again. Using a handle after
that throws an error. Read `panorama.ids.` again to get a new handle. It returns **nil**
while the panel does not exist.

`tostring` returns `panorama.Object<paneltype>` for the object of a panel that exists, and
`panorama.Object` for any other value.


  

<a id="panoramaobject"></a>
### `panorama.Object(...)`

```lua
panorama.Object([...: any]): any
```


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` |  |


  

### `panorama.Object[string]`


  

<a id="panoramaobject"></a>
### `#panorama.Object`


<a id="panorama-1"></a>

## panorama  — global table


Gives access to the Panorama UI of the game. Panorama runs JavaScript in V8.

Every script gets its own Panorama context. The context is created the first time that the
script uses this namespace. It is a JavaScript context of the same kind as the contexts of the
panels of the game. It holds the API objects of the game, `$`, and the standard globals of
JavaScript. It does not depend on the HUD or the main menu, so it works in the same way in the
menu, on the loading screen and in a match.

When the script unloads, the context is deleted. Everything that was registered from it is
deleted with it. This includes the handlers for unhandled events, the panels from
`panorama.CreatePanel`, and the functions that were defined in the context.

**`panorama.`** reads a global of the context of the script. This can be an API object,
such as `panorama.GameStateAPI` or `panorama["$"]`, a JavaScript global such as `panorama.JSON`,
or a name that the script defined. The API objects are listed on the API objects page under
Panorama in Dumped Data. A name that does not exist returns **nil**. Assign
`panorama. = value` to define a global in the context, for code that you compile with
`panorama.Compile`.

**`panorama.ids.`** returns the object of the panel with this id. Its type is the type of
the panel. The ids that the game had when the docs were made are listed on the Panel ids page
under Panorama in Dumped Data. The id of any other panel that exists also works, but its object
has no specific type. If several panels have the same id, the panel that owns a JavaScript
context is returned. Every lookup goes through all panels of the game, so keep the handle while
it works. Do not look it up again in every frame.

The functions below are names that Lua defines on `panorama`. If a JavaScript global has the
same name, you can still get it with `panorama.Compile("return Name")`.

An id is the name of one panel. A panel type is a class of panels. Valve uses some type names
also as ids. For example, `panorama.ids.CSGOHud` is the plain `Panel` at the root of the HUD,
and the panel of type `CSGOHud` is its child `panorama.ids.Hud`. `MainMenu` and `LoadingScreen`
work in the same way. The Panel ids page under Panorama in Dumped Data has a note for every id
of this kind. While the game runs, read `.paneltype` to get the type of a panel.

Values are converted to JavaScript when Lua calls a JavaScript function or assigns a property,
and when a Lua function that JavaScript called returns. This table shows the conversion.

| Lua                        | JavaScript                                                                                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| nil                        | `null`                                                                                                                                                                                     |
| boolean, number, string    | the same value                                                                                                                                                                             |
| table with the keys 1 to n | a new `Array`, with the first index `0`                                                                                                                                                    |
| any other table            | a new plain object with the string keys and number keys of the table. Keys of other types are left out. A table that holds itself, or that is passed twice in one call, becomes one object |
| function                   | a JavaScript function that calls the Lua function                                                                                                                                          |
| `panorama.Object`          | the JavaScript value of the handle                                                                                                                                                         |
| anything else              | `null`                                                                                                                                                                                     |

Values are converted back to Lua in this way. `null` and `undefined` become **nil**. Booleans,
numbers and strings stay the same. A `BigInt` becomes a string with its decimal value. Objects,
arrays and functions become `panorama.Object` handles. Any other value, such as a symbol,
becomes **nil**.

If JavaScript throws an exception while Lua reads, assigns, calls or compiles, Lua throws an
error with the message of the exception. The message starts with the script and the line where
the exception came from.

When you give a Lua function to JavaScript, these rules apply.

The JavaScript arguments are converted to Lua. The first return value of the Lua function is
returned to JavaScript. If the function returns nothing, JavaScript gets `undefined`.

The function runs as the script that gave it. If it throws an error, the error is listed under
the errors of that script, and JavaScript gets it as an `Error` that it can catch.

The function works until its script unloads. This includes the `shutdown` listener of the
script. After that, calling the function throws an error. All scripts are reloaded together,
so the function also stops working when you turn another script on or off, or when you save a
developer script.

Each time the function is passed to JavaScript, a new JavaScript function is made. Two of them
are not equal with `===`.

Calling the function with `new` throws a `TypeError`.

Lua and JavaScript can call each other up to 32 levels deep. A table can be nested up to 32
levels deep. If you go deeper, an error is thrown on the side that made the call.

`$.RegisterEventHandler` throws an error in the context of a script, because the game would keep
the handler on the target panel after the context of the script is deleted. Use
`panorama.RegisterForUnhandledEvent` instead, or run the registration in the own context of the
panel with `panorama.Compile(source, panel)`.

```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:0:0dd1741c4c39"
local hud = panorama.ids.Hud
if hud then
  local radar = hud.FindChildTraverse("HudRadar")
  if radar then radar.visible = false end

  local label = panorama.CreatePanel("Label", hud, "MyLabel") --[[@as panorama.panels.Label]]
  label.SetLocString("#SFUI_BuyMenu_Cannot_Afford")
end
```

```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:1:1941d88fb604"
local make_counter = panorama.Compile([[
  var kills = 0;
  return {
    kill: function (name) { kills++; return 'You killed ' + name + '! (' + kills + ')'; },
    reset: function () { kills = 0; },
  };
]])

local counter = make_counter()
print(counter.kill("XYZ")) -- You killed XYZ! (1)
counter.reset()
```


  

### `panorama.ids`

The panels by id.


  

### `panorama.Compile`

```lua
panorama.Compile(source: string[, panel: (panorama.Object|panorama.panels.Panel)]): panorama.Object
```

Compiles JavaScript as the body of a function and returns that function. Call the function to run the body. A `return` in the body gives the result of the call. Error messages give the script as `lua://<script name>` and the line in `source`.


| Parameter | Type | Description |
| --- | --- | --- |
| source | `string` | The JavaScript code of the function body. |
| panel? | `(panorama.Object\|panorama.panels.Panel)` | The panel whose context compiles the body. The default is the own context of the script. |


    
Without `panel`, the body runs in the own context of the script. With `panel`, the body runs in
the context of the scripts of that panel. There, the globals that those scripts defined are
visible, and `$.GetContextPanel()` returns the panel that owns the context. The function then
works while that context exists. Anything that the function registers there belongs to that
context. It is not deleted when the script unloads.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:2:44cf56051d89"
local hud = panorama.ids.Hud
if hud then
  local owner = panorama.Compile("return $.GetContextPanel().id", hud)
  print(owner()) -- the id of the panel that owns the HUD's context
end
```


  

  

### `panorama.RegisterForUnhandledEvent`

```lua
panorama.RegisterForUnhandledEvent(event: string, handler: fun(...: any)): integer
```

Calls `handler` each time the event `event` is dispatched and no panel handles it. This works in the same way as `$.RegisterForUnhandledEvent`. `handler` gets the arguments of the event. The registration belongs to the context of the script and ends when the script unloads.


| Parameter | Type | Description |
| --- | --- | --- |
| event | `string` | The name of the event. |
| handler | `fun(...: any)` | The function that is called with the arguments of the event. |


| Return | Type | Description |
| --- | --- | --- |
|  | `integer` | The id of the handler. Pass it to `panorama.UnregisterForUnhandledEvent` to remove the handler. |


    
Throws an error if `event` is not an event that the game registered.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:3:181f1f359506"
panorama.RegisterForUnhandledEvent("CSGOShowMainMenu", function()
  print("main menu shown")
end)
```


  

  

### `panorama.UnregisterForUnhandledEvent`

```lua
panorama.UnregisterForUnhandledEvent(event: string, id: integer)
```

Removes a handler that was registered with `panorama.RegisterForUnhandledEvent`.


| Parameter | Type | Description |
| --- | --- | --- |
| event | `string` | The name of the event that the handler was registered for. |
| id | `integer` | The id of the handler, as returned by `panorama.RegisterForUnhandledEvent`. |


  

### `panorama.DispatchEvent`

```lua
panorama.DispatchEvent(event: string[, ...: any]): boolean
```

Dispatches the event `event` with `...` as its arguments. This works in the same way as `$.DispatchEvent`. Every argument is passed as text, and the event converts it to the argument types that it uses.


| Parameter | Type | Description |
| --- | --- | --- |
| event | `string` | The name of the event. |
| ...? | `any` | The arguments of the event, and then the target if there is one. |


| Return | Type | Description |
| --- | --- | --- |
|  | `boolean` | `true` if a handler handled the event. |


    
If you pass one more argument after the arguments of the event, it is the target of the event.
The target is a panel or the id of a panel. Without a target, the event starts at the context
of the script, so only the handlers for unhandled events get it.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:4:e0e7a742c85c"
panorama.DispatchEvent("PlaySoundEffect", "UIPanorama.store_item_activated")
```


  

  

### `panorama.CreatePanel`

```lua
panorama.CreatePanel(type: string, parent: panorama.panels.Panel|panorama.Object[, id: string, properties: table]): panorama.panels.Panel
```

Creates a panel of type `type` as a child of `parent` and returns the object of the panel. This works in the same way as `$.CreatePanel`. The panel belongs to the script. It is deleted when the script unloads, in any place where it was put.


| Parameter | Type | Description |
| --- | --- | --- |
| type | `string` | A registered panel type, such as `"Label"` or `"Panel"`. |
| parent | `panorama.panels.Panel\|panorama.Object` | The parent panel. |
| id? | `string` | The id of the panel. |
| properties? | `table` | The attributes and events of the panel. |


    
`properties` sets attributes and panel events in the same way as layout XML, for example
`{ class = "MyClass", text = "#SFUI_BuyMenu_Cannot_Afford" }`. A panel event, such as
`onactivate` or `onmouseover`, can be a string of JavaScript or a Lua function. A string runs in
the context of the scripts of the panel. A Lua function runs as the script when the event
happens. A Lua function is set on the new panel with `SetPanelEvent`, so you can also call
`panel.SetPanelEvent("onactivate", fn)` later to get the same result.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/panorama:5:4439d00947f8"
local menu = panorama.ids.MainMenu
if menu then
  panorama.CreatePanel("TextButton", menu, "lua_button", {
    text = "Click me",
    style = "horizontal-align: center; vertical-align: center; width: 240px; height: 60px;",
    onactivate = function()
      panorama.DispatchEvent("PlaySoundEffect", "UIPanorama.store_item_activated")
    end,
  })
end
```
