> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Global Variables

## globals — global table

Global engine variables for timing and tick state.

If there is no network game client, every field returns nil and assignments do nothing.
Assigning a value to `tickinterval` while there is a network game client throws an error.


  

### `globals.absoluteframetime`

The render frame time without `host_timescale` and without the server and replay multipliers.


  

### `globals.curtime`

The current time of the main world simulation, equal to the server tick multiplied by `tickinterval`. The value is correct only during simulation.


  

### `globals.framecount`

The number of frames since the game started. It increases every frame, also while the game is paused.


  

### `globals.frametime`

The time of the last server or client frame. This is the time that must be simulated.


  

### `globals.in_simulation`

True in the simulation stage, and false in the rendering stage.


  

### `globals.interpolation_amount`

The part of the tick that is not complete in this frame, from 0 to 1. The value is correct only in the rendering stage, when `in_simulation` is false.


  

### `globals.interpolation_amount_prediction`

The part of the input tick that is not complete in this frame, from 0 to 1. The value is correct only in the rendering stage, when `in_simulation` is false.


  

### `globals.maxplayers`

The maximum number of players that the server allows. This is the number of controllers.


  

### `globals.realtime`

The time in seconds since the game started. Do not use it to measure short times between frames.


  

### `globals.sim_ticks_this_frame_index`

The index of the tick that is simulated now in this frame.


  

### `globals.sim_ticks_this_frame_total`

The total number of ticks that are simulated in this frame.


  

### `globals.tickcount`

The number of main world simulation ticks. It increases also while the game is paused.


  

### `globals.tickinterval`

The length of one tick in seconds. Read-only.


  

### `globals.unfilteredframetime`

The render frame time without the minimum and maximum limits.
