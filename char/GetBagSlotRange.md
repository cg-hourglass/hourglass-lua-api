<!-- Generated. DO NOT EDIT. -->
# GetBagSlotRange

## Char.GetBagSlotRange(CharIndex)

### 函数功能

Return the effective player bag slot range.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player or agent index.

### 返回值

Two integers, 8 and effective total slot limit minus 1; nil for an invalid or nonplayer character.

## 参考实例

```lua
local first, last = Char.GetBagSlotRange(player);
```

### 备注

Equipment slots 0..7 are excluded. The upper bound is inclusive.
