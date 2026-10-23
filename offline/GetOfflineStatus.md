<!-- Generated. DO NOT EDIT. -->
# GetOfflineStatus

## Offline.GetOfflineStatus(CharIndex)

### 函数功能

获取指定玩家当前是否处于离线挂机状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是玩家类型。

### 返回值

0 未离线，1 离线中。目标不是有效玩家时同样返回 0。

## 参考实例

```lua
local status = Offline.GetOfflineStatus(player);
```
