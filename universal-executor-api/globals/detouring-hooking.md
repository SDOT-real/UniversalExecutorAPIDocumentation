---
description: Detouring-related globals in the environment
cover: ../../.gitbook/assets/header.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# ↩️ Detouring

## hookfunction

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function hookfunction<Original>(toHook: Original & ()->(), hook: ()->(), hookFilter: FilterBase?): (Original & ()->())
-- // toHook <function>: function to hook
-- // hook <function>: function to hook with
-- // hookFilter <FilterBase> <optional?>: a filter for the hook

-- // Returns <function>: original function
```
{% endcode %}

`aliases: detourfunction, hookclosure`

#### Hooks the function "toHook" and replaces it to function "hook", mitigating detections.&#x20;

#### ❗ Warning/Limitations

Instead of using this function for metamethod/proto/signal hooking, look at functions, designed for the corresponding data type!

The original returned function will be a clone of the original function. Comparison will return `false`.

Be careful not to call the function you hook in the hook itself! It will result in a recursion. Call the original instead.

Be careful when accessing the arguments! They may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables. Be sure to deep-clone data you save with cloneref and other methods.

***



## hookmetamethod

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function hookmetamethod<Original>(toHook: userdata | {}, metamethod: string, hook: ()->(), argGuard: boolean?, hookFilter: FilterBase?): (Original & ()->())
-- // toHook <userdata OR table>: function to hook
-- // metamethod <string>: metamethod string
-- // hook <function>: function to hook with
-- // argGuard <boolean> <default: false> <optional?>: the hook will only be called if the metamethod call has valid arguments, protecting from detections
-- // hookFilter <FilterBase> <optional?>: a filter for the hook

-- // Returns <function>: original function
```
{% endcode %}

`aliases: none!`

#### Hooks a metamethod "metamethod" of "toHook"s metatable, replacing it with "hook", mitigating detections.&#x20;

#### ❗ Warning/Limitations

The returned function will be a clone of the original function. Comparison will return `false`.

Be careful not to call the function you hook in the hook itself! It will result in a recursion. Call the original instead.

Be careful when accessing the arguments! They may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables. Be sure to deep-clone data you save with cloneref and other methods.

***



## hookproto

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function hookproto(toHook: ProtoProxy, hook: ()->()): (nil)
-- // toHook <ProtoProxy>: proto to hook
-- // hook <function>: function to hook with

-- // Returns: none!
```
{% endcode %}

`aliases: none!`

#### Hooks a proto "toHook", replacing it with function "hook", allowing for hooking future closures created from that proto.

#### ❗ Warning/Limitations

Be careful not to call the function you hook in the hook itself! It will result in a recursion. Call the original instead.

Be careful when accessing the arguments! They may contain metamethods that can detect you! Use raw functions (rawset, rawequals, etc.) for safety and `__iter`-proof methods of looping through tables. Be sure to deep-clone data you save with cloneref and other methods.

***



## restorefunction

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function restorefunction(toRestore: ()->()): (nil)
-- // toRestore <function>: function to restore

-- // Returns: none!
```
{% endcode %}

`aliases: unhookfunction`

#### Unhooks the function.

***



## restoreproto

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function restoreproto(toRestore: ProtoProxy): (nil)
-- // toRestore <function>: proto to restore

-- // Returns: none!
```
{% endcode %}

`aliases: unhookproto`

#### Unhooks the proto.

***



## isfunctionhooked

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function isfunctionhooked(func: ()->()): (boolean)
-- // func <function>: function to check

-- // Returns <boolean>: true if hooked
```
{% endcode %}

`aliases: none!`

#### Checks if the function is hooked, returns true if it is.

***



## isprotohooked

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function isprotohooked(proto: ProtoProxy): (boolean)
-- // proto <ProtoProxy>: proto to check

-- // Returns <boolean>: true if hooked
```
{% endcode %}

`aliases: none!`

#### Checks if the proto is hooked, returns true if it is.

***



## clonefunction

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function clonefunction<Original>(toClone: Original & ()->()): (Original & ()->())
-- // toClone <function>: function to clone

-- // Returns <function>: function clone
```
{% endcode %}

`aliases: none!`

#### Copies function "toClone".

#### ❗ Warning/Limitations

The clone is not the same function you cloned! Comparison will return `false`.

If the cloned function is hooked, the clone will not be hooked! The clone and the original are two different functions!

***



## newcclosure

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function newcclosure<Original>(toWrap: Original & ()->(), name: string?): (Original & ()->())
-- // toWrap <function>: function to wrap
-- // name <string> <optional?>: cclosure name

-- // Returns <function>: wrapped function inside a cclosure
```
{% endcode %}

`aliases: none!`

#### Wraps the function "toWrap" into a C closure. The cclosure is a proxy for the "toWrap" function, if simplified.

#### ❗ Warning/Limitations

The new CClosure you created is not the same function you wrapped! Comparison will return `false`.

If the cclosure is hooked, the original will not be hooked! The cclosure and the original are two different functions!

***



## setstackhidden

<pre class="language-lua" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-lua"><strong>function setstackhidden(func: ()->(), hidden: boolean?): (boolean)
</strong>-- // func &#x3C;function>: function to hide
-- // hidden &#x3C;boolean> &#x3C;default: true> &#x3C;optional?>: hidden state

-- // Returns &#x3C;boolean>: returns true if it was hidden, false if not

-- OR

function setstackhidden(stackIndex: number, hidden: boolean?): (boolean)
-- // stackIndex &#x3C;uint>: function in the current callstack under stackIndex to hide
-- // hidden &#x3C;boolean> &#x3C;default: true> &#x3C;optional?>: hidden state

-- // Returns &#x3C;boolean>: returns true if it was hidden, false if not
</code></pre>

`aliases: none!`

#### Hides the function from the callstack and returns it's previous hidden state.&#x20;



***



## Classes

{% content-ref url="../classes/protoproxy.md" %}
[protoproxy.md](../classes/protoproxy.md)
{% endcontent-ref %}

