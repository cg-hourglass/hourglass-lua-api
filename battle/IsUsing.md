<!-- Generated. DO NOT EDIT. -->
# IsUsing

## Battle.IsUsing(BattleIndex)

### 函数功能

判断指定战斗槽是否正在使用中。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

1 表示战斗正在进行，0 表示该槽空闲；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.IsUsing(TM_BattleIndex) == 1 then
    print("战斗仍在进行");
end
```

### 备注

战斗index的合法性检查只做数组边界判断，不看战斗是否在用；因此一个边界合法但空闲的槽位
会正常返回 0，而不是错误码 -1。
