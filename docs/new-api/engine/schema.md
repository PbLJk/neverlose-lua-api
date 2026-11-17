> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Schema System


## schema — global table

Gives access to the schema system of the game. The schema system holds the information about
every networked class, its fields, and the types of the fields. Use it to find class types and
enums by name, so that you do not need to write offsets in your code.

Index this table with a name. If a class with this name exists, a `schema.Type` is returned.
If an enum with this name exists, a table that maps the names of the enum values to their
numbers is returned. If the name is the start of the name of a scope, such as `client`, a
`schema.Scope` is returned. Otherwise, **nil** is returned.

This namespace describes types. It does not hold objects of these types. When you read a
value, a structured field can return a `value.*` view, which holds a data pointer and a schema
type. Other fields return plain Lua values or cdata.


  

### `schema[string]`


## schema.Scope — object type

A schema scope. A scope is a game module, for example `client` or `server`. Index it with the
name of a class to get the `schema.Type` of that class in this scope. Index it with the name of
an enum to get a table that maps the names of the enum values to their numbers.


  

### `schema.Scope[string]`


## schema.Type — object type · callable

Describes a schema type. The length operator `#` returns the size of the type in bytes.

Call the type with a pointer to data of this type to read the value at that address. This
does not create a new object. The result can be an entity, a number, cdata or a schema value.
Use the returned views only while the object that owns the data is still valid.


  

### `schema.Type(pointer)`

```lua
schema.Type(pointer: userdata|ffi.cdata*): any
```


| Parameter | Type | Description |
| --- | --- | --- |
| pointer | `userdata\|ffi.cdata*` |  |


  

<a id="schematype"></a>
### `#schema.Type`


  

### `schema.Type:GetSize`

```lua
schema.Type:GetSize(): integer
```

Returns the size of the type in bytes.


  

### `schema.Type:GetAlignment`

```lua
schema.Type:GetAlignment(): integer
```

Returns the alignment of the type in bytes.


  

### `schema.Type:GetInstance`

```lua
schema.Type:GetInstance(): userdata
```

Returns the raw `CSchemaType` pointer.


    


**Warning:** 
This function is for advanced users. You can only use the pointer through FFI.


  

  

### `schema.Type:GetName`

```lua
schema.Type:GetName(): string
```

Returns the name of the schema type.


  

### `schema.Type:GetMetadata`

```lua
schema.Type:GetMetadata(): schema.Type.Meta
```

Returns the metadata of the type. Class, atomic and enum types have metadata. For other types, an empty table is returned. Use `Category` to find the category of a type.


    


**Warning:** 
This function is for advanced users. The metadata names can change between game builds. The
values are native pointers, and you can only use them through FFI.


  

  

### `schema.Type:GetMetadata`

```lua
schema.Type:GetMetadata(classfield: string): schema.Type.Meta
```

Returns the metadata of a field of a class type. If the type is not a class or has no field with this name, an empty table is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| classfield | `string` |  |


  

### `schema.Type:GetFieldOffset`

```lua
schema.Type:GetFieldOffset(classfield: string): integer?
```

Returns the offset in bytes of a field of a class type. Returns **nil** if the class has no field with this name, or if the type is not a class.


| Parameter | Type | Description |
| --- | --- | --- |
| classfield | `string` |  |


  

### `schema.Type:GetBaseClasses`

```lua
schema.Type:GetBaseClasses(): { offset: integer, type: schema.Type }
```

Returns one table for each direct base class of a class type. Each table is a separate return value, in the order in which the base classes are declared. Each table holds the type of the base class and its offset in bytes. Use `{type:GetBaseClasses()}` to put all of them in a table. For other types, nothing is returned.


| Return | Type | Description |
| --- | --- | --- |
| ... | `{ offset: integer, type: schema.Type }` |  |


  

### `schema.Type:GetFields`

```lua
schema.Type:GetFields([no_recurse: boolean]): string[]?
```

Returns the names of the fields of a class type. The fields of the class itself come first, and then the fields of its base classes. Returns **nil** if the type is not a class.


| Parameter | Type | Description |
| --- | --- | --- |
| no_recurse? | `boolean` | Pass `true` to return only the fields of the class itself, without the fields of its base classes. The default is `false`. |


  

### `schema.Type:GetFieldType`

```lua
schema.Type:GetFieldType(classfield: string): schema.Type?
```

Returns the schema type of a field of a class type. Returns **nil** if the class has no field with this name, or if the type is not a class.


| Parameter | Type | Description |
| --- | --- | --- |
| classfield | `string` |  |


  

### `schema.Type:Category`

```lua
schema.Type:Category(): string
```

Returns the category of the type. The category is one of `builtin`, `pointer`, `bitfield`, `array`, `atomic`, `class`, `enum` and `invalid`.


  

### `schema.Type:Atomic`

```lua
schema.Type:Atomic(): string?
```

Returns the kind of an atomic type. Returns **nil** for other types. The kind is one of these values.


    
`plain` is a type without type arguments.
`t` is a type with one type argument.
`collection_of_t` is a collection of one type argument.
`tt` is a type with two type arguments.
`i` is a type with an integer argument.


  

  

### `schema.Type:Inner`

```lua
schema.Type:Inner(): schema.Type
```

Returns the inner types of the type, each as a separate return value. For a pointer, this is the type that it points to. For a fixed array, this is the type of the elements. For an atomic type with type arguments, these are the type arguments in order. For other types, nothing is returned.


| Return | Type | Description |
| --- | --- | --- |
| ... | `schema.Type` |  |


  

### `schema.Type:Count`

```lua
schema.Type:Count(): integer?
```

Returns the number of elements of a fixed array type. Returns **nil** for other types.


  

### `schema.Type:NumBits`

```lua
schema.Type:NumBits(): integer?
```

Returns the width in bits of a bitfield type. Returns **nil** for other types.


  

### `schema.Type:Flags`

```lua
schema.Type:Flags(): { value: integer, virtual_members: boolean, abstract: boolean, trivial_constructor: boolean, trivial_destructor: boolean, limited_metadata: boolean, initialized: boolean, module_local_type_scope: boolean, global_type_scope: boolean, construct_allowed: boolean, construct_disallowed: boolean, network_assume_not_networkable: boolean, network_no_base: boolean, ignore_type_scope_meta_checks: boolean, disable_data_desc_validation: boolean, entity_limited_data_desc: boolean, custom_aligned_new_delete: boolean, kv3_transfer_polymorphic_classname: boolean }?
```

Returns the flags of a class type. Returns **nil** for other types. The `value` field holds all flag bits as one number, and each boolean field holds one of the bits. The optional fields exist only in game builds whose schema defines them. In other builds they are **nil**.


  

### `schema.Type:GetScope`

```lua
schema.Type:GetScope(): schema.Scope
```

Returns the schema scope that the type belongs to.


  

<a id="schema-Type-Meta"></a>
### `schema.Type.Meta`

A table that maps metadata names to native pointers.
