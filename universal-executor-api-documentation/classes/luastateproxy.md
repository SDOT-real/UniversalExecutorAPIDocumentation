---
description: Wrapper Around the Internal Structure of Lua State
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# ⛓️ LuaStateProxy

## Static Methods

{% code overflow="wrap" lineNumbers="true" %}
```lua
new(): (LuaStateProxy)
-- // creates a new Lua State
-- // Returns <LuaStateProxy>: a proxy for a new lua state
```
{% endcode %}

***

## Properties

<pre class="language-lua" data-overflow="wrap" data-line-numbers><code class="lang-lua"><strong>[readonly] Id: (number)
</strong><strong>-- // an identitifer for the lua state
</strong><strong>
</strong><strong>[readonly] IsActorState: (boolean)
</strong><strong>-- // whether the state was created for an actor
</strong></code></pre>

***

## Methods

{% code overflow="wrap" lineNumbers="true" %}
```lua
function GetActors(): ({Actors})
-- // Returns <Actor>: the actors associated with the state

function Execute(code: string, ...: string | number | Instance): ()
-- // Executes the code on the state and provides it with arguments
-- // argument types are limited
-- // Returns <nil>: nil
```
{% endcode %}

***

## Events

<pre class="language-lua"><code class="lang-lua"><strong>Event: (ExecutorSignal)
</strong>-- // a pre-created executor event for interstate communication
</code></pre>

***



## Mentioned Classes

{% content-ref url="executorsignal.md" %}
[executorsignal.md](executorsignal.md)
{% endcontent-ref %}

