<!-- Generated. DO NOT EDIT. -->
# GetMapSize

## Map.GetMapSize(MapId, FloorId)

### 函数功能

获取地图的尺寸。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 地图的 Map ID。
- FloorId: [数值型](../appendix/数值型.md) 地图的 Floor ID。

### 返回值

返回两个值，分别是 x 轴最大值与 y 轴最大值；Map ID/Floor ID 不匹配时返回 (-1, -1)。

## 参考实例

```lua
local xsize, ysize = Map.GetMapSize(mapId, floorId);
```
