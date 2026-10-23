<!-- Generated. DO NOT EDIT. -->
# RoundDone

## Chess.RoundDone(CharIndex, Seq)

### 函数功能

报告某角色的客户端已播完其图鉴棋局回放的前 Seq 个播放回合，用于按回报控制发包节奏。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 观看者的角色索引。
- Seq: [数值型](../appendix/数值型.md) 已播完的播放回合数（从 1 起，累计值）。

### 返回值

被接受时为 true；角色不在棋局回放中、Seq 不大于已报告数或大于已发送数时为 false。

## 参考实例

```lua
rpc.handle("chess", "round_done", function(charIndex, body)
  return { ok = Chess.RoundDone(charIndex, tonumber(body.seq) or 0) }
end)
```

### 备注

由 cgx 服务 chess/round_done 转发。服务端只有在该回合的最快播放下界（按 chess.playback_percent 折算）也已过去后才算它播完，提前回报不会加快节奏；超过 chess.round_timeout_seconds 没有回报时，回放结束并释放战斗槽。
