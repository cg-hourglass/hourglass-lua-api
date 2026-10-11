<!-- Generated. DO NOT EDIT. -->
# Walkable

## NLG.Walkable(MapID, FloorID, X, Y)

### 函数功能

检测地图上指定坐标是否可通行。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。
- X: [数值型](../appendix/数值型.md) X坐标。
- Y: [数值型](../appendix/数值型.md) Y坐标。

### 返回值

可通行返回 1，不可通行（或坐标/地图无效）返回 0。

## 参考实例

```lua
if NLG.Walkable(0, 1000, 10, 10) == 1 then
  NLG.WalkMove(_MeIndex, dir);
end
```
