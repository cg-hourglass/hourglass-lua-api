<!-- Generated. DO NOT EDIT. -->
# WarpDestination

## NLG.WarpDestination(CharIndex)

### 函数功能

读取传送点当前已初始化的目标地图和坐标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 传送点对象 index，含自动迷宫楼梯。

### 返回值

返回 {map, floor, x, y}；对象无效、不是传送点或没有初始化目标时返回 nil。

## 参考实例

```lua
local target = NLG.WarpDestination(index);
if target then
  print(NLG.GetMapName(target.map, target.floor));
end
```

### 备注

只读接口，读取传送点实际使用的目标，不执行传送、不解析参数字符串。
返回常规目标，不代表调用者当前满足传送条件；目标地图尚不可用时 GetMapName 返回空字符串。
