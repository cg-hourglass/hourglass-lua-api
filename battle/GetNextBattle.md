<!-- Generated. DO NOT EDIT. -->
# GetNextBattle

## Battle.GetNextBattle(BattleIndex, Flg)

### 函数功能

获取连战设置。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- Flg: [数值型](../appendix/数值型.md) 占位参数，必须传入但不会被读取（见备注）。

### 返回值

-1 表示没有连战配置；否则返回连战标志值。

## 参考实例

```lua
if Battle.GetNextBattle(TM_BattleIndex, 0) ~= -1 then
    print("已配置连战");
end
```

### 备注

**本版本已知行为**：本函数要求传入两个参数，却只读取第一个。少传参数会被参数检查拒绝，
所以第二个参数必须随便传一个值占位。

返回值有三种情况：连战已取消返回 -1；引擎连战设置为“未指定”且脚本侧曾单独设置过连战
标志时返回该标志；其余情况返回引擎内建的连战设置值。
