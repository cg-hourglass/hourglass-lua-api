<!-- Generated. DO NOT EDIT. -->
# GetStallItemPrice

## NLG.GetStallItemPrice(CharIndex)

### 函数功能

获取玩家摆摊道具的定价表。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

Returns -1 for nonplayers. Otherwise returns prices keyed by the effective bag range from Char.GetBagSlotRange, including zero prices for unlisted slots. The default range remains 8..27; expanded players may include slots up to 247.

## 参考实例

```lua
local prices = NLG.GetStallItemPrice(player);
-- prices[8] = 0, prices[9] = 100, ...
```
