<!-- Generated. DO NOT EDIT. -->
# GetPetSlotRange

## Bank.GetPetSlotRange(CharIndex)

### 函数功能

Return the player's effective bank pet range as inclusive absolute pool indices.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.

### 返回值

Two integers (0, effective pet rights minus 1), or nil for an invalid/nonplayer object.

## 参考实例

```lua
local first, last = Bank.GetPetSlotRange(player);
if first then
    for slot = first, last do
        local pet = Char.GetPoolPet(player, slot);
    end
end
```

### 备注

Default range is 0..9; maximum is 0..49. Pet rights are independent of item rights; the larger bank highest page does not grant slots of the other asset class.
