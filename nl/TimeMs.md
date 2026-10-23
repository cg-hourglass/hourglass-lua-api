<!-- Generated. DO NOT EDIT. -->
# TimeMs

## NL.TimeMs()

### 函数功能

Return process-shared monotonic milliseconds for short-lived schedules and clock sampling.

### 参数说明

无参数。

### 返回值

Non-negative integer milliseconds since the process clock origin.

## 参考实例

```lua
local start = NL.TimeMs() + 400;
```

### 备注

This is not Unix time. It does not jump when the system clock changes.
All Lua states use the same origin. Pair timestamps with NL.ClockId()
across connections; a process restart creates a new clock identity.
