<!-- Generated. DO NOT EDIT. -->
# SetMapName

## NLG.SetMapName(MapID, FloorID, Name)

### 函数功能

设置指定地图楼层的显示名称，并向当前在该楼层的所有玩家实时广播。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。
- Name: [字符串](../appendix/字符串.md) 要设置的地图名字。

### 返回值

成功返回 1，地图楼层不存在时返回 0。

## 参考实例

```lua
NLG.SetMapName(0, 1000, "法兰城·活动特别版");
```
