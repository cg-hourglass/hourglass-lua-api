<!-- Generated. DO NOT EDIT. -->
# CheckInFront

## NLG.CheckInFront(CharIndex, TargetCharIndex, Distance)

### 函数功能

判断目标对象是否位于自身朝向方向、指定距离以内的直线格子上。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 自身对象index，以该对象的朝向为基准。
- TargetCharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- Distance: [数值型](../appendix/数值型.md) 检测距离（格数）。

### 返回值

是（Lua 布尔值 true）或否（false）；两个对象无效、不在同一地图楼层、坐标重合或 Distance<=0 时都是 false。

## 参考实例

```lua
if NLG.CheckInFront(_MeIndex, playerIndex, 2) then
  NLG.SystemMessage(playerIndex, "你在我面前！");
end
```

### 备注

本函数返回的是 Lua 布尔值，不是 1/0 数值——判断请用 `== true`/`if ... then`，不要与数值 1 比较。
只要求 TargetCharIndex 落在 CharIndex 朝向方向的连线格子上，不要求 TargetCharIndex 转身面对 CharIndex；需要“互相面对面”的语义请用 CheckTalkRange 或 CanTalk。
