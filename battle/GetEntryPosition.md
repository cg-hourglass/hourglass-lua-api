<!-- Generated. DO NOT EDIT. -->
# GetEntryPosition

## Battle.GetEntryPosition(BattleIndex, CharIndex)

### 函数功能

获取对象在战场中的位置编号。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- CharIndex: [数值型](../appendix/数值型.md) 对象index，可以是玩家、宠物或敌人。

### 返回值

成功返回对象在战斗中的位置，范围 0-19，其中 0-9 为下方队列（己方），10-19 为上方队列（敌方）；失败返回 -1。

## 参考实例

```lua
local TM_Pos = Battle.GetEntryPosition(TM_BattleIndex, TM_TargetIndex);
if TM_Pos ~= -1 then
    Battle.ActionSelect(TM_CharIndex, %战斗指令_攻击%, TM_Pos, -1);
end
```

### 备注

要求对象自身记录的战斗index与第一个参数一致，否则返回 -1。
