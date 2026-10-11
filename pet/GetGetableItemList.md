<!-- Generated. DO NOT EDIT. -->
# GetGetableItemList

## Pet.GetGetableItemList(EnemyIndex)

### 函数功能

获取战斗中敌方怪物身上的可掉落道具对象列表。

### 参数说明

- EnemyIndex: [数值型](../appendix/数值型.md) 目标敌人的对象index。

### 返回值

返回一个下标 1-10 的 table，每个下标对应一个掉落槽，值为道具index，槽位为空时为 -1；对象不是敌人时返回 -1。

## 参考实例

```lua
local TM_List = Pet.GetGetableItemList(_enemy);
if type(TM_List) == "table" then
    for i = 1, 10 do
        if TM_List[i] ~= nil and TM_List[i] ~= -1 then
            print(i .. " -> " .. TM_List[i]);
        end
    end
end
```

### 备注

**已经被玩家取走的槽位会被整个跳过**，table 中连这个下标都不存在（读出来是 nil），
而不是 -1。遍历时要同时判断 nil 与 -1，示例中的写法即为此。
