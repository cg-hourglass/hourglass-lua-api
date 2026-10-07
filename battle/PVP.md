<!-- Generated. DO NOT EDIT. -->
# PVP

## Battle.PVP(CharIndex1, CharIndex2)

### 函数功能

在两个玩家之间创建一场 PK 战斗。

### 参数说明

- CharIndex1: [数值型](../appendix/数值型.md) 战斗一方玩家的对象index。
- CharIndex2: [数值型](../appendix/数值型.md) 战斗另一方玩家的对象index。

### 返回值

成功返回战斗index；-1 对象index无效或不是玩家；-2 其中一方已经在战斗中；-4 战斗引擎创建失败，或任意一方是代理角色、任意一方的队伍里有代理角色。

## 参考实例

```lua
local TM_BattleIndex = Battle.PVP(TM_Player1, TM_Player2);
if TM_BattleIndex >= 0 then
    Battle.SetNoRisk(TM_BattleIndex, 1); -- 无风险 PK
end
```

### 备注

两个对象都必须是 %对象类型_人% 且战斗状态为 %战斗状态_无%，否则直接失败；失败原因见上方返回值说明的 -1/-2/-4 区分。

代理角色不能参加玩家之间的战斗：参战的任意一方本身是代理角色，或者其队伍里有代理角色时，一律返回 -4。
本限制是本服务端新增的，C 版 gmsv 没有代理角色。
