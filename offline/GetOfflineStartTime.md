<!-- Generated. DO NOT EDIT. -->
# GetOfflineStartTime

## Offline.GetOfflineStartTime(CharIndex)

### 函数功能

获取指定玩家离线挂机的开始时间。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是玩家类型。

### 返回值

开始时间的 timestamp（秒）；目标不是有效玩家时返回 0。

## 参考实例

```lua
local startSec = Offline.GetOfflineStartTime(player);
```
