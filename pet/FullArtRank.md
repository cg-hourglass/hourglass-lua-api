<!-- Generated. DO NOT EDIT. -->
# FullArtRank

## Pet.FullArtRank(PetIndex, ArtType)

### 函数功能

获取指定宠物某项属性的满档成长值。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- ArtType: [数值型](../appendix/数值型.md) 要查看的属性，取值见 Pet.ArtRank 备注中的宠物成长常量。

### 返回值

该属性的满档成长值（怪物模板基础值 + 2）；对象无效、既不是宠物也不是敌人、或属性常量未知时返回 0。

## 参考实例

```lua
local TM_Full = Pet.FullArtRank(_pet, %宠档_魔成%);
print("魔成满档值 = " .. TM_Full);
```

### 备注

满档值取自怪物模板表中该宠物模板的基础成长值再加 2，是按模板查的常量，
与宠物当前状态无关。

边界情况：模板表里找不到该宠物的模板编号时，表查询返回 -1，本函数会因此返回 1（-1 + 2）。
拿到 1 这个可疑结果时应当先确认宠物模板编号是否有效。
