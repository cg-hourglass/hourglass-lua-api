<!-- Generated. DO NOT EDIT. -->
# GetTargetSelect

## Battle.GetTargetSelect(BattleIndex, AttackerIndex, TargetIndex)

### 函数功能

根据进攻者与目标在战场中的位置，换算出可直接用于战斗指令的目标参数。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- AttackerIndex: [数值型](../appendix/数值型.md) 进攻者的对象index，可以是玩家、宠物或敌人。
- TargetIndex: [数值型](../appendix/数值型.md) 目标的对象index，可以是玩家、宠物或敌人。

### 返回值

可直接作为 Battle.ActionSelect / Battle.UseTech 目标参数使用的位置值；任一对象无效或不属于该场战斗时返回 -1。

## 参考实例

```lua
local TM_Target = Battle.GetTargetSelect(TM_BattleIndex, TM_Attacker, TM_Victim);
if TM_Target ~= -1 then
    Battle.ActionSelect(TM_Attacker, %战斗指令_攻击%, TM_Target, -1);
end
```

### 备注

两个对象都必须记录着与第一个参数相同的战斗index，否则返回 -1。
