<!-- Generated. DO NOT EDIT. -->
# SendLuaCustomPacket

## Protocol.SendLuaCustomPacket(CharIndex, Para1, Para2)

### 函数功能

发送Lua自定义封包，固定走服务端的自定义封包通道。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的[对象index](../appendix/对象index.md)。
- Para1: [字符串](../appendix/字符串.md) 封包内容一。
- Para2: [字符串](../appendix/字符串.md) 封包内容二。

### 返回值

返回0失败，返回1成功。

## 参考实例

```lua
Protocol.SendLuaCustomPacket(TM_PlayPtr, "cmd", "1");
```

### 备注

对端需要定义全局函数 RecvLuaCustomPacket(Fd, CharIndex, Para1, Para2) 才能接收，详见[Protocol 说明](guide.md)。对象处于离线状态、或对象无效/没有可用连接时都会失败并返回0。
