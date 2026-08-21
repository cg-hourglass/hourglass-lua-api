<!-- Generated. DO NOT EDIT. -->
# SetNoRisk

## Battle.SetNoRisk(BattleIndex, Mod)

### 函数功能

设置战斗的 NoRisk（无风险）标志。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Mod: [数值型](../appendix/数值型.md) 0 或 1。

### 返回值

返回设置之前的旧 NoRisk 值；战斗index非法返回 -1。

## 参考实例

```lua
Battle.SetNoRisk(TM_BattleIndex, 1);
```

### 备注

返回值是**旧的 NoRisk 值**，不是“1 为成功”。
