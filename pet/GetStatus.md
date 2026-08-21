<!-- Generated. DO NOT EDIT. -->
# GetStatus

## Pet.GetStatus(CharIndex, PetSlot)

### 函数功能

获取玩家指定宠物栏位上宠物的出战状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标玩家的对象index。
- PetSlot: [数值型](../appendix/数值型.md) 宠物栏位置，取值 0-4。

### 返回值

指定宠物的状态常量；PetSlot 越界、对象不是玩家、或该栏位没有可用宠物时返回 -1。

## 参考实例

```lua
if Pet.GetStatus(_player, 0) == %宠物状态_战斗% then
    print("0 号栏位的宠物正在出战");
end
```

### 备注

宠物状态常量：%宠物状态_无%（0）、%宠物状态_待命%（1）、%宠物状态_战斗%（2）、%宠物状态_休息%（3）。

返回的是原始状态值，可能带有散步宠物标志位（16）。要比较基础状态请先按位与上 0x0f。
