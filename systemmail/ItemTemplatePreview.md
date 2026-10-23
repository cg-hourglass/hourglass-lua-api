<!-- Generated. DO NOT EDIT. -->
# ItemTemplatePreview

## SystemMail.ItemTemplatePreview(actor, item_id)

### 函数功能

只读预览合法模板，不创建奖励资产。

### 参数说明

- actor: [数值型](../appendix/数值型.md) actor 参数，详细字段见说明。
- item_id: [数值型](../appendix/数值型.md) item_id 参数，详细字段见说明。

### 返回值

{item_id,display_name,graphic,max_stack}；无权限 FORBIDDEN，非法模板 INVALID_ITEM。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
