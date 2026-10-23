<!-- Generated. DO NOT EDIT. -->
# CompleteDelivery

## SystemMail.CompleteDelivery(handle)

### 函数功能

到达 ready_at 后整封发放，并执行普通保存。

### 参数说明

- handle: [字符串](../appendix/字符串.md) handle 参数，详细字段见说明。

### 返回值

投递状态表；发放成功为 claimed。保存错误不会重新开放领取；depart_at 按实际完成时间计算且不超过资源TTL。

## 参考实例

```lua
-- 参阅 SystemMail 说明中的受信任服务示例。
```

### 备注

成功返回表（Configure/MarkRead 为 1），失败返回 nil, code, detail。
player/actor 是当前真人角色的整数索引，每次调用重新校验会话。
只有受信任服务器脚本可直接使用本命名空间；玩家网络入口不能任意分发函数名。
