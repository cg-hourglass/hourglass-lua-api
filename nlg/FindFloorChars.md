<!-- Generated. DO NOT EDIT. -->
# FindFloorChars

## NLG.FindFloorChars(MapID, FloorID, Kind)

### 函数功能

列出指定地图楼层上某一类非玩家对象（NPC、传送点或指定类型）的对象index。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图（迷宫）。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。
- Kind: [字符串](../appendix/字符串.md) 要列出的对象种类："npc"（除传送点、玩家、宠物、敌人以外的所有类型，与 Foreach.Npc 相同）、"warp"（传送点，CHAR_TYPEWARP，含迷宫楼梯），或一个由对象类型编号（%对象_序% 的取值）组成的数组 table。

### 返回值

一个从下标1开始的 Lua table，元素为对象index，按角色数组顺序排列；楼层上没有符合条件的对象时返回空 table（`{}`），返回值始终是 table。

## 参考实例

```lua
local warps = NLG.FindFloorChars(1, floorId, "warp");
for i = 1, #warps do
  print(Char.GetData(warps[i], %对象_X%), Char.GetData(warps[i], %对象_Y%));
end
local shops = NLG.FindFloorChars(0, 1000, {9, 25}); -- 按类型编号筛选
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有；脚本需要同时兼容两者时，先判断 `NLG.FindFloorChars` 是否为 nil，为 nil 时用 Foreach.Npc / Foreach.Warp 加 %对象_MAP% / %对象_地图% 过滤得到同样的结果（只是要遍历全服）。
扫描范围与 FindNpcByPos 相同（角色数组里玩家之后的槽位），所以玩家永远不会出现在结果里，即使类型数组里写了玩家类型。
Kind 不是 "npc"、"warp" 或数组，或数组里有非数值元素，或参数个数不是 3 个时，直接抛出可被 pcall 捕获的参数错误。
GM 调试命令 npcsearch / warpsearch 用的是同一套筛选逻辑。
