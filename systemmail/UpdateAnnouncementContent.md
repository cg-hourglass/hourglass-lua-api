<!-- Generated. DO NOT EDIT. -->
# UpdateAnnouncementContent

## SystemMail.UpdateAnnouncementContent(actor, job_id, patch, expected_revision)

### 函数功能

只更正已发布公告标题和正文。

### 参数说明

- actor: [数值型](../appendix/数值型.md) actor 参数，详细字段见说明。
- job_id: [字符串](../appendix/字符串.md) job_id 参数，详细字段见说明。
- patch: [表](../appendix/表.md) patch 参数，详细字段见说明。
- expected_revision: [数值型](../appendix/数值型.md) expected_revision 参数，详细字段见说明。

### 返回值

任务表，content_revision递增；patch 仅 title/body，奖励与原始 mail 模板不变，不重置已读。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
