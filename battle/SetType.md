<!-- Generated. DO NOT EDIT. -->
# SetType

## Battle.SetType(BattleIndex, Type)

### 函数功能

设置战斗类型，如普通战、PVP 战等。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Type: [数值型](../appendix/数值型.md) 新的战斗类型，取值参照战斗类型常量。

### 返回值

返回设置之前的旧战斗类型；战斗index非法返回 -1。

## 参考实例

```lua
Battle.SetType(TM_BattleIndex, %战斗_BOSS战%);
```

### 备注

可用的战斗类型常量：%战斗_普通%（1）、%战斗_PVP%（2）、%战斗_观战%（3）、%战斗_BOSS战%（5）。

本函数返回的是**旧值**而不是“1 为成功”。整个 Set 家族
（SetType/SetMod/SetNoRisk/SetGainMode）都是这个约定。
