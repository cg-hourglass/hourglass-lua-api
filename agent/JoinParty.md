<!-- Generated. DO NOT EDIT. -->
# JoinParty

## Agent.JoinParty(CharIndex)

### 函数功能

让已召出的代理角色加入它控制者的队伍。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 已召出代理的对象index。

### 返回值

成功（或代理已在控制者的队伍里）返回 1。失败返回 `nil, 错误码`：`NOT_AGENT` 不是已召出的代理；`NO_CONTROLLER` 控制者不在场；`STATE` 代理或控制者正在战斗、观战、交易或摆摊，或代理已经在别的队伍里；`FLOOR` 两者不在同一楼层；`NOT_LEADER` 控制者在别人的队伍里；`BUS` 控制者在巴士队伍里；`FULL` 队伍已满；`VETO` 被 `NL.RegPartyEvent` 的回调否决。

## 参考实例

```lua
local ok, code = Agent.JoinParty(charIndex);
if ok == nil then
  print("入队失败：" .. code);
end
```

### 备注

同步执行。控制者单人时成为队长，代理成为队员，之后按普通队员跟随队长。不检查控制者的组队开关，也不要求两者相邻。入队前会触发队伍事件，回调可以否决。
代理只能加入自己控制者的队伍，永远不当队长；其他玩家不能主动加入代理，也不能把代理拉进别的队伍。让代理离队用 `Char.DischargeParty`，并检查它的返回值（离队同样可能被队伍事件否决）。
本函数是本服务端新增的接口，C 版 gmsv 没有。
