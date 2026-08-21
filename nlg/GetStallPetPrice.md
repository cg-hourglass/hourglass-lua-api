<!-- Generated. DO NOT EDIT. -->
# GetStallPetPrice

## NLG.GetStallPetPrice(CharIndex)

### 函数功能

获取玩家摆摊宠物的定价表。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

目标不是玩家时返回数值 -1；否则返回一个 Lua table，下标0到4（对应5个宠物栏位），值为该栏位宠物的摆摊定价，从未摆摊过的栏位价格为0。

## 参考实例

```lua
local prices = NLG.GetStallPetPrice(player);
-- prices[0] = 0, prices[1] = 99999, ...
```
