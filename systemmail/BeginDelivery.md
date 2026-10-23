<!-- Generated. DO NOT EDIT. -->
# BeginDelivery

## SystemMail.BeginDelivery(player, mail_id, policy)

### 函数功能

校验当前角色并开始系统投递。

### 参数说明

- player: [数值型](../appendix/数值型.md) player 参数，详细字段见说明。
- mail_id: [字符串](../appendix/字符串.md) mail_id 参数，详细字段见说明。
- policy: [表](../appendix/表.md) policy 参数，详细字段见说明。

### 返回值

{id,handle,state,ready_at,depart_at,expires_at,mail_expires_at?}；policy 仅受信任脚本传入 travel_seconds/depart_seconds/ttl_seconds，默认3/1/15。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
