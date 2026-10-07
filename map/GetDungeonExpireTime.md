<!-- Generated. DO NOT EDIT. -->
# GetDungeonExpireTime

## Map.GetDungeonExpireTime(FloorId)

### 函数功能

获取一张（经典随机地城系统的）地图距离重置还剩的秒数。

### 参数说明

- FloorId: [数值型](../appendix/数值型.md) 地图的 Floor ID。

### 返回值

返回距离重置时间还剩的秒数；该 Floor 不是被追踪的活跃地城时返回 -1。

## 参考实例

```lua
local remainSec = Map.GetDungeonExpireTime(floorId);
```

### 备注

这里查询的是「经典自动地城」子系统，与 Map.MakeMazeMap 生成的 Lua
迷宫地图是两套独立的机制；对一张纯 Lua 生成的地图调用本函数通常会
得到 -1（因为它没有被登记为经典地城）。
