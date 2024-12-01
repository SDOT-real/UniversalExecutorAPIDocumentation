---
description: LuaState environment-related globals
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# ☄️ Environment

## Environment Hierarchy

1. function environment `(getfenv(func) or getfenv(1))`
2. thread environment `(gettenv(thread) or gettenv(coroutine.running()))`
3. script environment `(getsenv(script) or getfenv(0))`

#### In executors:

4. executor environment `(getgenv())`
5. Roblox environment `(getrenv())`

#### In RobloxScripts:

5. Roblox environment `(getrenv())`

These environments are basically chained. If there is a value in different environments with the same keys, you will get the value from the lowest environment. For example: there are 2 different requires: in Roblox environment (5) and in executor environment (4), you (from your executor script) will get the value from the lowest (4<5) environment.



***



## getgenv

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getgenv(): ({[any]: any})

-- // Returns <table>: the global environment
```
{% endcode %}

`aliases: none!`

#### Returns the global (executor) environment.

***



## getrenv

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrenv(): ({[any]: any})

-- // Returns <table>: the Roblox environment
```
{% endcode %}

`aliases: none!`

#### Returns the Roblox (original) environment.

#### ❗ Warning/Limitations

Be careful when modifying the Roblox environment! The scripts can check for modifications and detect you!

***



## gettenv

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrenv(targetThread: thread): ({[any]: any})

-- // Returns <table>: the thread environment
```
{% endcode %}

`aliases: none!`

#### Returns the thread environment.

#### ❗ Warning/Limitations

Be careful when modifying the thread environment! A script can check for modifications and detect you!

***



## getsafeenv

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrenv(env: {}): (boolean)
-- // env <table>: environment to check

-- // Returns <boolean>: is the environment flagged as safe
```
{% endcode %}

`aliases: issafeenv`

#### Checks if the environment provided is flagged as safe inside Luau internals.

***



## getreg

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getreg(): ({thread | {} | ()->() | number})

-- // Returns <table>: the luau registry
```
{% endcode %}

`aliases: debug.getregistry`

#### Returns the Luau registry. Useful for acquiring threads (coroutines) and some functions, tables.

#### ❗ Warning/Limitations

Be careful not to modify this table! It can lead to undefined behavior! (needs to be checked)

Be careful when accessing the tables and userdatas! They may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables.

***



## getgc

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getgc(includeUserdata: false?): ({()->()})
-- // includeUserdata <boolean> <optional?>: should the table include tables and userdata?

-- // Returns <table>: table with all garbage collected functions

-- // OR

function getgc(includeUserdata: true): ({{} | ()->() | userdata})
-- // includeUserdata <boolean> <optional?>: should the table include tables and userdata?

-- // Returns <table>: table with all garbage collected items
```
{% endcode %}

`aliases: none!`

#### Returns a table with all garbage collected functions. If provided with `includeTables = true`, the table will also contain tables and userdata.

#### ❗ Warning/Limitations

Be careful not to modify this table! It can lead to undefined behavior! (needs to be checked)

Be careful when accessing the tables and userdatas! They may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables.



***



## filtergc

<pre class="language-lua" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-lua"><strong>function filtergc&#x3C;T>(type: string, options: {}, returnOne: false?): ({T})
</strong>-- // type &#x3C;string>: data type which should be looked for
-- // options &#x3C;table>: the options for filters
-- // returnOne &#x3C;boolean> &#x3C;optional?>: should the function return only the first match or all matches?

-- // Returns &#x3C;table>: table of matches

-- // OR

function filtergc&#x3C;T>(type: string, options: {}, returnOne: true): (T)
-- // type &#x3C;string>: data type which should be looked for
-- // options &#x3C;table>: the options for filters
-- // returnOne &#x3C;boolean> &#x3C;optional?>: should the function return only the first match or all matches?

-- // Returns &#x3C;any OR nil>: the first match or nil if not found
</code></pre>

`aliases: none!`

#### Filters the GC for value(s) with defined filters. More performant because of the implementation in C.

**Options for table type**:

