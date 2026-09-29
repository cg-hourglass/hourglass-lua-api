<!-- Generated. DO NOT EDIT. -->
# SetStallOffline

## NLG.SetStallOffline(CharIndex, On)

### 函数功能

设置摊主的离线摆摊开关（摆摊扩展）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 摊主的对象index，必须正在摆摊。
- On: [布尔型](../appendix/布尔型.md) true 开启、false 关闭；也可以传数值，非 0 为开启。

### 返回值

成功返回 0；离线摆摊未开启（配置 `stall.offline.enabled`）或对象没有在摆摊时返回 -1。

## 参考实例

```lua
if NLG.StallStart(player, "小铺", "", {[8] = {gold = 500}}) == 0 then
  NLG.SetStallOffline(player, true);
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
开关随收摊一起清除，重新开摊后需要再次设置。NLG.GetStallList 的 offline_opt 字段反映这个开关。
开关打开的摊主断线或主动登出时，如果不在战斗、交易或观战中，就不走登出流程：角色留在世界里、改挂到一个负数会话号上继续摆摊，账号保持锁定，登出（Logout / Drop）事件此时不触发。主动登出的客户端照常收到登出成功。之后 NLG.GetStallList 的 offline 为 true，成交事件的 SellerOffline 为 1。
离线摊位在以下时候结束：该账号重新登录（任意角色）、离线时长到期（配置 `stall.offline.max_hours`）或停服。前两种会先收摊（周围玩家看到摊位消失），再按超时断线登出并存盘（此时触发一次 Drop 事件），然后注销角色、解除账号锁定；停服时随全服存盘一起保存并解锁。
摊主已经离线后再关闭开关，不会让摊位提前结束。
