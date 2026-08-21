<!-- Generated. DO NOT EDIT. -->
# GetMapPlayerNum

## NLG.GetMapPlayerNum(Map, Floor)

### 函数功能

获取指定地图楼层上在线玩家的数量。

### 参数说明

- Map: [数值型](../appendix/数值型.md) 地图类型，0为固定地图，1为随机地图。
- Floor: [数值型](../appendix/数值型.md) 地图编号。

### 返回值

该地图楼层上的在线玩家数（大于等于0的整数）。

## 参考实例

```lua
local num = NLG.GetMapPlayerNum(0, 1000);
```

### 备注

本函数没有失败返回 -1 的分支，地图楼层不存在或无人时直接返回 0。
