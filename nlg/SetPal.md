<!-- Generated. DO NOT EDIT. -->
# SetPal

## NLG.SetPal(CharIndex, PalID, FrameCnt)

### 函数功能

改变玩家客户端当前显示的地图调色板。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- PalID: [数值型](../appendix/数值型.md) 调色板编号。
- FrameCnt: [数值型](../appendix/数值型.md) 调色渐变的帧数，省略时默认为 1；不是持续时间秒数。 [可为空]

### 返回值

目标有效返回 1，无效返回 0。

## 参考实例

```lua
NLG.SetPal(player, 3);
```

### 备注

第三个参数的真实含义是调色渐变的帧数，并不是“持续时间，单位秒”，脚本编写时请以此为准。
本函数只要目标对象指针有效就返回1，不检查目标是否真的有一条活动连接；封包会尝试发送，但发送失败也不影响返回值。
