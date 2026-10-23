<!-- Generated. DO NOT EDIT. -->
# GetPoolPet

## Char.GetPoolPet(CharIndex, Slot)

### 函数功能

获取玩家银行中指定位置的宠物对象index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) Absolute bank pet slot within Bank.GetPetSlotRange(CharIndex). Default range 0..9, maximum 0..49.

### 返回值

该位置宠物的对象index；位置为空、位置越界、宠物已失效、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local first, last = Bank.GetPetSlotRange(Player);
if first then
    for slot = first, last do
        local pet = Char.GetPoolPet(Player, slot);
    end
end
```

### 备注

The effective upper bound follows the player's pet rights and char.bank_pages_max, independently of item rights. Use Bank.GetPetSlotRange instead of a fixed loop bound.
对象指针无效时会在服务端日志留下一条错误记录。
