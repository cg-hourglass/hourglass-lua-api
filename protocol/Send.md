<!-- Generated. DO NOT EDIT. -->
# Send

## Protocol.Send(CharIndex, PacketID, Packet)

### 函数功能

向指定对象发送一个自定义内容的封包。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的[对象index](../appendix/对象index.md)。
- PacketID: [数值型](../appendix/数值型.md) 封包头定义，参考附录[常量](../appendix/常量.md)。
- Packet: [字符串](../appendix/字符串.md) 封包内容，作为该封包的单个参数发送。

### 返回值

返回0失败，返回1成功。

## 参考实例

```lua
Protocol.Send(TM_PlayPtr, %SEND_MSG%, "Hello");
```

### 备注

失败情形包括：对象无效/不可用、目标没有可用的网络连接、以及 PacketID 找不到对应的封包头定义。
