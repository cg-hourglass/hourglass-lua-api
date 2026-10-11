<!-- Generated. DO NOT EDIT. -->
# GetFloorPets

## NLG.GetFloorPets(MapId, FloorId)

### 函数功能

获取指定地图楼层上放置在地面的所有宠物对象。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorId: [数值型](../appendix/数值型.md) 地图编号。

### 返回值

一个从下标1开始的 Lua table，元素为宠物对象index；没有符合条件的宠物时返回空 table。

## 参考实例

```lua
local pets = NLG.GetFloorPets(0, 1000);
```
