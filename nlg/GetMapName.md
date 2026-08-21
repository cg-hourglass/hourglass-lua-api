<!-- Generated. DO NOT EDIT. -->
# GetMapName

## NLG.GetMapName(MapID, FloorID)

### 函数功能

获取指定地图楼层当前设置的显示名称。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。

### 返回值

地图名称字符串；地图楼层不存在或尚未设置名称时返回空字符串 ""。

## 参考实例

```lua
local name = NLG.GetMapName(0, 1000);
```

### 备注

失败时返回的是空字符串 ""，不是数值 0；脚本判断失败应该用 `name == ""`，不要用 `name == 0`（类型不同，恒不相等）。
