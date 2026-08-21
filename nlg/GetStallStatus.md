<!-- Generated. DO NOT EDIT. -->
# GetStallStatus

## NLG.GetStallStatus(CharIndex)

### 函数功能

获取玩家的摆摊状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

-1表示未开过摊/不是玩家；0表示摆摊准备中；>=1表示正在摆摊中。

## 参考实例

```lua
local status = NLG.GetStallStatus(player);
```
