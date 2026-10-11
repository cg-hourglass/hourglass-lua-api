<!-- Generated. DO NOT EDIT. -->
# DumpLuaMap

## Map.DumpLuaMap(Path, FloorId, WriteAsFloor)

### 函数功能

把一张 Lua 地图导出为本地地图文件（可当作简易地图编辑器使用）。

### 参数说明

- Path: [字符串](../appendix/字符串.md) 本地输出路径，不包含文件名，文件夹需以 "\" 结尾。
- FloorId: [数值型](../appendix/数值型.md) 要导出的地图的 Floor ID。
- WriteAsFloor: [数值型](../appendix/数值型.md) 写入文件内部记录的地图编号；省略时与 FloorId 相同。 [可为空]

### 返回值

失败返回 0，成功返回 1。

## 参考实例

```lua
local LUAMAPID = %地图类型_LUAMAP%;
function dumpMapFile(index, path, floorID, writeAsFloor)
  local ret = Map.DumpLuaMap(path, floorID, writeAsFloor);
  if (ret == 0) then
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."输出至文件失败！");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."已经输出至文件:["..path..LUAMAPID.."_"..floorID.."]");
  end
  return;
end
```

### 备注

第一个参数如果不是字符串或数字，会直接返回 0，不会抛出 Lua 错误。
