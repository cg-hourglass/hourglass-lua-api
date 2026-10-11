<!-- Generated. DO NOT EDIT. -->
# GetNoRisk

## Battle.GetNoRisk(BattleIndex)

### 函数功能

获取战斗的 NoRisk（无风险）标志。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

0 或 1；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.GetNoRisk(TM_BattleIndex) == 1 then
    print("no risk battle");
end
```
