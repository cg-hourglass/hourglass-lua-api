<!-- Generated. DO NOT EDIT. -->
# GetItemSlotRange

## Bank.GetItemSlotRange(CharIndex)

### 函数功能

Return the player's effective bank item range as inclusive absolute pool indices.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.

### 返回值

Two integers (0, effective item rights minus 1), or nil for an invalid/nonplayer object.

## 参考实例

```lua
local first, last = Bank.GetItemSlotRange(player);
if first then
    for slot = first, last do
        local item = Char.GetPoolItem(player, slot);
    end
end
```

### 备注

Default range is 0..39; maximum is 0..199. Item rights are rounded/clamped independently of pet rights and char.bank_pages_max. No open bank window or BK1 negotiation is required. Indices are not page-local packet rows.
