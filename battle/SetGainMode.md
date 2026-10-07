<!-- Generated. DO NOT EDIT. -->
# SetGainMode

## Battle.SetGainMode(BattleIndex, Mod)

### 函数功能

设置战斗奖励模式，如奖励经验、奖励 DP。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Mod: [数值型](../appendix/数值型.md) 战斗奖励类型，参照奖励模式常量。

### 返回值

返回调用前的 GainMode 值；战斗index非法返回 -1。

## 参考实例

```lua
Battle.SetGainMode(TM_BattleIndex, %战奖_PVP%);
```

### 备注

可用的奖励模式常量：%战奖_普通%（0）、%战奖_PVP%（1）。

**本版本已知行为**：SetGainMode 当前版本不会真正切换奖励模式——本函数读取并返回的
是另一个内部字段的旧值，实际被写入的是战斗类型（等同于一次 Battle.SetType）。因此
连续调用 SetGainMode 会一直返回同一个旧值。该行为沿袭旧版，脚本不要依赖它来切换
奖励模式；需要读取奖励模式请用 Battle.GetGainMode。
