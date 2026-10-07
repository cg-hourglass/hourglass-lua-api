<!-- Generated. DO NOT EDIT. -->
# SetGetableItemList

## Pet.SetGetableItemList(EnemyIndex, ItemID, ItemSlot)

### 函数功能

设置战斗中敌方怪物身上的可掉落道具对象。

### 参数说明

- EnemyIndex: [数值型](../appendix/数值型.md) 目标敌人的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID（item.txt 中的 ID）。传 -1 视为无效，位置照常返回但道具index为 -1。
- ItemSlot: [数值型](../appendix/数值型.md) 掉落槽位置，取值 0-9。省略或传 -1 时自动寻找第一个空槽。 [可为空]

### 返回值

返回两个值——道具所在的位置（1 起算）与新建道具的道具index。位置越界时返回 -1, -1；其余失败情况位置正常返回而道具index为 -1。

## 参考实例

```lua
-- 自动放入第一个空槽
local TM_Pos, TM_Item = Pet.SetGetableItemList(_enemy, 10007);

-- 指定放入第 3 个槽（下标 0 起算），会替换该槽原有道具
local TM_Pos2, TM_Item2 = Pet.SetGetableItemList(_enemy, 10008, 2);
```

### 备注

本函数设置的是**可掉落**道具列表；可偷窃道具请用 Pet.SetStealableItem。

入参 ItemSlot 是 0 起算的，返回的位置是 1 起算的，两者相差 1，不要直接把返回值回传。

**本版本已知行为**：ItemSlot 省略且 10 个槽全满时，不会失败，而是回退到第 0 槽并
覆盖那里原有的道具。

指定槽位上已有道具时会先释放旧道具再放入新道具；旧道具对象随之失效。
