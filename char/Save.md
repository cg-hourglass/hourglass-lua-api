<!-- Generated. DO NOT EDIT. -->
# Save

## Char.Save(CharIndex)

### 函数功能

立即同步保存一个在线玩家（含代理角色）的存档。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 要保存的玩家对象index。

### 返回值

成功返回 1；失败返回 nil 和错误码字符串：
`BAD_ARGS`（对象不是可用的玩家）、`BUSY`（该角色正在保存中）、`DB`（数据库写入失败）、
`CONTEXT`（在 AgentDespawn 回调里、或代理收回过程中触发的事件（如它离开战斗时的 BattleExit）里调用；收回本身会保存代理）。

## 参考实例

```lua
local ok, err = Char.Save(player);
if not ok then
    print("save failed: " .. err);
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
存档是当前状态的快照，与战斗不冲突，战斗中也可以调用。保存在调用线程上同步完成，会阻塞到数据库写完为止，不要在高频回调里反复调用。
