<!-- Generated. DO NOT EDIT. -->
# AddPacket

## Protocol.AddPacket(RecvHeader, SendHeader)

### 函数功能

注册一对脚本自定义的封包头（接收/发送标识），用于承载脚本自己扩展的协议。

### 参数说明

- RecvHeader: [字符串](../appendix/字符串.md) 自定义封包的接收方向标识。
- SendHeader: [字符串](../appendix/字符串.md) 自定义封包的发送方向标识。

### 返回值

成功返回分配给这对标识的注册槽位号；已达到128个上限、或该接收/发送标识组合已经注册过时返回 -1。

## 参考实例

```lua
local slot = Protocol.AddPacket("MYRECV", "MYSEND");
```

### 备注

- 与 Protocol.OnRecv 共享同一张128槽的注册表，二者合计不能超过这个上限。
- RecvHeader/SendHeader 作为封包头写入协议层的原生3字节包头表，超出3字节的部分会被截断，建议只使用ASCII标识。
