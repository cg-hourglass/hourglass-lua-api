<!-- Generated. DO NOT EDIT. -->
# GetMod

## Battle.GetMod(BattleIndex)

### 函数功能

获取战斗的运行模式（战斗流程状态机所处的阶段）。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

运行模式值；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.GetMod(TM_BattleIndex) == 3 then
    print("战斗已进入结束阶段");
end
```

### 备注

运行模式取值常量表中**没有**对应的 %常量%，只能按数值比较：
0 无、1 初始化、2 战斗中、3 结束、4 停止、5 BOSS、6-10 观战 1-5、11 全部结束。

本函数返回的是战斗流程状态机的阶段，与 Battle.GetType 的战斗类型是不同字段；要判断
普通战／PVP 战／BOSS 战请用 Battle.GetType 或 Battle.IsBossBattle。
