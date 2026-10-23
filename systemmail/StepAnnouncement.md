<!-- Generated. DO NOT EDIT. -->
# StepAnnouncement

## SystemMail.StepAnnouncement(job_id, opts)

### 函数功能

推进一个有界的选择、发送或撤回批次。

### 参数说明

- job_id: [字符串](../appendix/字符串.md) job_id 参数，详细字段见说明。
- opts: [表](../appendix/表.md) opts 参数，详细字段见说明。

### 返回值

公告任务表；limit 1..100，仅负责服可执行。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
