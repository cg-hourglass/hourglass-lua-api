<!-- Generated. DO NOT EDIT. -->
# List

## SystemMail.List(player, opts)

### 函数功能

分页列出本人可见邮件。

### 参数说明

- player: [数值型](../appendix/数值型.md) player 参数，详细字段见说明。
- opts: [表](../appendix/表.md) opts 参数，详细字段见说明。

### 返回值

{entries,next_cursor}；opts 为 cursor、anchor_id、limit（1..10）、filter（all/pending）。anchor_id 与 cursor 互斥，从本人可见定位项开始，不标记已读。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
