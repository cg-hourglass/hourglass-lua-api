<!-- Generated. DO NOT EDIT. -->
# FindNpcByPos

## NLG.FindNpcByPos(MapID, FloorID, X, Y)

### 函数功能

按坐标查找该格子上的第一个 NPC 类对象。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。
- X: [数值型](../appendix/数值型.md) X坐标。
- Y: [数值型](../appendix/数值型.md) Y坐标。

### 返回值

目标NPC的对象index；没有找到返回 -1。

## 参考实例

```lua
local npcIdx = NLG.FindNpcByPos(0, 1000, 20, 20);
```

### 备注

扫描范围是角色数组里“玩家之后、宠物与敌人之前之外”的其余槽位，并排除传送点、玩家、宠物、敌人这四类，其余（各类系统内建 NPC、剧情 NPC、Lua NPC 等）都参与匹配，按槽位顺序取第一个命中的。
