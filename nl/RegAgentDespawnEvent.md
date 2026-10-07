<!-- Generated. DO NOT EDIT. -->
# RegAgentDespawnEvent

## NL.RegAgentDespawnEvent(Dofile, FuncName)

### 函数功能

注册代理角色被收回时触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AgentDespawnCallBack(Cdkey, CharIndex, Reason, InParty)

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号，服务器编码的原始字节。
- CharIndex: [数值型](../appendix/数值型.md) 代理角色的对象index；外部注销时为 -1。
- Reason: [字符串](../appendix/字符串.md) 收回原因。脚本收回时是脚本传入的原因串；`controller` 控制者不在场；`capacity` 为腾出服务器名额而收回；`gm` 由 GM 收回；`external` 外部注销。
- InParty: [数值型](../appendix/数值型.md) 代理是否在控制者的队伍里：1 在，0 不在。外部注销时恒为 0。

### 返回值

无

## 参考实例

```lua
NL.RegAgentDespawnEvent(nil, "MyAgentDespawnEvent");

function MyAgentDespawnEvent(Cdkey, CharIndex, Reason, InParty)
  if CharIndex >= 0 then
    -- 身体仍可读取；这里只能用 Agent.SetMeta 记录状态
  end
  if Reason == "controller" and InParty == 1 then
    -- 控制者离开时代理还在队伍里
  end
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
引擎收回代理时，本事件在代理注销之前触发，此时身体仍可读取；回调里只允许用 `Agent.SetMeta` 写入数据，召出、收回、删除代理、采集、转移与存档等接口都会返回 `nil, "CONTEXT"`。
回调看到的背包仍含登出掉落的道具：引擎在回调返回之后才按真人登出的规则把它们丢到地上（或让带丢弃消失标志的道具消失），再存档。外部注销经过登出时（例如 GM 让全员登出），这一步在该次登出里完成，补发的事件触发时道具已经不在。
代理被引擎以外的途径注销（外部注销）时，本事件在注销之后的服务器循环里补发，CharIndex 为 -1，Reason 为 `external`。
InParty 反映代理离队之前的状态（引擎触发本事件后才让代理离队）。Reason 为 `controller` 时，控制者的登出本身已经解散了队伍，所以 InParty 取的是控制者最后一次在场时（上一个服务器循环）的采样：控制者在场期间队伍已被解散（例如逃跑成功）再登出，得到 0；入队后在下一次采样前就登出，得到 1。离队与控制者离开发生在同一个服务器循环里（例如逃跑成功的同一循环内控制者超时断线）时，取到的仍是上一个循环的 1。其他原因取触发时的实时状态。
只声明三个参数的旧处理函数照常运行，多出的 InParty 被忽略。
本函数是本服务端新增的接口，C 版 gmsv 没有。
