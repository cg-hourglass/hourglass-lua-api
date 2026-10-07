<!-- Generated. DO NOT EDIT. -->
# Delete

## Agent.Delete(Cdkey)

### 函数功能

删除一个未召出的代理角色，连同它的全部角色数据与登记。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号。

### 返回值

成功返回 1。失败返回 `nil, 错误码`：`NO_AGENT` 没有这个代理；`NOT_LOADED` 代理的控制者不在线；`SPAWNING` 代理正在召出；`SPAWNED` 代理已召出（先收回再删除）；`CONTEXT` 当前上下文不允许调用；`DB` 写库失败。

## 参考实例

```lua
local ok, code = Agent.Delete(cdkey);
if ok == nil and code == "SPAWNED" then
  Agent.Despawn(Agent.Get(cdkey), "dismiss");
end
```

### 备注

同步执行，返回时已完成删除。只能删除处于未召出状态的代理；物品、宠物、技能等全部随角色一起删除，不可恢复。
不能在战斗处理阶段（包括代理战斗指令回调和各战斗事件回调）以及 `NL.RegAgentDespawnEvent` 的回调里调用，否则返回 `nil, "CONTEXT"`。
删除控制者角色时，引擎会一并删除它名下的全部代理。
本函数是本服务端新增的接口，C 版 gmsv 没有。
