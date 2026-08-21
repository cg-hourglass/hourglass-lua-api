<!-- Generated. DO NOT EDIT. -->
# GetStallItemPrice

## NLG.GetStallItemPrice(CharIndex)

### 函数功能

获取玩家摆摊道具的定价表。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

目标不是玩家时返回数值 -1；否则返回一个 Lua table，下标从8开始（对应背包栏位8-27），值为该栏位道具的摆摊定价，从未摆摊过的栏位价格为0。

## 参考实例

```lua
local prices = NLG.GetStallItemPrice(player);
-- prices[8] = 0, prices[9] = 100, ...
```
