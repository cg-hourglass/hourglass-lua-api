<!-- Generated. DO NOT EDIT. -->
# GetStealableItem

## Pet.GetStealableItem(EnemyIndex)

### 函数功能

获取战斗中敌方怪物身上的可偷窃道具对象。

### 参数说明

- EnemyIndex: [数值型](../appendix/数值型.md) 目标敌人的对象index。

### 返回值

可偷窃道具的道具index，可交给 Item 库操作；没有可偷窃道具或对象不是敌人时返回 -1。

## 参考实例

```lua
local TM_Item = Pet.GetStealableItem(_enemy);
if TM_Item ~= -1 then
    print(Item.GetData(TM_Item, %道具_名字%));
end
```
