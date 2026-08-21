<!-- Generated. DO NOT EDIT. -->
# GetCharByFd

## Protocol.GetCharByFd(Fd)

### 函数功能

根据网络连接套接字ID获取对应的玩家对象index。

### 参数说明

- Fd: [数值型](../appendix/数值型.md) 玩家客户端连接的套接字ID。

### 返回值

成功返回对象index；套接字无效、或未关联可用的玩家对象时返回 -1。

## 参考实例

```lua
local charindex = Protocol.GetCharByFd(_fd);
```
