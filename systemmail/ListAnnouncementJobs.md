<!-- Generated. DO NOT EDIT. -->
# ListAnnouncementJobs

## SystemMail.ListAnnouncementJobs(opts)

### 函数功能

分页查找公告任务。

### 参数说明

- opts: [表](../appendix/表.md) opts 参数，详细字段见说明。

### 返回值

{entries,next_cursor}；entries 为不含正文、selector、奖励的任务摘要，含 id/key/state/current_title/dispatch_server_number/source/updated_at/recipient_count/counts。默认本服活动任务；管理入口 scope="all"、states、cursor、limit<=10。实际条数同时受单帧编码预算约束。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
