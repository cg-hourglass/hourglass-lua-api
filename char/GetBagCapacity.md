<!-- Generated. DO NOT EDIT. -->
# GetBagCapacity

## Char.GetBagCapacity(CharIndex)

### 函数功能

Return the number of usable player bag slots, excluding equipment.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player or agent index.

### 返回值

Effective total slot limit minus 8; nil for an invalid or nonplayer character.

## 参考实例

```lua
local capacity = Char.GetBagCapacity(player);
```
