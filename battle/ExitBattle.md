<!-- Generated. DO NOT EDIT. -->
# ExitBattle

## Battle.ExitBattle(CharIndex)

### 函数功能

强制让指定对象退出当前所在的战斗。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index，必须正处于战斗中。

### 返回值

1 成功；0 战斗引擎拒绝；-1 对象index无效，或对象不在战斗中／战斗index非法。

## 参考实例

```lua
Battle.ExitBattle(TM_CharIndex);
```

### 备注

**1 为成功**，不是“0 为成功”，判断请勿写反。

要让一个战斗已结束的角色彻底脱离战斗（常见于离线挂机角色），请使用
Battle.FinishPlayerBattle。
