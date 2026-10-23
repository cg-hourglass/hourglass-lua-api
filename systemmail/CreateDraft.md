<!-- Generated. DO NOT EDIT. -->
# CreateDraft

## SystemMail.CreateDraft(actor, spec)

### 函数功能

用固定业务键创建持久草稿。

### 参数说明

- actor: [数值型](../appendix/数值型.md) actor 参数，详细字段见说明。
- spec: [表](../appendix/表.md) spec 参数，详细字段见说明。

### 返回值

任务表；spec 为 key、title、body、selector、items、gold、expires_at，不生成物品。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
