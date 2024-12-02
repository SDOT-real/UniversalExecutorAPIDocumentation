---
description: Every Global Designed for Tables and Userdatas
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# 📥 Table

## getrawmetatable

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrawmetatable(object: {} | userdata): ({}?)
-- // object <table OR userdata>: object to extract original metatable from

-- // Returns <table OR nil>: metatable of object
```
{% endcode %}

`aliases: debug.getmetatable`

#### Gets the metatable of the provided object, ignoring `__metatable` metamethod. Useful for acquiring metamethods even when the metatable is protected with `__metatable`.

#### ❗ Warning/Limitations

Metatables can still have metatables in them! Be sure to check it or use raw functions `(rawget, rawequals, etc.)` and use `__iter`-proof table iteration.

Instead of using this function to get the metatable and replace any metatable field with a new function, use `hookmetamethod`.

***



## setrawmetatable

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrawmetatable(object: {} | userdata, value: {}?): ({}?)
-- // object <table OR userdata>: object to change the metatable of
-- // value <table OR nil>: new metatable of object

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: debug.setmetatable`

#### Sets the metatable of object to a new value, ignoring `__metatable` metamethod.

#### ❗ Warning/Limitations

Be careful when replacing metatables! There may be employed various detection methods!

***



## setreadonly

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function setreadonly(table: {}, flag: boolean): (boolean)
-- // table <table>: table to change the readonly flag of
-- // state <boolean>: new readonly flag for the provided object

-- // Returns <boolean>: previous readonly flag
```
{% endcode %}

`aliases: makewriteable, makereadonly`

#### Changes the readonly (freezed) flag of the provided table. (with flag `false`: opposite of table.freeze)

#### ❗ Warning/Limitations

Be careful when using this function as it is very easy to check if the table is readonly (freezed).

***



## isreadonly

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function isreadonly(table: {}): (boolean)
-- // table <table>: table to check the readonly flag of

-- // Returns <boolean>: readonly flag of the provided table
```
{% endcode %}

`aliases: none!`

#### Checks the readonly (freezed) flag of the provided table.

***



## setuntouched

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function setuntouched(env: {}, flag: boolean): (boolean)
-- // table <table>: environment to set the untouched flag of
-- // flag <boolean>: new untouched flag

-- // Returns <boolean>: previous untouched flag of the provided environment
```
{% endcode %}

`aliases: setsafeenv`

#### Sets a Luau table's untouched flag. This flag is relevant to certain Luau optimizations, namely built-ins. If true, "built-in" globals such as `game` or `print` are fetched from a cache and cannot be modified. If false, the cache is disabled and built-ins are fetched from the environment table as normal. Functions `getfenv` and `setfenv` set this flag to false implicitly. Untouched flag is the safeenv flag (needs confirmation). In simple words: allows you to modify the environment even if it is "protected".

***



## isuntouched

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function setuntouched(env: {}): (boolean)
-- // table <table>: environment to check the untouched flag of

-- // Returns <boolean>: untouched flag of the provided environment
```
{% endcode %}

`aliases: getsafeenv`

#### Returns the untouched (safeenv) flag of the provided environment.
