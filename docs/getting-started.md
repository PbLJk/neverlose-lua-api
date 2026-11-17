# Getting started

Place a `.lua` script in the `scripts` folder beside your config folder and load it in Extensions.

Existing lowercase API example:

```lua
local tab = ui.tab("Example")
local group = tab:group("Settings")
local enabled = group:checkbox("Enabled", true)
print("Enabled:", enabled:get())
```

New value-type example (Allow Insecure must already be enabled):

```lua
local v = Vector(3, 4, 0)
print(v:Length()) -- 5
local direction = QAngle(0, 90, 0):GetForward()
print(direction.x, direction.y, direction.z)
```

The first example describes the existing native API. The math example was exercised in the standalone LuaJIT checks; it is not an in-game test receipt.
