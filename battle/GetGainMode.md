<!-- Generated. DO NOT EDIT. -->
# GetGainMode

## Battle.GetGainMode(BattleIndex)

### 函数功能

获取战斗奖励模式，如奖励经验、奖励 DP。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

战斗奖励类型；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.GetGainMode(TM_BattleIndex) == %战奖_PVP% then
    print("DP battle");
end
```

### 备注

可用的奖励模式常量：%战奖_普通%（0）、%战奖_PVP%（1）。
由于 Battle.SetGainMode 当前版本不会真正切换奖励模式，本函数读到的值不会被 SetGainMode 改变。
