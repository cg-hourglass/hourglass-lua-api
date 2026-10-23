<!-- Generated. DO NOT EDIT. -->
# FindItemId

## Char.FindItemId(CharIndex, ItemID)

### 函数功能

查找对象身上第一个指定 ID 道具所在的道具栏位置。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。

### 返回值

第一个匹配道具所在的道具栏位置（0-27）；没有该道具或对象指针无效时返回 -1。

## 参考实例

```lua
local Slot = Char.FindItemId(Player, 10001);
if Slot ~= -1 then
    Item.UpItem(Player, Slot);
end
```

### 备注

与 Char.HaveItem 是同一次扫描，区别只在返回什么：这里返回栏位号，HaveItem 返回道具index。
扫描覆盖 0-27 全部栏位，装备栏 0-7 也在内。
