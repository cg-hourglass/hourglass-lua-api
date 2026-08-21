<!-- Generated. DO NOT EDIT. -->
# SetNextBattle

## Battle.SetNextBattle(BattleIndex, Flg)

### 函数功能

设置连战（本场战斗结束后接续下一场）。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Flg: [数值型](../appendix/数值型.md) 连战标志。设置为 -1 表示取消连战；其他值会通过 NL.RegBattleNextEnemyEvent 注册的回调函数传出。

### 返回值

1 成功，0 战斗index非法。

## 参考实例

```lua
Battle.SetNextBattle(TM_BattleIndex, 1);  -- 开启连战，标志值 1
Battle.SetNextBattle(TM_BattleIndex, -1); -- 取消连战
```

### 备注

Flg 为 -1 时同时清空引擎内建的连战设置与脚本侧记录的连战标志；其他值会把引擎内建连战
设置从“未设置”改为“已设置”，再把标志值写入脚本侧记录的字段。
