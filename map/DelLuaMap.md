<!-- Generated. DO NOT EDIT. -->
# DelLuaMap

## Map.DelLuaMap(FloorId)

### 函数功能

删除一张 Lua 生成的地图，释放其 Floor 编号，并将该地图上的所有实体清场。

### 参数说明

- FloorId: [数值型](../appendix/数值型.md) 要删除的地图的 Floor ID。

### 返回值

地图确实存在并删除成功返回 1；地图不存在（未被 Lua 占用）返回 0。

## 参考实例

```lua
local LUAMAPID = %地图类型_LUAMAP%;
function deleteLuaMap(index, floorID)
  local ret = Map.DelLuaMap(floorID);
  if (ret == 0) then
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."删除失败！");
  else
    NLG.SystemMessage(index, "地图"..LUAMAPID..","..floorID.."已经成功删除！");
  end
  return;
end
```

### 备注

清场规则：地图上的掉落道具随对象一并删除；玩家会收到系统提示后被强制
传送回登录点；宠物/NPC 类实体交由清场钩子处理（含停止游荡、邮寄迷路
宠物、直接删除等分支）。地面散落的金币对象是唯一被刻意放过、不清场的
类型，此为沿袭旧版的行为。
