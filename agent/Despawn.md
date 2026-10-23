<!-- Generated. DO NOT EDIT. -->
# Despawn

## Agent.Despawn(CharIndex, Reason)

### 函数功能

收回一个已召出的代理角色：存档后让它离开地图。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 已召出代理的对象index。
- Reason: [字符串](../appendix/字符串.md) 收回原因，1 到 16 字节的 ASCII 短串（不能含空格和 `|`），原样传给收回事件。

### 返回值

成功返回 1。失败返回 `nil, 错误码`：`NOT_AGENT` 不是已召出的代理；`BAD_ARGS` Reason 不合法或使用了保留值；`CONTEXT` 当前上下文不允许调用；`SAVE` 存档失败（代理仍然被收回）。

## 参考实例

```lua
local ok, code = Agent.Despawn(charIndex, "rest");
```

### 备注

同步执行。引擎先触发 `NL.RegAgentDespawnEvent`（此时代理身体仍可读取，InParty 是代理此刻是否在控制者的队伍里），再让代理离队、存档、离开地图，代理回到未召出状态，卡時的打卡标志在下次召出时继续生效。
收回按真人登出的规则处理登出掉落的道具：存档之前把它们丢在代理身边的地面上（同时带丢弃消失标志的道具直接消失），所以存档和下次召出时都不再有这些道具；普通道具、装备和宠物原样保留。收回事件触发时这些道具仍在背包里。与真人登出一样，代理阵亡或周围没有空地等原因丢不出去的道具会留在存档里，下次召出时再丢一次。
保留的原因 `controller`、`capacity`、`gm`、`external` 由引擎自己使用，脚本传入时返回 `nil, "BAD_ARGS"`。
不能在战斗处理阶段（包括代理战斗指令回调和各战斗事件回调）以及 `NL.RegAgentDespawnEvent` 的回调里调用，否则返回 `nil, "CONTEXT"`。
本函数是本服务端新增的接口，C 版 gmsv 没有。
