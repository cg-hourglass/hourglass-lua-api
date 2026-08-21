<!-- Generated. DO NOT EDIT. -->
# GetTurn

## Battle.GetTurn(BattleIndex)

### 函数功能

获取战斗当前的回合数。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

当前回合数；战斗index非法返回 -1。

## 参考实例

```lua
print("turn = " .. Battle.GetTurn(TM_BattleIndex));
```
