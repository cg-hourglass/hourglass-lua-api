<!-- Generated. DO NOT EDIT. -->
# HavePet

## Char.HavePet(CharIndex, PetID)

### 函数功能

检测对象身上是否有指定 ID 的宠物，并返回其宠物栏位置。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- PetID: [数值型](../appendix/数值型.md) 宠物 ID，对应敌人模板中的编号。

### 返回值

第一个持有该 PetID 的宠物栏位置（0-4）；没有或对象不是玩家时返回 -1。

## 参考实例

```lua
local Slot = Char.HavePet(Player, 100);
if Slot ~= -1 then
    Char.DelSlotPet(Player, Slot);
end
```

### 备注

返回的是宠物栏位置，不是宠物的对象index；要拿对象index请把这个位置传给 Char.GetPet。
对象指针无效时会在服务端日志留下一条记录。
