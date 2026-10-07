<!-- Generated. DO NOT EDIT. -->
# GetMAC

## NLG.GetMAC(CharIndex)

### 函数功能

获取玩家登录时上报的MAC地址（本版本已启用MAC地址限制功能）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

玩家的MAC地址字符串；目标不是当前在线玩家时返回空字符串 ""。

## 参考实例

```lua
local mac = NLG.GetMAC(player);
```
