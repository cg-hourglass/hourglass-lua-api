# 说明

Protocol 库用于处理游戏服务端的封包收发：可以拦截/过滤客户端发给服务端的封包（`Protocol.OnRecv`），可以旁观服务端发给客户端的每一个封包（全局函数 `ServerProtocolSend`），也可以直接向指定对象发送封包，或注册、收发脚本自定义的封包类型。

## 拦截客户端封包：Protocol.OnRecv

用 `Protocol.OnRecv` 为某个封包头注册一个回调后，服务端每收到一个属于该封包头的客户端封包，都会先把封包内容交给这个回调；回调返回 1 会拦截该封包（服务端原生的处理逻辑完全不会执行，等同于把这个封包在服务端一侧“吃掉”），返回 0（或其它任何非 1 的值，乃至回调本身出错）则放行，服务端照常处理。详见 [OnRecv](OnRecv.md)。

## 旁观服务端发出的封包：ServerProtocolSend

这不是通过 `Protocol.*` 下的某个函数注册的，而是脚本直接定义一个名为 `ServerProtocolSend(Fd, Packet)` 的全局函数——服务端每发送一个封包（不论是不是由脚本触发）都会调用它一次。这是一个纯旁观钩子：返回值不会被读取，也没有办法拦截发送；`Packet` 是已经编码好、即将写上连接的原始封包文本，不是脚本能直接理解的“文本消息”。

## 主动发送封包

- `Protocol.Send(CharIndex, PacketID, Packet)` —— 用已有的原生（或 `Protocol.AddPacket` 注册的自定义）封包头，向指定对象发送一段内容。
- `Protocol.RawSend(CharIndex, Packet)` —— 跳过封包头查找与参数转义，把 `Packet` 原样写给指定对象（自动补换行）；不会触发 `ServerProtocolSend`。
- `Protocol.SendLuaCustomPacket(CharIndex, Para1, Para2)` —— 走固定的 Lua 自定义封包通道，对端脚本用全局函数 `RecvLuaCustomPacket(Fd, CharIndex, Para1, Para2)` 接收。

## 自定义封包类型：Protocol.AddPacket

`Protocol.AddPacket(RecvHeader, SendHeader)` 注册一对脚本自定义的封包头标识，返回值是这对标识在内部注册表里的槽位号；之后可以配合 `Protocol.Send`/`Protocol.OnRecv` 使用这个自定义封包头收发数据。该注册表与 `Protocol.OnRecv` 的回调表共用同一份 128 条上限。

## 其它

`Protocol.GetCharByFd(Fd)` 用连接的套接字ID换取对应的玩家对象index，常用在 `Protocol.OnRecv` 的回调里，把回调收到的 `Fd` 转成可以调用 `Char.*`/`NLG.*` 接口的对象index。
