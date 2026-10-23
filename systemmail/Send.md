<!-- Generated. DO NOT EDIT. -->
# Send

## SystemMail.Send(target, spec)

### 函数功能

向确切账号与角色发送持久邮件。

### 参数说明

- target: [表](../appendix/表.md) target 参数，详细字段见说明。
- spec: [表](../appendix/表.md) spec 参数，详细字段见说明。

### 返回值

{id,state,existing}；同业务键不重新生成附件。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
