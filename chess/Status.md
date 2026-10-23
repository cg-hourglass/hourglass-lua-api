<!-- Generated. DO NOT EDIT. -->
# Status

## Chess.Status(ReplayId)

### 函数功能

查询一场图鉴棋局回放的状态，供房间轮询回合屏障。

### 参数说明

- ReplayId: [数值型](../appendix/数值型.md) Chess.Play 返回的回放 ID。

### 返回值

"playing"（进行中）、"completed"（播完）、"timeout"（客户端超过 chess.round_timeout_seconds 没有回报，回放已结束）、"left"（观看者下线）、"stopped"（被 Chess.Stop 结束）；未知 ID 或结束已超过 10 分钟时为 nil。

## 参考实例

```lua
if Chess.Status(seat.replay) ~= "playing" then
  seat.replay = nil
end
```

### 备注

结束时还会触发 NL.RegChessReplayEndEvent 事件；本函数用于补查（例如重载脚本后）。
