---
description: List of Code Examples
cover: .gitbook/assets/header.png
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
    visible: false
---

# ✅ Examples

## hookfunction/clonefunction/restorefunction example

{% code lineNumbers="true" fullWidth="true" %}
```lua
-- our target that we want to hook
local function targetFunction(name: string): string
    print("im " .. name)
end

-- checking if its hooked. returns: "im untouched"
target("untouched") -- "im untouched"

local originalFunction = nil
do
    original = hookfunction(targetFunction, function(arg1)
        -- hook function has all the arguments the original function gets
        --print(arg1) -- "untouched"
        
        -- we can return whatever we what from the hook function
        -- the caller will get what we return
        -- be careful not to call yourself! it will result in a recursion, call the original instead
        return originalFunction("hooked")
    end
end

-- checking if its hooked. returns: "im hooked" after our hook
targetFunction("untouched") -- "im untouched"

-- calling the original function will give us the original behavior
originalFunction("untouched") -- "im untouched"

print(originalFunction == targetFunction) -- false
```
{% endcode %}

