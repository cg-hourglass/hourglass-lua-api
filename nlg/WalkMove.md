<!-- Generated. DO NOT EDIT. -->
# WalkMove

## NLG.WalkMove(CharIndex, Dir)

### 函数功能

让对象朝指定方向走一格（真实位移，不只是转身）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- Dir: [数值型](../appendix/数值型.md) 移动方向，取值范围 0-7，对应游戏内的八个方向。

### 返回值

0 表示移动成功；1（内部指针无效）、2（坐标超出地图范围）、4（前置行走事件拒绝）、6（目标格不可通行）为各类失败原因；Dir 超出 0-7 范围时直接返回 -1。

## 参考实例

```lua
local dir = math.random(0, 7);
NLG.SetAction(_MeIndex, 1); -- 设置为走路动作
NLG.WalkMove(_MeIndex, dir); -- 让_MeIndex对应的NPC随机移动一格
```

### 备注

移动成功后仅在非战斗状态下广播一次“行走”观察事件（act=1）；本版本尚未提供“向新进入视野的角色补发一次行走中重绘封包”的能力——对已经在视野内的客户端没有影响，只在角色刚刚进入某个玩家视野的边界情况下可能少一次同步，是已知的能力缺口。
