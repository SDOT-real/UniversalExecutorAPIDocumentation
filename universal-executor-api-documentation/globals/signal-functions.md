---
description: Globals for Expanded Signal and Connection Control
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# 🎊 Signal

## getconnections

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getconnections(signal: RBXScriptSignal): ({RBXScriptConnection})
-- // signal <RBXScriptSignal>: signal to get connections from

-- // Returns <table>: a list of tables that represent connections
```
{% endcode %}

`aliases: none!`

#### Returns a list callbacks of every single connection of the signal. Useful for disabling connections, firing them individually, etc.&#x20;

***



## firesignal

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function firesignal(signal: RBXScriptSignal, ...: any): (nil)
-- // signal <RBXScriptSignal>: signal to fire
-- // vararg... <any>: arguments to fire signal with

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Fires the provided signal on the client with the provided arguments.&#x20;

#### ❗ Warning/Limitations

Be careful when firing signals! There may be sanity checks that will detect if nothing has changed in the game! Consider reverse engineering the game first before firing.

Only Luau connections are fired.&#x20;

***



## cfiresignal

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function cfiresignal(signal: RBXScriptSignal, ...: any): (nil)
-- // signal <RBXScriptSignal>: signal to fire

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Fires the provided signal on the client with the provided arguments.

#### ❗ Warning/Limitations

Argument types should have the right arguments! Check out `getsignalarguments`.

Only engine (C) connections are fired.

***



## replicatesignal

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function replicatesignal(signal: RBXScriptSignal, ...: any): (nil)
-- // signal <RBXScriptSignal>: signal to replicate
-- // vararg... <any>: arguments to fire signal with

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Replicates (fires) the provided signal on the server with the provided arguments.

#### ❗ Warning/Limitations

Argument types should have right arguments! Check out `getsignalarguments`.

Signal must be replicable! Check out `cansignalreplicate`.

***



## cansignalreplicate

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function cansignalreplicate(signal: RBXScriptSignal): (boolean)
-- // signal <RBXScriptSignal>: signal to check

-- // Returns <boolean>: can signal replicate or not
```
{% endcode %}

`aliases: none!`

#### Checks if the provided signal can replicate to server.

***

## getsignalarguments

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getsignalarguments(signal: RBXScriptSignal): ({string})
-- // signal <RBXScriptSignal>: signal to check

-- // Returns <table>: a list of argument types
```
{% endcode %}

`aliases: none!`

#### Returns a list of types as strings which the provided signal accepts.

***



## hooksignal <a href="#hooksignal" id="hooksignal"></a>

<pre class="language-lua" data-overflow="wrap" data-line-numbers><code class="lang-lua">function hooksignal(signal: RBXScriptSignal, callback: (info: {
    Connection: RBXScriptConnection, -- // the connection itself
    Index: number, -- // the index of the connection, connections are connected in a specific order
    Function: ()->(), -- // connected function
    Thread: thread -- // connected thread
}, ...: any)->(
<strong>    boolean, -- // should the connection be invoked?
</strong>    ...any -- // arguments for the connection
)): (nil)
-- // signal &#x3C;RBXScriptSignal>: signal to hook
-- // callback &#x3C;function>: function to hook signal with

-- Returns &#x3C;nil>: nil
</code></pre>

`aliases: none!`

#### Enables the interception (detouring/hooking) of a signal. When signal is fired, callback is called for every _Lua_ connection in signal with an information table and the invocation arguments.

***



## restoresignal <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function restoresignal(signal: RBXScriptSignal): (nil)
-- // signal <RBXScriptSignal>: signal to restore from hooksignal

-- Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Restores the original behavior of the provided signal. In simple words: unhooks the provided signal.

***



## issignalhooked <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function issignalhooked(signal: RBXScriptSignal): (boolean)
-- // signal <RBXScriptSignal>: signal to check

-- Returns <boolean>: is signal hooked or not
```
{% endcode %}

`aliases: none!`

#### Returns a boolean, which indicates if the provided signal is hooked or not.

***



## isconnectionenabled <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function isconnectionenabled(connection: RBXScriptConnection): (boolean)
-- // connection <RBXScriptConnection>: connection to check

-- Returns <boolean>: is connection enabled or not
```
{% endcode %}

`aliases: none!`

#### Checks if the connection is enabled internally or not.

***



## setconnectionenabled <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function setconnectionenabled(connection: RBXScriptConnection, state: boolean): (nil)
-- // connection <RBXScriptConnection>: connection which will be enabled/disabled
-- // state <boolean>: new state of the connection

-- Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Changes if the connection is disabled or enabled internally.

***



## isluaconnection <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function isluaconnection(connection: RBXScriptConnection): (boolean)
-- // connection <RBXScriptConnection>: connection to check

-- Returns <boolean>: is connection a Luau connection
```
{% endcode %}

`aliases: none!`

#### Checks if the provided connection is a Luau connection.

***



## iswaitingconnection <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function iswaitingconnection(connection: RBXScriptConnection): (boolean)
-- // connection <RBXScriptConnection>: connection to check

-- Returns <boolean>: is connection a waiting connection
```
{% endcode %}

`aliases: none!`

#### Checks if the provided connection is a waiting connection (the result of a :Wait() call).

***



## isgamescriptconnection <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function iswaitingconnection(connection: RBXScriptConnection): (boolean)
-- // connection <RBXScriptConnection>: connection to check

-- Returns <boolean>: is connection not a core script connection
```
{% endcode %}

`aliases: none!`

#### Checks if the provided connection is not a CoreScript connection.

***



## isgamescriptconnection <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function iswaitingconnection(connection: RBXScriptConnection): (boolean)
-- // connection <RBXScriptConnection>: connection to check

-- Returns <boolean>: is connection not a core script connection
```
{% endcode %}

`aliases: none!`

#### Checks if the provided connection is not a CoreScript connection.

***



## getconnectionfunction <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function getconnectionfunction(connection: RBXScriptConnection): (any)
-- // connection <RBXScriptConnection>: connection to get the callback of

-- Returns <any>: connection function or any other connected callback
```
{% endcode %}

`aliases: getconnectioncallback`

#### Returns the connected callback of the connection.

#### ❗ Warning/Limitations

The provided connection must be a Luau and not a CoreScript connection!

It's possible that not only scripts are connected to the connection! Add type checking in your code when working with this function!

***



## getconnectionthread <a href="#hooksignal" id="hooksignal"></a>

{% code overflow="wrap" lineNumbers="true" %}
```lua
function getconnectionfunction(connection: RBXScriptConnection): (thread)
-- // connection <RBXScriptConnection>: connection to get the callback of

-- Returns <thread>: thread of the connection
```
{% endcode %}

`aliases: none!`

#### Returns the thread of the connection..

#### ❗ Warning/Limitations

The provided connection must be a Luau connection!
