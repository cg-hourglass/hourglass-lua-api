<!-- Generated. DO NOT EDIT. -->
# AddItemLimit

## Char.AddItemLimit(CharIndex, Delta)

### 函数功能

Grant additional total player item slots.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player or agent index.
- Delta: [数值型](../appendix/数值型.md) Positive number of slots to add.

### 返回值

Effective total slots including equipment; nil for an invalid or nonplayer character.

## 参考实例

```lua
local total = Char.AddItemLimit(player, 20);
```

### 备注

Nonpositive deltas do nothing. Grants clamp at the configured maximum without overflow.
Newly opened slots synchronize through original I records, including persisted items previously hidden by configuration.
Char.SetData(index, 32, value) retains its old-value return and also notifies actual capacity growth.
