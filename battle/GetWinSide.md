<!-- Generated. DO NOT EDIT. -->
# GetWinSide

## Battle.GetWinSide(BattleIndex)

### 函数功能

获取战斗胜利方所在的队列。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

0 表示下方队列（战斗位置 0-9）获胜，1 表示上方队列（战斗位置 10-19）获胜；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.GetWinSide(TM_BattleIndex) == 0 then
    print("下方队列获胜");
end
```

### 备注

战斗尚未分出胜负时该字段保持引擎的初始值，判定胜负前请配合 Battle.IsUsing 使用。
