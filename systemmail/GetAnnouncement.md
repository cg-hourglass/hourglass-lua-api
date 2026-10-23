<!-- Generated. DO NOT EDIT. -->
# GetAnnouncement

## SystemMail.GetAnnouncement(job_id)

### 函数功能

读取管理任务与准确持久进度。

### 参数说明

- job_id: [字符串](../appendix/字符串.md) job_id 参数，详细字段见说明。

### 返回值

任务表含 id、key、selector、mail、current_title/current_body、draft_revision/prepared_revision/content_revision、dispatch_server_number、state、counts、选择时间窗口。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
