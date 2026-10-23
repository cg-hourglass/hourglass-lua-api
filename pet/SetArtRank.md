<!-- Generated. DO NOT EDIT. -->
# SetArtRank

## Pet.SetArtRank(PetIndex, ArtType, Value)

### 函数功能

设置指定宠物某项属性的成长值（档数）。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- ArtType: [数值型](../appendix/数值型.md) 要设置的属性，取值见 Pet.ArtRank 备注中的宠物成长常量。
- Value: [数值型](../appendix/数值型.md) 要设置的成长值，负数会被钳位为 0。

### 返回值

对象是宠物或敌人时返回 1，否则返回 0。

## 参考实例

```lua
Pet.SetArtRank(_pet, %宠档_体成%, 10); -- 把体力成长设为 10 档
Pet.ReBirth(_player, _pet);            -- 再回炉一次，让基础属性按新档数重算
```

### 备注

**1 为成功，0 为失败**，不是“0 成功”。

本函数只改写成长档数，不会重新分配宠物已有的 bp；要让基础属性跟着新档数重算，
需要配合 Pet.ReBirth 使用。

**本版本已知行为**：只钳位负值，没有上限钳位。写入大于 63 的值会溢出到相邻的
属性成长值上，污染其他属性；写入 128 以上还会影响到打包数值的符号位，脚本请务必
将 Value 控制在 0-63 范围内。
ArtType 传入未知常量时不修改任何字段，但仍然会返回 1。