<table><thead><tr><th width="162">Key</th><th width="387">Description</th><th width="81">Default</th><th>Type</th></tr></thead><tbody><tr><td>Keys</td><td>If not empty, only include tables with keys corresponding to all values in this table</td><td>nil</td><td>{any}</td></tr><tr><td>Values</td><td>If not empty, only include tables with values corresponding to all values in this table</td><td>nil</td><td>{any}</td></tr><tr><td>KeyValuePairs</td><td>If not empty, only include tables with keys/value pairs corresponding to all values in this table</td><td>nil</td><td>{[any]: any}</td></tr><tr><td>Metatable</td><td>If not empty, only include tables with the metatable passed</td><td>nil</td><td>{}</td></tr></tbody></table>

**Options for function type**:

<table><thead><tr><th width="161">Key</th><th width="388">Description</th><th>Default</th><th>Type</th></tr></thead><tbody><tr><td>Name</td><td>If not empty, only include functions with this name</td><td>nil</td><td>string</td></tr><tr><td>Constants</td><td>If not empty, only include functions with constants that match all values in this table</td><td>nil</td><td>{any}</td></tr><tr><td>Upvalues</td><td>If not empty, only include functions with upvalues that match all values in this table</td><td>nil</td><td>{any}</td></tr><tr><td>IgnoreExecutor</td><td>If false, do not ignore executor functions</td><td>true</td><td>boolean</td></tr></tbody></table>

#### ❗ Warning/Limitations

Be careful not to modify this table! It can lead to undefined behavior! (needs to be checked)

Be sure to check if the value is not nil!

Be careful when accessing the data! It may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables. Be sure to deep-clone data you save with cloneref and other methods.

***



## getnilinstances

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getnilinstances(): ({Instance})

-- // Returns <table>: table with all instances that are parented to nil
```
{% endcode %}

`aliases: none!`

#### Returns a table with all instances that are parented to nil. Useful for acquiring hidden instances.

#### ❗ Warning/Limitations

Be sure to deep-clone data you save with cloneref and other methods to avoid detections!

***



## getscripts

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getscripts(): ({LuaSourceContainer})

-- // Returns <table>: table with all scripts in the game, including that are parented to nil
```
{% endcode %}

`aliases: none!`

#### Returns a table with all scripts of the game. Useful for faster looping through the scripts.

#### ❗ Warning/Limitations

Be sure to deep-clone data you save with cloneref and other methods to avoid detections!

***



## getloadedmodules

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getloadedmodules(): ({ModuleScript})

-- // Returns <table>: table with all loaded modules
```
{% endcode %}

`aliases: none!`

#### Returns a table of all loaded modules. Useful for checking if the module is loaded or not.

#### ❗ Warning/Limitations

Be sure to deep-clone data you save with cloneref and other methods to avoid detections!



***

## fireclickdetector

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function fireclickdetector(detector: ClickDetector): (nil)
-- // detector <ClickDetector>: the detector which should be triggered

-- // Returns: nil
```
{% endcode %}

`aliases: none!`

#### Triggers a click detector on client and server if possible.



***

## fireproximityprompt

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function fireproximityprompt(prompt: ProximityPrompt): (nil)
-- // prompt <ProximityPrompt>: the proximity rompt which should be triggered

-- // Returns: nil
```
{% endcode %}

`aliases: none!`

#### Triggers a proximity prompt on client and server if possible.



***

## firetouchinterest

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function firetouchinterest(toTouch: BasePart | TouchInterest, touchWith: BasePart, toggle: boolean): (nil)
-- // toTouch <BasePart OR TouchInterest>: the target which should be touched
-- // touchWith <BasePart>: base part to touch with
-- // toggle <boolean>: is the touch ending or starting?

-- // Returns: nil
```
{% endcode %}

`aliases: none!`

#### Triggers a touch event for base part or touch interest "toTouch" with base part "touchWith" on client and server if possible. Boolean "toggle" is responsible for deciding if Touched or TouchEnded should be triggered. Triggers on client and server if possible.
