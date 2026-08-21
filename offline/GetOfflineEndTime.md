<!-- Generated. DO NOT EDIT. -->
# GetOfflineEndTime

## Offline.GetOfflineEndTime(CharIndex)

### 函数功能

获取指定玩家离线挂机的结束时间。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是玩家类型。

### 返回值

结束时间的 timestamp（秒）；目标不是有效玩家时返回 0。

## 参考实例

```lua
local endSec = Offline.GetOfflineEndTime(player);
```
