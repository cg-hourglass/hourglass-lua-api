<!-- Generated. DO NOT EDIT. -->
# GetPlayIndex

## Battle.GetPlayIndex(BattleIndex, EntryNo)

### 函数功能

获取战斗队列中指定位置上对象实例的对象index。

### 函数别名

- `Battle.GetPlayer(BattleIndex, EntryNo)`

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。
- EntryNo: [数值型](../appendix/数值型.md) 战斗队列中的位置，范围 0-19，其中 0-9 为下方队列（玩家方），10-19 为上方队列（敌方）。

### 返回值

该位置上可用对象的对象index；位置为空或战斗index非法返回 -1；EntryNo 不在 0-19 范围内返回 -3。

## 参考实例

```lua
local TM_Char = Battle.GetPlayIndex(TM_BattleIndex, 10);
if TM_Char ~= -1 then
    print("上方队列第一个位置的对象index = " .. TM_Char);
end
```

### 备注

位置到队列的换算规则：0-9 直接对应下方队列的第 0-9 个位置，10-19 减 10 后对应上方队列的第 0-9 个位置。
只有当前可用的对象才会被返回，槽位存在但对象已失效同样返回 -1。
