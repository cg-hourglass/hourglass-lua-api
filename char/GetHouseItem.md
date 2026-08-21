<!-- Generated. DO NOT EDIT. -->
# GetHouseItem

## Char.GetHouseItem(CharIndex, Slot)

### 函数功能

获取玩家出租屋中指定位置的道具index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 出租屋道具栏位置，本版本范围 0-19。

### 返回值

该位置的道具index；位置为空、位置越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local ItemIndex = Char.GetHouseItem(Player, 0);
```

### 备注

位置上限本版本是 20，即 0-19。
对象指针无效时会在服务端日志留下一条错误记录。
