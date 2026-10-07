<!-- Generated. DO NOT EDIT. -->
# SetMeta

## Agent.SetMeta(Cdkey, Bytes)

### 函数功能

保存代理角色的自定义数据。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号。
- Bytes: [字符串](../appendix/字符串.md) 要保存的字节串，最长 4096 字节；引擎原样保存，不解释内容。

### 返回值

成功返回 1。失败返回 `nil, 错误码`：`NO_AGENT` 没有这个代理；`NOT_LOADED` 代理的控制者不在线；`TOO_LONG` 超过 4096 字节；`BAD_ARGS` Bytes 不是字符串；`DB` 写库失败。

## 参考实例

```lua
local ok, code = Agent.SetMeta(cdkey, "rank=2;tactic=heal");
```

### 备注

同步执行，返回时已写库。代理不需要召出，控制者在线即可写入。
本函数可以在 `NL.RegAgentDespawnEvent` 的回调里调用，用来在代理被收回前记录状态；该回调里其他会改变代理的接口都会返回 `nil, "CONTEXT"`。
建议只保存 ASCII 内容，便于不同编码的服务器之间迁移。
本函数是本服务端新增的接口，C 版 gmsv 没有。
