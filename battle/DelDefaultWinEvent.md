<!-- Generated. DO NOT EDIT. -->
# DelDefaultWinEvent

## Battle.DelDefaultWinEvent(BattleIndex)

### 函数功能

删除指定战斗的引擎内建胜利事件。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

成功返回 0；战斗index非法返回 -1。

## 参考实例

```lua
Battle.DelDefaultWinEvent(TM_BattleIndex); -- 屏蔽引擎自带的战斗结算事件
```

### 备注

本函数只清除引擎内建的胜利事件回调；由 Battle.SetWinEvent 安装的 Lua 胜利回调是另一个独立槽位，
不会被本函数清除。本函数会返回 0 或 -1，并非无返回值。
