<!-- Generated. DO NOT EDIT. -->
# RegChessReplayEndEvent

## NL.RegChessReplayEndEvent(Dofile, FuncName)

### 函数功能

注册图鉴棋局回放结束时触发的 Lua 函数，房间用它释放回合屏障。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## ChessReplayEndCallBack(CharIndex, ReplayId, Status)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 观看者的角色索引（下线结束时为下线前的索引）。
- ReplayId: [数值型](../appendix/数值型.md) Chess.Play 返回的回放 ID。
- Status: [字符串](../appendix/字符串.md) "completed"（播完）、"timeout"（客户端超时未回报）、"left"（观看者下线）、"stopped"（Chess.Stop）。

### 返回值

无

## 参考实例

```lua
NL.RegChessReplayEndEvent(nil, "MyChessReplayEnd");

function MyChessReplayEnd(charIndex, replayId, status)
  -- status: "completed" / "timeout" / "left" / "stopped"
end
```

### 备注

本事件是本服务端新增的，C 版 gmsv 没有。每场回放结束恰好触发一次，在结束它的那次战斗循环末尾（下线导致的结束在下一次战斗循环）触发，从不在 Chess.Stop 调用内部或下线流程中触发。
观看者下线或断线时，服务端立即结束其回放并释放战斗槽，本事件以 "left" 送达。
