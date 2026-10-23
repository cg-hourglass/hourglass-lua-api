<!-- Generated. DO NOT EDIT. -->
# Capacity

## Chess.Capacity()

### 函数功能

查询还能开始多少场图鉴棋局回放。

### 参数说明

无参数。

### 返回值

三个整数 available, active, limit：现在还能开始的回放数（chess.max_battles 的余量与空闲战斗槽数取小）、正在进行的回放数、chess.max_battles。

## 参考实例

```lua
local available = Chess.Capacity();
```

### 备注

chess.max_battles 为 0 时关闭回放，available 恒为 0；房间仍可只结算不播放。
