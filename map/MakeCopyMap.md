<!-- Generated. DO NOT EDIT. -->
# MakeCopyMap

## Map.MakeCopyMap(MapId, FloorId)

### 函数功能

复制一张已存在的地图（原样拷贝地板/物件/遭遇等信息）到 Lua 地图区块中的一个新 Floor。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 要复制的地图的 Map ID。
- FloorId: [数值型](../appendix/数值型.md) 要复制的地图的 Floor ID。

### 返回值

成功返回新地图所在的 FloorId（Map ID 固定为常量 `%地图类型_LUAMAP%`）；失败返回 -1。

## 参考实例

```lua
local LUAMAPID = %地图类型_LUAMAP%;
function makeCopyMap(index, c_mapid, c_floor)
  local newFloorID = Map.MakeCopyMap(c_mapid, c_floor);
  if (newFloorID == -1) then
    NLG.SystemMessage(index, "地图复制失败。");
  else
    NLG.SystemMessage(index, "地图"..c_mapid..","..c_floor.."已经成功复制到"..LUAMAPID..","..newFloorID);
    NLG.SystemMessage(index, "使用GM命令[warp "..LUAMAPID.." "..newFloorID.." x坐标 y坐标] 可以移动过去看看哦");
  end
  return;
end
```

### 备注

新 Floor 分配自固定 128 个槽位的 Lua 地图区块，采用线性扫描找第一个
空闲槽位；槽位耗尽或源地图查无该 Floor 时返回 -1，分配失败会释放已
申请的资源，不留半成品槽位。
