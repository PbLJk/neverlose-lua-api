> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Math


<a id="math-1"></a>

## math  — global table


Standard Lua math library, providing common mathematical functions.


  

### `math.huge`

Positive infinity (`1/0`). Useful as an initial value for minimum searches.


  

### `math.pi`

The value of π (3.14159265358979323846…).


  

### `math.abs`

```lua
math.abs(x: Number): Number
```

Returns the absolute value of `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `Number` | Value to take the absolute value of. |


  

### `math.acos`

```lua
math.acos(x: number): number
```

Returns the arc cosine of `x` in radians. `x` must be in the range `[-1, 1]`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Cosine value. Must be in `[-1, 1]`. |


  

### `math.asin`

```lua
math.asin(x: number): number
```

Returns the arc sine of `x` in radians. `x` must be in the range `[-1, 1]`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Sine value. Must be in `[-1, 1]`. |


  

### `math.atan`

```lua
math.atan(y: number): number
```

Returns the arc tangent of `y` in radians. Use `math.atan2` to compute the angle from an (x, y) pair with proper quadrant handling.


| Parameter | Type | Description |
| --- | --- | --- |
| y | `number` | Tangent value. |


  

### `math.atan2`

```lua
math.atan2(y: number, x: number): number
```

Returns the arc tangent of `y/x` in radians, using the signs of both arguments to determine the correct quadrant. Handles the case where `x` is zero correctly.


| Parameter | Type | Description |
| --- | --- | --- |
| y | `number` | Numerator (y component). |
| x | `number` | Denominator (x component). |


  

### `math.ceil`

```lua
math.ceil(x: number): integer
```

Returns the smallest integer value greater than or equal to `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value to round up. |


  

### `math.cos`

```lua
math.cos(x: number): number
```

Returns the cosine of angle `x` (given in radians).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Angle in radians. |


  

### `math.cosh`

```lua
math.cosh(x: number): number
```

Returns the hyperbolic cosine of `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value. |


  

### `math.deg`

```lua
math.deg(x: number): number
```

Converts angle `x` from radians to degrees.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Angle in radians. |


  

### `math.exp`

```lua
math.exp(x: number): number
```

Returns the value `e^x` (the exponential function).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Exponent. |


  

### `math.floor`

```lua
math.floor(x: number): integer
```

Returns the largest integer value less than or equal to `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value to round down. |


  

### `math.fmod`

```lua
math.fmod(x: number, y: number): number
```

Returns the remainder of the division of `x` by `y` that rounds the quotient towards zero.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Dividend. |
| y | `number` | Divisor. |


  

### `math.frexp`

```lua
math.frexp(x: number): number, number
```

Returns the mantissa and binary exponent of `x`. The value satisfies `x = m * 2^e`, where `0.5 <= |m| < 1` (or `m = 0`).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value to decompose. |


  

### `math.ldexp`

```lua
math.ldexp(m: number, e: number): number
```

Returns `m * 2^e` (the inverse of `math.frexp`).


| Parameter | Type | Description |
| --- | --- | --- |
| m | `number` | Mantissa. |
| e | `number` | Exponent. |


  

### `math.log`

```lua
math.log(x: number[, base: integer]): number
```

Returns the logarithm of `x`. If `base` is provided, returns the logarithm in that base; otherwise returns the natural logarithm.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value. Must be positive. |
| base? | `integer` | Logarithm base. Defaults to `e` (natural log). |


  

### `math.log10`

```lua
math.log10(x: number): number
```

Returns the base-10 logarithm of `x`. Equivalent to `math.log(x, 10)`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value. Must be positive. |


  

### `math.max`

```lua
math.max(x: Number[, ...: Number]): Number
```

Returns the maximum value among its arguments.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `Number` | First value. |
| ...? | `Number` | Additional values to compare. |


  

### `math.min`

```lua
math.min(x: Number[, ...: Number]): Number
```

Returns the minimum value among its arguments.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `Number` | First value. |
| ...? | `Number` | Additional values to compare. |


  

### `math.modf`

```lua
math.modf(x: number): integer, number
```

Returns the integral and fractional parts of `x`. Both results have the same sign as `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value to split. |


  

### `math.pow`

```lua
math.pow(x: number, y: number): number
```

Returns `x` raised to the power `y`. Equivalent to `x^y`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Base. |
| y | `number` | Exponent. |


  

### `math.rad`

```lua
math.rad(x: number): number
```

Converts angle `x` from degrees to radians.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Angle in degrees. |


  

### `math.random`

```lua
math.random(m: integer, n: integer): integer
```

Returns a pseudo-random number.


| Parameter | Type | Description |
| --- | --- | --- |
| m | `integer` | Upper bound (single-argument form) or lower bound (two-argument form). |
| n | `integer` | Upper bound (two-argument form). |


    
* `math.random()` returns a float in the range `[0, 1)`.
* `math.random(m)` returns an integer in the range `[1, m]`.
* `math.random(m, n)` returns an integer in the range `[m, n]`.


  

  

### `math.randomseed`

```lua
math.randomseed(x: integer)
```

This function does nothing. All scripts share one pseudo-random number generator, and it is seeded when the script runtime starts.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Seed value. |


    
The first time a script calls this function, a warning is added to the Errors list of the
script and written to the game console.


  

  

### `math.sin`

```lua
math.sin(x: number): number
```

Returns the sine of angle `x` (given in radians).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Angle in radians. |


  

### `math.sinh`

```lua
math.sinh(x: number): number
```

Returns the hyperbolic sine of `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value. |


  

### `math.sqrt`

```lua
math.sqrt(x: number): number
```

Returns the square root of `x`. `x` must be non-negative.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Non-negative value. |


  

### `math.tan`

```lua
math.tan(x: number): number
```

Returns the tangent of angle `x` (given in radians).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Angle in radians. |


  

### `math.tanh`

```lua
math.tanh(x: number): number
```

Returns the hyperbolic tangent of `x`.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `number` | Value. |
