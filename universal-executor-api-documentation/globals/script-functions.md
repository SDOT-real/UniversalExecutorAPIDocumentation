---
description: Globals for LuaSourceContainers and Functions
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# 📄 Script

## checkcaller

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function checkcaller(): (boolean)

-- // Returns <boolean>: is in executor thread
```
{% endcode %}

`aliases: none!`

#### Checks if the function is called inside executor thread. In simple words: checks if the function is called by the executor.

***



## checkcallstack

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function checkcallstack(level: number): (boolean)
-- // level <uint>: level to check above

-- // Returns <boolean>: is in executor thread
```
{% endcode %}

`aliases: none!`

#### Checks if the function is called inside executor thread and the functions above the level are owned by the executor. In simple words: checks if the function is called by the executor, but recursive.

***



## isexecutorclosure

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function isexecutorclosure(func: ()->()): (boolean)
-- // func <function>: function to check

-- // Returns <boolean>: is the function created by the executor
```
{% endcode %}

`aliases: isexecutorfunction, isourclosure, isourfunction`

#### Checks if the provided closure is created by the executor.



***

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function islclosure(func: ()->()): (boolean)
-- // func <function>: function to check

-- // Returns <boolean>: is the function a lua function
```
{% endcode %}

`aliases: none!`

#### Checks if the provided closure is a Lua closure.

***



## decompile

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function decompile(target: ()->() | LuaSourceContainer): (string)
-- // target <function OR LuaSourceContainer>: target to decompile

-- // Returns <string>: the decompiled target
```
{% endcode %}

`aliases: none!`

#### Decompiles the target, returning code that resembles the source code of the target as close as possible. Allows you to look at the code of scripts or functions.

***



## getsenv

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getsenv(script: LuaSourceContainer): ({[any]: any})
-- // script <function OR LuaSourceContainer>: script from which the environment will be taken

-- // Returns <table>: script environment
```
{% endcode %}

`aliases: none!`

#### Returns the environment of a script, allowing modification of globals in that script.

#### ❗ Warning/Limitations

Be careful when modifying the script environment! The script may check for any modifications and detect you!

***



## getscriptfunction

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getscriptfunction(script: LuaSourceContainer): (()->())
-- // script <LuaSourceContainer>: script from which the main function will be extracted from

-- // Returns <function>: script main function
```
{% endcode %}

`aliases: getscriptclosure`

#### Returns the main function of the script, allowing you to examine the functions with the debug library.

#### ❗ Warning/Limitations

It's not the best idea to call this function! This will most likely not work as expected.



***

## getscriptbytecode

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getscriptbytecode(script: LuaSourceContainer): (string)
-- // script <LuaSourceContainer>: script from which the bytecode will be extracted from

-- // Returns <string>: script bytecode
```
{% endcode %}

`aliases: getbytecode, dumpbytecode, dumpstring`

#### Returns the bytecode of the script, allowing disassembly of it.



***

## getfunctionbytecode

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getfunctionbytecode(func: ()->()): (string)
-- // func <()->()>: function from which the bytecode will be extracted from

-- // Returns <string>: function bytecode
```
{% endcode %}

`aliases: getbytecode, dumpbytecode, dumpstring`

#### Returns the bytecode of the function, allowing disassembly of it.

***



## getfunctionhash

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getfunctionhash(func: ()->()): (string)
-- // func <LuaSourceContainer>: function from which the hash will be extracted from

-- // Returns <string>: function bytecode
```
{% endcode %}

`aliases: none!`

#### Returns the hash of the function, allowing for function identification or change detection.

***



## getscripthash

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getscripthash(script: LuaSourceContainer): (string)
-- // script <LuaSourceContainer>: script from which the hash will be extracted from

-- // Returns <string>: script bytecode
```
{% endcode %}

`aliases: none!`

#### Returns the hash of the script, allowing for script identification or change detection.



***

## getcallingscript

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getcallingscript(): (LuaSourceContainer?)

-- // Returns <LuaSourceContainer?>: the script which called the function or nil if couldn't find
```
{% endcode %}

`aliases: none!`

#### Attempts to find the script, which called the function in which the getcallingscript is called. Useful for checking the caller inside hooks.
