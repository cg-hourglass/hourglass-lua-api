<!-- Generated. DO NOT EDIT. -->
# GetImage

## Map.GetImage(MapId, FloorId, X, Y)

### 函数功能

获取地图指定坐标的地板（底层）图档编号与物件（顶层）图档编号。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 地图的 Map ID。
- FloorId: [数值型](../appendix/数值型.md) 地图的 Floor ID。
- X: [数值型](../appendix/数值型.md) 坐标 X。
- Y: [数值型](../appendix/数值型.md) 坐标 Y。

### 返回值

正常返回两个值（地板图档、物件图档）；Map ID 越界或 Floor 查无时只返回单个 0（不是一对 0,0）。

## 参考实例

```lua
function getTileandObj(index)
  local nowMap = Char.GetData(index, %对象_MAP%);
  local nowFloor = Char.GetData(index, %对象_地图%);
  local nowXpos = Char.GetData(index, %对象_X%);
  local nowYpos = Char.GetData(index, %对象_Y%);
  local tile, obj = Map.GetImage(nowMap, nowFloor, nowXpos, nowYpos);
  NLG.SystemMessage(index, "获取地图"..nowMap..","..nowFloor..","..nowXpos..","..nowYpos.."的地图元素[地板:"..tile.."],[物件:"..obj.."]");
  return;
end
```

### 备注

失败时只返回一个 0（单值），与 Map.SetImage 失败时同样返回单值 0 形成
巧合的一致，但与「成功时永远两个值」的直觉不一致；脚本里用
`local tile, obj = Map.GetImage(...)` 接收失败结果时 `obj` 会是 nil，
务必在下游代码里判断。
