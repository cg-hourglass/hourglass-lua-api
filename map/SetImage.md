<!-- Generated. DO NOT EDIT. -->
# SetImage

## Map.SetImage(MapId, FloorId, X, Y, Image)

### 函数功能

设置地图指定坐标的地板或物件图档编号（系统自动判定该图档属于地板层还是物件层）。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 地图的 Map ID。
- FloorId: [数值型](../appendix/数值型.md) 地图的 Floor ID。
- X: [数值型](../appendix/数值型.md) 坐标 X。
- Y: [数值型](../appendix/数值型.md) 坐标 Y。
- Image: [数值型](../appendix/数值型.md) 要设置的图档编号；系统按图档号区间自动判定归入地板层还是物件层。

### 返回值

失败返回 0；成功返回 1。

## 参考实例

```lua
function setTileandObj(index, image)
  local nowMap = Char.GetData(index, %对象_MAP%);
  local nowFloor = Char.GetData(index, %对象_地图%);
  local nowXpos = Char.GetData(index, %对象_X%);
  local nowYpos = Char.GetData(index, %对象_Y%);
  local ori_tile, ori_obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  Map.SetImage(nowMap, nowFloor, nowXpos, nowYpos, image);
  local now_tile, now_obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  NLG.SystemMessage(index, "地图"..nowMap..","..nowFloor..","..nowXpos..","..nowYpos.."的地图元素变更[地板:"..ori_tile.."->"..now_tile.."],[物件:"..ori_obj.."->"..now_obj.."]");
  return;
end
```

### 备注

写入不会对 X/Y 坐标做边界检查，调用方需自行保证坐标合法。写入成功后
会广播给该坐标附近的在线玩家，对已在该楼层的玩家立即可见。
