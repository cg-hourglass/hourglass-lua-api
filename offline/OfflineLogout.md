<!-- Generated. DO NOT EDIT. -->
# OfflineLogout

## Offline.OfflineLogout(CharIndex)

### 函数功能

强制结束当前离线挂机角色的登录状态（立即登出）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是玩家类型。

### 返回值

0 失败（对象无效或当前并非离线状态）；1 成功。

## 参考实例

```lua
Offline.OfflineLogout(player);
```

### 备注

成功时只是把结束时间设为当前时间，真正的登出由离线管理器的过期扫描
在下一次巡检时执行，不是本调用同步完成。
