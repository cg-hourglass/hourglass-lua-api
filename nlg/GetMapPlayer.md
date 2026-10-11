<!-- Generated. DO NOT EDIT. -->
# GetMapPlayer

## NLG.GetMapPlayer(MapID, FloorID)

### 函数功能

获取指定地图楼层上所有在线玩家的对象index。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。

### 返回值

一个从下标1开始的 Lua table，元素为对象index；该地图楼层没有玩家时返回空 table（`{}`），返回值始终是 table，不会是其他类型。

## 参考实例

```lua
local playertbl = NLG.GetMapPlayer(0, 1000);
for i = 1, #playertbl do
  NLG.SystemMessage(playertbl[i], "法兰城公告");
end
```

### 备注

本函数的返回值恒为 table（哪怕该地图楼层没有玩家也是空 table），不需要用 `type()` 判断返回值类型来区分“有玩家”和“无地图/无玩家”，直接看 `#playertbl` 是否为 0 即可。
