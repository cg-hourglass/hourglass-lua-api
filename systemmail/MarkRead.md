<!-- Generated. DO NOT EDIT. -->
# MarkRead

## SystemMail.MarkRead(player, mail_id)

### 函数功能

幂等标记本人的一封可见邮件已读。

### 参数说明

- player: [数值型](../appendix/数值型.md) player 参数，详细字段见说明。
- mail_id: [字符串](../appendix/字符串.md) mail_id 参数，详细字段见说明。

### 返回值

1；读取正文成功后由界面显式调用。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
