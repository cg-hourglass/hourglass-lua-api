<!-- Generated. DO NOT EDIT. -->
# IsAgentOf

## Agent.IsAgentOf(AgentIndex, ControllerIndex)

### 函数功能

检查已召出的代理是否属于当前在场控制者及其原生登录 generation。

### 参数说明

- AgentIndex: [数值型](../appendix/数值型.md) 已召出代理的对象 index。
- ControllerIndex: [数值型](../appendix/数值型.md) 当前控制者的对象 index。

### 返回值

完全匹配返回 1，否则返回 0。

## 参考实例

```lua
if Agent.IsAgentOf(agent, controller) == 1 then
    print("agent belongs to this live controller");
end
```

### 备注

只读，复用原生 IsAgentOf。检查当前 controller 对象、账号/角色身份、在场状态和登录 generation。
同名、同 index 重新登录后，旧代理在下一次 AgentLoop 收回前也返回 0；不得只凭 Lua 缓存的 controller_index 授权。
