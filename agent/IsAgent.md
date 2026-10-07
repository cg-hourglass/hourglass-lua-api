<!-- Generated. DO NOT EDIT. -->
# IsAgent

## Agent.IsAgent(CharIndex)

### 函数功能

判断一个对象是不是代理角色。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index。

### 返回值

是代理角色返回 1，否则返回 0。

## 参考实例

```lua
for entry = 0, 9 do
  local charIndex = Battle.GetPlayIndex(battleIndex, entry);
  if charIndex >= 0 and Agent.IsAgent(charIndex) == 0 then
    -- 只给真人玩家发奖励
  end
end
```

### 备注

只读。注意返回值 0 在 Lua 里也是真值，判断时要写 `== 1`。对玩家生效的事件（战斗、经验、升级、传送、队伍等）同样会对代理触发，脚本可以用本函数把代理排除在外。
本函数是本服务端新增的接口，C 版 gmsv 没有。
