<!-- Generated. DO NOT EDIT. -->
# GetBattleFieldAttribute

## Battle.GetBattleFieldAttribute(BattleIndex)

### 函数功能

获取当前战斗的战场魔法效果，如属性翻转、魔法封印。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

成功返回 3 个值，依次是战场魔法状态、状态剩余回合数、状态强度；战斗index非法时只返回一个 0。

## 参考实例

```lua
local TM_Attr, TM_Count, TM_Power = Battle.GetBattleFieldAttribute(TM_BattleIndex);
if TM_Attr == %战属_魔封% then
    print("魔法封印中，剩余 " .. TM_Count .. " 回合");
end
```

### 备注

战场状态常量：%战属_地%（1）、%战属_水%（2）、%战属_火%（4）、%战属_风%（8）、%战属_魔封%（16）。
这些是位标志，可以按位组合。
