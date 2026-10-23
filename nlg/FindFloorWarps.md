<!-- Generated. DO NOT EDIT. -->
# FindFloorWarps

## NLG.FindFloorWarps(MapId, Floor)

### 函数功能

List live object warps loaded from warp.txt on a map and floor.

### 参数说明

- MapId: [数值型](../appendix/数值型.md) Source map type.
- Floor: [数值型](../appendix/数值型.md) Source floor ID.

### 返回值

A 1-based array of {x, y, target_map, target_floor}; empty if none exist.

## 参考实例

```lua
for _, warp in ipairs(NLG.FindFloorWarps(0, 1000)) do
  print(warp.x, warp.y, NLG.GetMapName(warp.target_map, warp.target_floor));
end
```

### 备注

Read-only. Object warps are separate from character warps returned by FindFloorChars.
Use WarpDestination for character warps, including generated dungeon stairs.
A destination name does not imply that the player satisfies its entry conditions.
