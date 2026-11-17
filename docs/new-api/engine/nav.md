> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Nav


<a id="nav-1"></a>

## nav  — global table


Finds walking paths on the navigation mesh of the current map.

The mesh is read from the `.nav` file of the map on the first call after a level loads. It is
removed when the map changes or when you disconnect. Outside a game, or on a map without a
`.nav` file, `nav.IsLoaded` returns `false` and the other functions return `nil`.

Paths are for a player on foot. They can use steps, drops and jumps up to the height of a
crouch jump.

Distances are in walk units. One walk unit is the time a player needs to run one world unit
with a knife at 250 units per second. Drops and jumps take more time, so they count as more
than their length. Divide a distance by 250 to estimate the time in seconds.


  

### `nav.IsLoaded`

```lua
nav.IsLoaded(): boolean
```

Returns whether the navigation mesh of the current map is loaded. The first call on a new level builds the mesh.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/nav:0:7b9b84c6e519"
if not nav.IsLoaded() then print("no nav mesh on this map") end
```


  

  

### `nav.Snap`

```lua
nav.Snap(pos: Vector[, max_distance: number]): Vector?, number?
```

Finds the point on the navigation mesh that is closest to a world position.


| Parameter | Type | Description |
| --- | --- | --- |
| pos | `Vector` | The position in world space. |
| max_distance? | `number` | The search radius in world units. The default is `256`. |


| Return | Type | Description |
| --- | --- | --- |
| point | `Vector?` | The closest point on the mesh. |
| distance | `number?` | The distance from `pos` to `point`. |


    
Returns the point on the mesh and its distance from `pos`. Returns `nil` if there is no
walkable area within `max_distance`. Throws an error if `pos` is not a finite vector or if
`max_distance` is negative or not finite.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/nav:1:9f9a465a39ff"
local point, distance = nav.Snap(Vector(-300, 1200, 100))
if point then
    print("nearest walkable point ", point, ", ", distance, " units away")
end
```


  

  

### `nav.GetDistance`

```lua
nav.GetDistance(from: Vector, to: Vector): number?
```

Returns the shortest walking distance between two world positions, in walk units.


| Parameter | Type | Description |
| --- | --- | --- |
| from | `Vector` | The start position. |
| to | `Vector` | The goal position. |


    
Both positions are moved to the closest point on the mesh within 256 units. Returns `nil` if a
position has no mesh within 256 units, or if no walkable route connects the two positions.
Throws an error if a position is not a finite vector.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/nav:2:acb6f9fe0826"
local pawn = entity.GetLocalPlayerPawn()
local distance = pawn and nav.GetDistance(pawn:GetAbsOrigin(), Vector(-300, 1200, 100))
if distance then print(("about %.1f s away"):format(distance / 250)) end
```


  

  

### `nav.FindPath`

```lua
nav.FindPath(from: Vector, to: Vector): Vector[]?
```

Returns the shortest walking path between two world positions, as a list of points from `from` to `to`.


| Parameter | Type | Description |
| --- | --- | --- |
| from | `Vector` | The start position. |
| to | `Vector` | The goal position. |


    
Both positions are moved to the closest point on the mesh within 256 units to find the
route. The path is smoothed, so it cuts corners where the mesh allows it. Returns `nil` if a
position has no mesh within 256 units, or if no walkable route connects the two positions.
Throws an error if a position is not a finite vector.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/nav:3:2b73dbfcbb19"
local pawn = entity.GetLocalPlayerPawn()
local path = pawn and nav.FindPath(pawn:GetAbsOrigin(), Vector(-300, 1200, 100))
if path then
    for i = 2, #path do
        print(("segment %d: %.0f units"):format(i - 1, path[i - 1]:DistTo(path[i])))
    end
end
```
