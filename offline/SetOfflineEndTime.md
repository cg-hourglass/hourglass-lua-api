<!-- Generated. DO NOT EDIT. -->
# SetOfflineEndTime

## Offline.SetOfflineEndTime(CharIndex, AdditionTime)

### 函数功能

重新设置离线挂机角色的结束时间（从当前时间起续期）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 离线登录角色的对象 index，必须是玩家类型。
- AdditionTime: [数值型](../appendix/数值型.md) 从当前时间点续期的秒数；传 0 则结束时间等于当前时间（等效立即登出触发点）。

### 返回值

0 表示失败（对象无效，或对象当前并未处于离线状态）；其他值为新的结束时间 timestamp（秒）。

## 参考实例

```lua
local newEnd = Offline.SetOfflineEndTime(player, 300); -- 从现在起再续期 300 秒
```

### 备注

仅对当前确实处于离线状态（Offline.GetOfflineStatus 为 1）的对象生效，
非离线状态直接返回 0，不会把角色“设置为离线”。
