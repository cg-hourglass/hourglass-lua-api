<!-- Generated. DO NOT EDIT. -->
# GetPet

## Char.GetPet(CharIndex, Slot)

### 函数功能

获取对象指定宠物栏位上的宠物对象index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 宠物栏位置，范围 0-4。

### 返回值

该栏位宠物的对象index；栏位为空、栏位越界、宠物已失效或对象不是玩家时返回 -1。

## 参考实例

```lua
local Pet = Char.GetPet(Player, 0);
if Pet ~= -1 then
    Char.GetData(Pet, %对象_名字%);
end
```

### 备注

本函数会对宠物做可用性检查，失效的宠物返回 -1；而 Char.PetNum 只数指针，不做这项检查，
因此两者的结果在极端情况下可能对不上。
