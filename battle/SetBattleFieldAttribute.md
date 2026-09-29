<!-- Generated. DO NOT EDIT. -->
# SetBattleFieldAttribute

## Battle.SetBattleFieldAttribute(BattleIndex, Attribute, TurnCount, AttributePower)

### 函数功能

设置当前战斗的战场魔法效果，如属性翻转、魔法封印。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Attribute: [数值型](../appendix/数值型.md) 战场状态，取值见备注中的战场状态常量，可按位组合。
- TurnCount: [数值型](../appendix/数值型.md) 状态持续回合数。
- AttributePower: [数值型](../appendix/数值型.md) 状态强度。

### 返回值

成功返回 3 个值，依次是写入后的战场魔法状态、持续回合数、状态强度；战斗index非法时只返回一个 0。

## 参考实例

```lua
Battle.SetBattleFieldAttribute(TM_BattleIndex, %战属_魔封%, 5, 100); -- 魔法封印 5 回合
```

### 备注

战场状态常量：%战属_地%（1）、%战属_水%（2）、%战属_火%（4）、%战属_风%（8）、%战属_魔封%（16）。
