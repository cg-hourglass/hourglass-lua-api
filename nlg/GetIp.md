<!-- Generated. DO NOT EDIT. -->
# GetIp

## NLG.GetIp(CharIndex)

### 函数功能

获取玩家当前连接的IP地址。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

玩家的IP地址字符串（不含端口）；目标不是当前在线玩家时返回空字符串 ""。

## 参考实例

```lua
local ip = NLG.GetIp(player);
```
