<!-- Generated. DO NOT EDIT. -->
# SetOfflinePlayer

## Offline.SetOfflinePlayer(CharIndex, Duration)

### 函数功能

设置指定玩家进入离线挂机状态，并保持指定时长。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是当前在线的玩家。
- Duration: [数值型](../appendix/数值型.md) 离线挂机维持的时长，单位秒。

### 返回值

0 失败，1 成功。

## 参考实例

```lua
Offline.SetOfflinePlayer(player, 600); -- 让该玩家离线挂机 600 秒
```

### 备注

玩家离线后角色不会从地图上消失，会保持当前位置与动作（例如摆摊中的
角色可以继续摆摊），到达指定时间后自动登出。玩家离线挂机期间如果该
帐号发起新的登录请求，会把当前的离线挂机会话直接顶下线。已离线（无
活跃会话）的对象再次调用会因为找不到可分离的连线而返回 0。本函数与
`NLG.SetOfflinePlayer` 是同一实现（不在本文档范围）。
