<!-- Generated. DO NOT EDIT. -->
# Get

## SystemMail.Get(player, mail_id, opts)

### 函数功能

读取正文和一页附件摘要，不自动阅读。

### 参数说明

- player: [数值型](../appendix/数值型.md) player 参数，详细字段见说明。
- mail_id: [字符串](../appendix/字符串.md) mail_id 参数，详细字段见说明。
- opts: [表](../appendix/表.md) opts 参数，详细字段见说明。

### 返回值

{id,announcement_id,title,body,sender,state,created_at,read_at,claimed_at,expires_at,gold,attachment_count,attachment_page,attachments}；附件为 {index,display_name,graphic,amount}，每页10条，最多2页。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
