<!-- Generated. DO NOT EDIT. -->
# Play

## Chess.Play(CharIndex, A, B, Seed, Viewer, Opts)

### 函数功能

模拟对战并把某一方视角的原生战斗回放播给一名在线玩家（合成观战战斗），返回回放 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 观看者的角色索引，必须是在线玩家。
- A: [表](../appendix/表.md) 甲方棋盘，格式同 Chess.Simulate。
- B: [表](../appendix/表.md) 乙方棋盘。
- Seed: [数值型](../appendix/数值型.md) 随机种子，同 Chess.Simulate。
- Viewer: [数值型](../appendix/数值型.md) 观看者所在方，0 为甲方、1 为乙方。
- Opts: [表](../appendix/表.md) 可选，同 Chess.EncodeMovie。

### 返回值

成功时为回放 ID（正整数，进程内唯一）；失败时为 nil 和原因："offline"（角色不在线或不是玩家）、"busy"（已在战斗、观战或另一场回放中）、"capacity"（并发回放数已达 chess.max_battles，或战斗槽池已满）。

## 参考实例

```lua
local id, why = Chess.Play(charIndex, boardA, boardB, seed, 0, opts);
if not id then
  -- play this seat without a movie
end
```

### 备注

回放占用一个共享战斗槽（battle.max_battles），并受 chess.max_battles 限制；用 Chess.Capacity 预先检查。
播放节奏由客户端回报（Chess.RoundDone）驱动；用 Chess.Status 轮询回放何时结束。棋盘或参数非法时抛出错误，同 Chess.EncodeMovie。
同一场对战两名玩家各自观看时，各调用一次（各自的 Viewer）；模拟是确定性的，两边看到同一场战斗。
也可以写成 Chess.Play(CharIndex, Movie)：直接播放 Chess.EncodeMovie 的结果（{bc, m} 数组）；数组为空或某项缺少 bc（以 C| 开头）/ m（以 M| 开头）时抛出错误。
回放结束时触发 NL.RegChessReplayEndEvent 注册的事件（charIndex, replayId, status）。
