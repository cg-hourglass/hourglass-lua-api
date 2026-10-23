<!-- Generated. DO NOT EDIT. -->
# GetPoolItem

## Char.GetPoolItem(CharIndex, Slot)

### 函数功能

获取玩家银行中指定位置的道具index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) Absolute bank item slot within Bank.GetItemSlotRange(CharIndex). Default range 0..39, maximum 0..199.

### 返回值

该位置的道具index；位置为空、位置越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local first, last = Bank.GetItemSlotRange(Player);
if first then
    for slot = first, last do
        local itemIndex = Char.GetPoolItem(Player, slot);
    end
end
```

### 备注

读的是银行（Pool）道具栏，不是出租屋。
The effective upper bound follows the player's item rights and char.bank_pages_max, independently of pet rights. Use Bank.GetItemSlotRange instead of a fixed loop bound.
对象指针无效时会在服务端日志留下一条错误记录。
