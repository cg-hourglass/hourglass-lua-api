<!-- Generated. DO NOT EDIT. -->
# ClockId

## NL.ClockId()

### 函数功能

Return the process clock identity shared by all Lua states.

### 参数说明

无参数。

### 返回值

A 32-character lowercase hexadecimal boot identifier.

## 参考实例

```lua
local sample = { boot = NL.ClockId(), ms = NL.TimeMs() };
```

### 备注

Generated from 128 random bits once at process initialization. It is
constant within one process and independent of account or session identity.
