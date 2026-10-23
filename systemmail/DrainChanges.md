<!-- Generated. DO NOT EDIT. -->
# DrainChanges

## SystemMail.DrainChanges(opts)

### 函数功能

有界取出本进程会话失效提示。

### 参数说明

- opts: [表](../appendix/表.md) opts 参数，详细字段见说明。

### 返回值

{entries}；limit 1..100；每项 {char_index,reason}，按具体真人会话合并。不是持久推送队列。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
