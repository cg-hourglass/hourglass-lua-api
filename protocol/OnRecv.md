<!-- Generated. DO NOT EDIT. -->
# OnRecv

## Protocol.OnRecv(Dofile, FuncName, PacketID)

### 函数功能

为指定封包ID注册一个接收回调，可以过滤/拦截该封包在服务端的后续派发。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；回调函数若已在当前文件中定义，填 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发的 Lua 函数名称，声明格式见下方 OnRecvCallBack。
- PacketID: [数值型](../appendix/数值型.md) 封包头定义，参考附录[常量](../appendix/常量.md)。

### 返回值

成功返回注册的槽位号（大于等于0）；已达到128个上限、该封包已被其它回调注册、或试图挂钩登录令牌封包（R_TK/S_TK）时返回 -1。

## OnRecvCallBack(Fd, Head, Packet)

### 参数说明

- Fd: [数值型](../appendix/数值型.md) 触发该事件的连接套接字ID，由引擎传入；可通过 Protocol.GetCharByFd 换取对应的对象index。
- Head: [数值型](../appendix/数值型.md) 封包头定义，参考附录[常量](../appendix/常量.md)。
- Packet: [字符串](../appendix/字符串.md) 封包内容，各字段以“:”分隔（取自该封包未转义的原始行）。

### 返回值

返回0则放行该封包，服务端照常处理；返回1则拦截该封包，服务端原生的处理函数不会执行；返回其它任意数字同样视为放行。

## 参考实例

```lua
Protocol.OnRecv(nil, "MyProtocolWRecvEvent", %RECV_W%); -- 当gmsv收到W(行走)封包时会触发

function MyProtocolWRecvEvent(_fd, _head, _packet)
  return 0; -- 放行该封包
end
```

### 备注

- PacketID 命中登录令牌封包（R_TK/S_TK）时始终返回 -1，这是硬编码的安全例外，不占用注册表槽位。
- Dofile 若为字符串会先执行一次 dofile 加载该文件；加载失败只记录日志，不会中断本次注册。
- FuncName 在注册时不校验是否已经是一个函数，解析被推迟到封包实际到达、按名字查找全局变量的那一刻，所以可以先注册、后定义。
- 回调返回值只有严格等于数字 1 才会拦截封包；找不到回调、回调不是函数、执行出错、返回值不是数字等任何一种失败情形都按“放行”处理。
- 该钩子只在服务端单一的序列化处理流程上触发；其它来源产生的封包处理请求会被直接丢弃（不会误触发脚本回调），只记一次日志。
