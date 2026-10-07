<!-- Generated. DO NOT EDIT. -->
# SetMod

## Battle.SetMod(BattleIndex, Mod)

### 函数功能

设置战斗的运行模式（战斗流程状态机所处的阶段）。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Mod: [数值型](../appendix/数值型.md) 新的运行模式值，取值见备注。

### 返回值

返回设置之前的旧运行模式；战斗index非法返回 -1。

## 参考实例

```lua
local TM_OldMod = Battle.GetMod(TM_BattleIndex);
Battle.SetMod(TM_BattleIndex, 3); -- 把战斗推进到结束阶段
```

### 备注

运行模式取值常量表中**没有**对应的 %常量%，只能填数值：
0 无、1 初始化、2 战斗中、3 结束、4 停止、5 BOSS、6-10 观战 1-5、11 全部结束。

本函数操作的是战斗流程状态机，与 Battle.SetType 的战斗类型是不同字段，注意不要混淆。

返回值是**旧的模式值**，不是“1 为成功”。

本函数直接改写字段，**不做状态转移合法性校验**（引擎内部的模式切换是有转移表约束的）。
写入不符合当前阶段的值可能让战斗流程停摆，非必要不要使用。
