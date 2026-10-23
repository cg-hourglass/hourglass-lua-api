<!-- Generated. DO NOT EDIT. -->
# EndDelivery

## SystemMail.EndDelivery(handle, reason)

### 函数功能

幂等清理系统投递表现。

### 参数说明

- handle: [字符串](../appendix/字符串.md) handle 参数，详细字段见说明。
- reason: [字符串](../appendix/字符串.md) reason 参数，详细字段见说明。

### 返回值

{handle,state="ended"}；未发放且仍属于本会话时恢复 pending，claimed 不回退。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
