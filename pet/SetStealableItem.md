<!-- Generated. DO NOT EDIT. -->
# SetStealableItem

## Pet.SetStealableItem(EnemyIndex, ItemID)

### 函数功能

设置战斗中敌方怪物身上的可偷窃道具对象。

### 参数说明

- EnemyIndex: [数值型](../appendix/数值型.md) 目标敌人的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID（item.txt 中的 ID）。传 -1 视为无效，函数直接失败。

### 返回值

新建道具的道具index，可交给 Item 库操作；对象不是敌人、ItemID 为 -1 或道具创建失败时返回 -1。

## 参考实例

```lua
local TM_Item = Pet.SetStealableItem(_enemy, 10007);
```

### 备注

若该敌人偷窃槽上已有道具，会先释放旧道具再放入新道具；旧道具对象随之失效。
