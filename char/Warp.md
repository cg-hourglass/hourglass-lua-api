<!-- Generated. DO NOT EDIT. -->
# Warp

## Char.Warp(CharIndex, MapID, FloorID, X, Y)

### 函数功能

将对象连同其队伍传送到指定地图坐标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- MapID: [数值型](../appendix/数值型.md) 目标地图 ID。
- FloorID: [数值型](../appendix/数值型.md) 目标楼层 ID。
- X: [数值型](../appendix/数值型.md) 目标 X 坐标。
- Y: [数值型](../appendix/数值型.md) 目标 Y 坐标。

### 返回值

传送成功返回 1；坐标非法或传送失败返回 0；对象指针无效时返回 nil。

## 参考实例

```lua
Char.Warp(Player, 100, 1000, 40, 40);
```

### 备注

这是整队传送，队伍成员会跟着一起移动，不只是调用者本人。
坐标会先做合法性校验，不合法时静默返回 0，不会有任何提示。
