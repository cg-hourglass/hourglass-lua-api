<!-- Generated. DO NOT EDIT. -->
# RawSend

## Protocol.RawSend(CharIndex, Packet)

### 函数功能

向指定对象发送一段未经封包头封装的原始数据。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的[对象index](../appendix/对象index.md)。
- Packet: [字符串](../appendix/字符串.md) 要原样写入连接的数据；发送时引擎会自动补上一个换行符。

### 返回值

返回0失败，返回1成功。

## 参考实例

```lua
Protocol.RawSend(TM_PlayPtr, "S_TK 123:456:");
```

### 备注

与 Protocol.Send 不同，RawSend 不做封包头查找、不对内容做转义处理，也不会触发 ServerProtocolSend 观察者钩子——写入的是脚本自己拼好的完整封包文本，按原始字节写出，不做任何编码转换。对象处于离线状态、或对象无效/没有可用连接时失败并返回0。
