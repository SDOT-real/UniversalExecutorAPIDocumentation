---
description: Every Reflection-Related Global
cover: ../../.gitbook/assets/header.png
coverY: 0
---

# 🪞 Reflection

## getproperties

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getproperties(instance: Instance): ({[string]: any})
-- // toHook <Instance>: instance to get properties of

-- // Returns <table>: list of properties and their values of the provided instance
```
{% endcode %}

`aliases: none!`

#### Returns a list of properties of the provided instance. Useful for custom instance saving.

***



## gethiddenproperties

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function gethiddenproperties(instance: Instance): ({[string]: any})
-- // instance <Instance>: instance to get hidden properties of

-- // Returns <table>: list of hidden properties and their values of the provided instance
```
{% endcode %}

`aliases: none!`

#### Returns a list of hidden properties of the provided instance. Useful for custom instance saving.

***



## setscriptable

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function setscriptable(instance: Instance, property: string, flag: boolean): (boolean)
-- // instance <Instance>: instance which has the provided property
-- // property <string>: property to change the scriptable flag of
-- // flag <boolean>: what state the flag should be

-- // Returns <boolean>: the previous state of the flag
```
{% endcode %}

`aliases: none!`

#### Changes the "scriptable" flag of the provided property of the instance. Non-scriptable properties cannot be changed from the Luau scripts. This function changes the flag, allowing scripts to change the property. Returns the previous state of the flag.

#### ❗ Warning/Limitations

By changing the flag to `true`, you are allowing every single script in the game to change the property! This behavior can lead to detections, use this function carefully! Check out gethiddenproperty/sethiddenproperty.

***



## gethiddenproperty

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function gethiddenproperty(instance: Instance, property: string): (any)
-- // instance <Instance>: instance which has the provided property
-- // property <string>: the name of the property

-- // Returns <any>: property value
```
{% endcode %}

`aliases: none!`

#### Safely reads any non-scriptable property of the provided instance. Able to safely read even binary types!

***



## sethiddenproperty

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function gethiddenproperty(instance: Instance, property: string, value: any): (nil)
-- // instance <Instance>: instance which has the provided property
-- // property <string>: the name of the property
-- // value <any>: new value to set the property to

-- // Returns <nil>: nil
```
{% endcode %}

`aliases: none!`

#### Safely writes any non-scriptable property.

***



## getcallbackvalue

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getcallbackvalue(instance: Instance, callbackName: string): ((()->())?)
-- // instance <Instance>: instance which has a callback with the provided callback name
-- // callbackName <string>: the name of the callback

-- // Returns <function OR nil>: the callback if exists
```
{% endcode %}

`aliases: getcallbackmember`

#### Returns the value of the a callback with the provided callback name. Useful for hooking callbacks.

***



## getpcd

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getpcd(mesh: TriangleMeshPart): (string, string)
-- // mesh <TriangleMeshPart>: what triangle mesh part to read

-- // Returns <string, string>: the hash and the data of the mesh
```
{% endcode %}

`aliases: getpcdprop`

#### Returns TriangleMeshPart's PhysicalConfigData property value and the hash as the first return value.

***



## getbspval

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getbspval(instance: Instance, property: string, base64: boolean?): (string, string)
-- // instance <Instance>: what instance to read from
-- // property <string>: name of the property to read from

-- // Returns <string, string>: the data of the mesh
```
{% endcode %}

`aliases: getbsp`

#### Reads BinaryString properties with toggleable base64 encoding. (encoding part needs confirmation)

***



## getsignalmember

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getsignalmember(instance: Instance, property: string, base64: boolean?): (string, string)
-- // instance <Instance>: what instance to get a new signal from
-- // property <string>: name of the signal

-- // Returns <RBXScriptSignal>: new unrestricted signal
```
{% endcode %}

`aliases: none!`

#### Creates an unrestricted signal object for any event in the provided instance. Useful for connecting to conventionally non-scriptable signals.

***



## getrendersteppedlist()

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```lua
function getrendersteppedlist(): ({{
    Name: string,
    RenderPriority: number,
    Function: ()->()
}})

-- // Returns <table>: a list of tables that contains information about the connected renderstepped bind
```
{% endcode %}

`aliases: none!`

#### Returns a table of renderstepped binds that are created with RunService:BindToRenderStep().
