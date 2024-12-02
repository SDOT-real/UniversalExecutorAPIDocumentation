---
description: Globals for Actors and Their LuaStates
---

# 🌙 Actor

## Why actors exist?

TODO

***



## What are Luau states?

TODO

***



## Why there are these functions?

TODO

***



## getactors

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getactors(): ({Actor})

-- // Returns <Actor>: a table of all actors
```
{% endcode %}

`aliases: none!`

#### Returns a table of all actors in the game, even that are parented to nil.&#x20;

#### ❗ Warning/Limitations

Actors can be destroyed, thus hidden from this function! Use `getluastates`.

***



## getluastates

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getluastates(): ({LuaStateProxy})

-- // Returns <table>: a table of all lua states represented as LuaStateProxys
```
{% endcode %}

`aliases: getactorthreads`

#### Returns a table of all actors in the game, even the ones that are parented to nil.

***



## getgamestate

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getgamestate(): (LuaStateProxy)

-- // Returns <LuaStateProxy>: the main lua state 
```
{% endcode %}

`aliases: none!`

#### Returns the main state, where all scripts run that are not parented to an actor.

***



## getluastate

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getgamestate(target: LuaSourceContainer | Actor): (LuaStateProxy)

-- // Returns <LuaStateProxy>: the lua state where the target runs
```
{% endcode %}

`aliases: none!`

#### Returns Luau state, where the provided target runs.



***

## getcurrentstate

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getcurrentstate(): (LuaStateProxy)

-- // Returns <LuaStateProxy>: the lua state where the function was called
```
{% endcode %}

`aliases: none!`

#### Returns Luau state, where the function was called.



***

## checkparallel

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getcurrentstate(): (boolean)

-- // Returns <LuaStateProxy>: true if called in the main Luau state
```
{% endcode %}

`aliases: isgamestate`

#### Checks if the function is called in the main (game) state.

***



## run\_on\_actor

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function run_on_actor(actor: Actor, code: string, ...: string | number | Instance): (boolean)

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Runs the provided source code on the provided actor, the arguments are given to the script once ran. The arguments are limited to specific types.

***



## on\_actor\_state\_created

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
run_on_actor: ExecutorEvent<Actor>
-- // Returns <Actor>: new actor that was just created
```
{% endcode %}

`aliases: none!`

#### Executor event, which gets fired when a new actor is created, prior any script execution.

***



## Mentioned Classes

{% content-ref url="../classes/luastateproxy.md" %}
[luastateproxy.md](../classes/luastateproxy.md)
{% endcontent-ref %}

{% content-ref url="../classes/executorsignal.md" %}
[executorsignal.md](../classes/executorsignal.md)
{% endcontent-ref %}

