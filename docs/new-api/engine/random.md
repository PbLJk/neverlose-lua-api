> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Random


<a id="random-1"></a>

## random  — global table


Uses the random number generator of the engine. It is a different generator from the one
used by `math.random`.

The functions `random.Int`, `random.Float`, `random.FloatExp` and `random.GaussianFloat` use
the shared generator of the game. You cannot set a seed for it, because a new seed would change
the random results of the game itself. Use `random.Stream` to get a sequence of numbers that
you can repeat with a seed.


  

### `random.Int`

```lua
random.Int(min: integer, max: integer): integer
```

Returns a random integer from `min` to `max`. Both `min` and `max` can be returned. If `min` is greater than `max`, the two values are swapped.


| Parameter | Type | Description |
| --- | --- | --- |
| min | `integer` | The lowest value. |
| max | `integer` | The highest value. |


  

### `random.Float`

```lua
random.Float(min: number, max: number): number
```

Returns a random floating point number from `min` to `max`. If `min` is greater than `max`, the two values are swapped.


| Parameter | Type | Description |
| --- | --- | --- |
| min | `number` | The lowest value. |
| max | `number` | The highest value. |


  

### `random.FloatExp`

```lua
random.FloatExp(min: number, max: number[, exponent: number]): number
```

Returns a random floating point number from `min` to `max`. First, a uniform random number from 0 up to 1 is made. This number is raised to the power of `exponent`, and then it is scaled to the range. If `min` is greater than `max`, the two values are swapped.


| Parameter | Type | Description |
| --- | --- | --- |
| min | `number` | The lowest value. |
| max | `number` | The highest value. |
| exponent? | `number` | The power that the uniform random number is raised to. The default is `1`. |


  

### `random.GaussianFloat`

```lua
random.GaussianFloat([mean: number, stddev: number]): number
```

Returns a random number with a normal distribution.


| Parameter | Type | Description |
| --- | --- | --- |
| mean? | `number` | The mean of the distribution. The default is `0`. |
| stddev? | `number` | The standard deviation of the distribution. The default is `1`. |


  

<a id="randomstream"></a>
### `random.Stream`

```lua
random.Stream([seed: integer]): random.Stream
```

Creates a separate generator that uses the same algorithm as the engine, `CUniformRandomStream`. A seed always gives the same sequence of numbers as the engine gives for that seed. Using a stream does not change the shared generator of the game.


| Parameter | Type | Description |
| --- | --- | --- |
| seed? | `integer` | A 32 bit seed. The default is `0`. |


    
`seed` can be any signed or unsigned 32 bit value, from `-2^31` to `2^32 - 1`. Any other value
throws an error. Unsigned values are converted to signed values in the same way as the engine
converts them. The engine gives the same sequence for `seed` and `-seed`, and it uses the seed
`1` in place of `0`.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/engine/random:0:3909439b8c7b"
local a, b = random.Stream(1337), random.Stream(1337)
assert(a:Float(0, 360) == b:Float(0, 360)) -- same seed, same sequence
```


  


## random.Stream — object type

A generator with a seed, created by `random.Stream`. Its methods pass `min` and `max` to the
engine exactly as they are given. They never swap the two values.


  

### `random.Stream:SetSeed`

```lua
random.Stream:SetSeed(seed: integer)
```

Starts the stream again with a new seed. The seed follows the same rules as the seed of `random.Stream`.


| Parameter | Type | Description |
| --- | --- | --- |
| seed | `integer` | A signed or unsigned 32 bit seed. |


  

### `random.Stream:Int`

```lua
random.Stream:Int(min: integer, max: integer): integer
```

Returns a random integer from `min` to `max`. Both `min` and `max` can be returned. If `max` is less than `min`, `min` is returned and the stream does not move on to the next number.


| Parameter | Type | Description |
| --- | --- | --- |
| min | `integer` | The lowest value. |
| max | `integer` | The highest value. |


  

### `random.Stream:Float`

```lua
random.Stream:Float([min: number, max: number]): number
```

Returns a random floating point number from `min` to `max`.


| Parameter | Type | Description |
| --- | --- | --- |
| min? | `number` | The lowest value. The default is `0`. |
| max? | `number` | The highest value. The default is `1`. |


  

### `random.Stream:FloatExp`

```lua
random.Stream:FloatExp([min: number, max: number, exponent: number]): number
```

Returns a random floating point number from `min` to `max`. First, a uniform random number from 0 up to 1 is made. This number is raised to the power of `exponent`, and then it is scaled to the range.


| Parameter | Type | Description |
| --- | --- | --- |
| min? | `number` | The lowest value. The default is `0`. |
| max? | `number` | The highest value. The default is `1`. |
| exponent? | `number` | The power that the uniform random number is raised to. The default is `1`. |


  

### `random.Stream:GaussianFloat`

```lua
random.Stream:GaussianFloat([mean: number, stddev: number]): number
```

Returns a random number with a normal distribution.


| Parameter | Type | Description |
| --- | --- | --- |
| mean? | `number` | The mean of the distribution. The default is `0`. |
| stddev? | `number` | The standard deviation of the distribution. The default is `1`. |


  

### `random.Stream:Clone`

```lua
random.Stream:Clone(): random.Stream
```

Returns a copy of the stream in its current state. The copy continues the same sequence. Using one of them does not change the other.
