<!-- Generated. DO NOT EDIT. -->
# Spawn

## Agent.Spawn(Cdkey, Opts)

### 函数功能

召出一个未召出的代理角色，让它出现在指定对象身边。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号。
- Opts: [表](../appendix/表.md) 选项表。`near` 为落点参照对象的对象index，省略时为控制者。 [可为空]

### 返回值

召出请求被受理时返回 1，结果之后经 `NL.RegAgentSpawnEvent` 送达。立即失败时返回 `nil, 错误码`：`NO_AGENT` 没有这个代理；`NOT_LOADED` 代理的控制者不在线；`ONLINE` 代理已召出、正在召出或正在被收回；`CONTROLLER` 控制者不在场；`FULL` 服务器剩余玩家名额不足；`BAD_ARGS` Opts 不是表，或 near 不是可用的对象；`CONTEXT` 当前上下文不允许调用。

## 参考实例

```lua
NL.RegAgentSpawnEvent(nil, "OnAgentSpawn");

function OnAgentSpawn(cdkey, charIndex, code)
  if code == "OK" then
    Agent.JoinParty(charIndex);
  end
end

Agent.Spawn(cdkey, { near = player });
```

### 备注

异步执行：返回 1 只表示已受理。引擎读取完整的角色数据后，把代理放在 near 所在楼层、身边的可行走格子上；召出事件最早在下一次服务器循环触发，此时代理已经可以被各接口操作。读档失败或 30 秒内没有完成时以 `LOAD` 结果触发，状态回到未召出。
服务器剩余玩家名额少于配置项 `agent.reserve_player_slots`（默认 10）时返回 `FULL`，代理不会挤占真人的登录名额；玩家名额已满时真人登录会让引擎先收回一个代理。
召出的代理不会触发登录类事件（Login、LoginGate、GetLoginPoint 等），不登记名片，不计入在线人数。控制者不在场后，引擎在下一次服务器循环里收回它的全部代理（收回原因 `controller`）。
不能在战斗处理阶段（包括代理战斗指令回调和各战斗事件回调）以及 `NL.RegAgentDespawnEvent` 的回调里调用，否则返回 `nil, "CONTEXT"`。
本函数是本服务端新增的接口，C 版 gmsv 没有。
