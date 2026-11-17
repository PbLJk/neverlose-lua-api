> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Schema Values


## value.Object — object type

A value that is read from game memory through the schema system.

Structured schema values are views of the memory of the game. A view reads and writes the
memory directly, and it is valid only while the object that owns the memory exists.
`value.QuantizedFloat` values are copies of the data at the time of the read.

`Entity` and `value.View` have the methods below, which return the data pointer and the
schema type.


  

### `value.Object:GetInstance`

```lua
value.Object:GetInstance(): userdata
```

Returns the data pointer.


    


**Warning:** 
This function is for advanced users. You can only use the pointer through FFI. The pointer is
valid only while the object that owns the data exists. Do not keep it after the entity is
deleted.


  

  

### `value.Object:GetSchemaType`

```lua
value.Object:GetSchemaType(): schema.Type
```

Returns the schema type.


## value.View — object type


A `value.Object` that holds a pointer together with its type. Use `Cast` to read the same
address as a different `schema.Type`.


  

### `value.View:Cast`

```lua
value.View:Cast(type: schema.Type): value.View
```

Returns a view of the same address with the given schema type. The type must describe the data at that address. A cast does not change the data. If `type` is **nil**, the view keeps its current type.


| Parameter | Type | Description |
| --- | --- | --- |
| type | `schema.Type` | The new type. It must describe the data at this address. |


## value.AtomicCollection — object type


A dynamic array of the engine, such as `CUtlVector`. The length operator `#` returns the
number of elements. When you index the array directly, the first element has the index `0`.
An index outside the array reads as **nil**.

`Value`, `pairs` and `ipairs` use a copy of the array in a Lua table, where the first element
has the index `1`.


  

### `value.AtomicCollection:Value`

```lua
value.AtomicCollection:Value(): T[]
```

Copies the elements into a Lua table, where the first element has the index `1`. Entities in the collection are not copied. The table holds references to them.


## value.FixedArray — object type


A fixed size array of the engine, such as `uint32[2]`. The length operator `#` returns the
number of elements. When you index the array directly, the first element has the index `0`.
An index outside the array reads as **nil**.

`Value`, `pairs` and `ipairs` use a copy of the array in a Lua table, where the first element
has the index `1`.


  

### `value.FixedArray:Value`

```lua
value.FixedArray:Value(): T[]
```

Copies the elements into a Lua table, where the first element has the index `1`.


## value.Named — object type

Adds the `GetClassName` method to values whose schema type is a declared class of the engine.


  

### `value.Named:GetClassName`

```lua
value.Named:GetClassName(): string
```

Returns the name of the class.


## value.DeclaredClass — object type


An object of a declared class of the engine. Read and write its schema fields by name with
`self.<name>`.


  

### `value.DeclaredClass:GetField`

```lua
value.DeclaredClass:GetField(name: string): any
```

Reads a schema field by name. This does the same as `self.<name>`. Use it when the name of the field is held in a variable, or when the field has the same name as a method.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the schema field. |


  

### `value.DeclaredClass:SetField`

```lua
value.DeclaredClass:SetField(name: string, value: any)
```

Writes a schema field by name. This does the same as `self.<name> = value`.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the schema field. |
| value | `any` | The value to write. It is converted to the schema type of the field. |


    
It takes the same values as a field assignment. Throws an error if the field has a type that
cannot be written, such as a bitfield or a fixed array.


  


## value.Bitfield — object type


A packed integer field that uses fewer bits than its storage type. You cannot get its value
through the schema. Reading the field returns this object, and writing the field throws an
error.


  

### `value.Bitfield:NumBits`

```lua
value.Bitfield:NumBits(): integer
```

Returns the number of bits in the field.


## value.QuantizedVector — object type


An object of a quantized vector class, such as `CNetworkOriginQuantizedVector`.


  

### `value.QuantizedVector:Get`

```lua
value.QuantizedVector:Get(): Vector
```

Returns the quantized vector as a regular 3D `Vector`.


## value.QuantizedFloat — object type

A copy of one component of a quantized vector. The copy does not change when the game
changes the field. Read the field again to get the current value.


  

### `value.QuantizedFloat:MinValue`

```lua
value.QuantizedFloat:MinValue(): number
```

Returns the lowest value that the real value can have.


  

### `value.QuantizedFloat:MaxValue`

```lua
value.QuantizedFloat:MaxValue(): number
```

Returns the highest value that the real value can have.


  

### `value.QuantizedFloat:Get`

```lua
value.QuantizedFloat:Get(): number
```

Returns the value.


  

### `value.QuantizedFloat:NumBits`

```lua
value.QuantizedFloat:NumBits(): integer
```

Returns the number of bits that the value uses.
