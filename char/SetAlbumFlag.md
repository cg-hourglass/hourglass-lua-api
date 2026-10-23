<!-- Generated. DO NOT EDIT. -->
# SetAlbumFlag

## Char.SetAlbumFlag(CharIndex, AlbumId, Lit, Reveal)

### 函数功能

点亮或清除玩家的一个图鉴条目，并刷新客户端图鉴。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index。
- AlbumId: [数值型](../appendix/数值型.md) 图鉴编号（1 ~ 最大图鉴编号-1），与 enemybase 的 ALBUMNO 一致。
- Lit: [布尔型](../appendix/布尔型.md) true（或非 0 数字）点亮，false（或 0）清除。
- Reveal: [布尔型](../appendix/布尔型.md) 可选。为 true 且本次点亮了条目时，再发送该条目的图鉴详情和与卡片登录相同的揭示演出（ALO）。

### 返回值

条目状态发生变化时为 true；已是目标状态、对象不是玩家或编号越界时为 false。

## 参考实例

```lua
if Char.SetAlbumFlag(player, albumId, true, true) then
    NLG.SystemMessage(player, "album entry unlocked");
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有（图鉴棋局奖励用）。
位布局与图鉴读取一致（条目 N 对应第 N-1 位）；状态改变后总会重发整张图鉴标记（AL）。
