<!-- Generated. DO NOT EDIT. -->
# Stop

## Chess.Stop(CharIndex)

### 函数功能

立即结束某角色正在进行的图鉴棋局回放（客户端退出战斗画面）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 观看者的角色索引。

### 返回值

结束了一场回放时为 true；该角色不在回放中时为 false。

## 参考实例

```lua
Chess.Stop(charIndex);
```

### 备注

用于认输、房间解散等；该回放的 Chess.Status 变为 "stopped"。
