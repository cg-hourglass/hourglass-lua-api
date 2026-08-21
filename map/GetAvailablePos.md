<!-- Generated. DO NOT EDIT. -->
# GetAvailablePos

## Map.GetAvailablePos(FloorId)

### 函数功能

在一张随机（迷宫）地图上获取一个可通行的空地坐标。

### 参数说明

- FloorId: [数值型](../appendix/数值型.md) 随机地图的 Floor ID。

### 返回值

返回 x、y 两个坐标值；失败时 x、y 都为 0。

## 参考实例

```lua
local LUAMAPID = %地图类型_LUAMAP%;
function getPosition(index, floorID)
  local mapx, mapy = Map.GetAvailablePos(floorID);
  if (mapx == 0 and mapy == 0) then
    NLG.SystemMessage(index, "获取地图可用坐标失败，请重试");
  else
    NLG.SystemMessage(index, "获取地图"..LUAMAPID..","..floorID.."可用坐标"..mapx..","..mapy);
    NLG.SystemMessage(index, "使用GM命令[warp "..LUAMAPID.." "..floorID.." "..mapx.." "..mapy.."] 可以移动过去看看哦");
  end
  return;
end
```
