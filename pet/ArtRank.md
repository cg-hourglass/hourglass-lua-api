<!-- Generated. DO NOT EDIT. -->
# ArtRank

## Pet.ArtRank(PetIndex, ArtType)

### 函数功能

获取指定宠物某项属性的当前成长值（档数）。

### 函数别名

- `Pet.GetArtRank(PetIndex, ArtType)`

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- ArtType: [数值型](../appendix/数值型.md) 要查看的属性，取值见备注中的宠物成长常量。

### 返回值

该属性的当前成长值（0-63）；对象无效、既不是宠物也不是敌人、或属性常量未知时返回 0。

## 参考实例

```lua
local arr_rank1 = Pet.ArtRank(_pet, %宠档_体成%);
local arr_rank11 = Pet.FullArtRank(_pet, %宠档_体成%);
-- arr_rank1 为宠物当前的体力成长值，arr_rank11 为该宠物体力成长的满档值
-- arr_rank11 - arr_rank1 即为体力距离满档还差的档数
print(arr_rank11 - arr_rank1);
```

### 备注

宠物成长常量：%宠档_体成%（1）、%宠档_力成%（2）、%宠档_强成%（3）、%宠档_敏成%（4）、%宠档_魔成%（5）。

五项成长值以 5 个 6 位字段的形式打包在同一个内部整数里，本函数按位段解包，
因此单项取值范围是 0-63。

注意相减顺序：应当用满档值减当前值，写反会得到负数。
