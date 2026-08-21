<!-- Generated. DO NOT EDIT. -->
# HaveItem

## Char.HaveItem(CharIndex, ItemID)

### 函数功能

检测对象身上是否有指定 ID 的道具，并返回该道具index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。

### 返回值

第一个匹配到的道具index；没有该道具或对象指针无效时返回 -1。

## 参考实例

```lua
local ItemIndex = Char.HaveItem(Player, 10001);
if ItemIndex ~= -1 then
    Item.GetData(ItemIndex, %道具_名字%);
end
```

### 备注

返回的是道具index（道具实例的编号），不是道具栏位置；要拿栏位号请用 Char.FindItemId。
扫描覆盖 0-27 全部栏位，装备栏也在内。
