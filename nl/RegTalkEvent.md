<!-- Generated. DO NOT EDIT. -->
# RegTalkEvent

## NL.RegTalkEvent(Dofile, FuncName)

### 函数功能

注册玩家说话时触发的 Lua 函数，可用来做自定义指令、GM 命令与聊天过滤。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## TalkEventCallBack(CharIndex, Msg, Color, Range, Size)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 说话的玩家对象index，由引擎传入。
- Msg: [字符串](../appendix/字符串.md) 说话内容，已经过转义符剥离，由引擎传入。
- Color: [数值型](../appendix/数值型.md) 说话颜色，由引擎传入。
- Range: [数值型](../appendix/数值型.md) 说话音量（传播范围），由引擎传入。
- Size: [数值型](../appendix/数值型.md) 说话字体大小，由引擎传入。

### 返回值

返回0拦截这句话（不发送）；返回非0正常发送。未注册、解析失败或调用出错时默认发送。

## 参考实例

```lua
NL.RegTalkEvent(nil, "MyTalkEvent");

function MyTalkEvent(CharIndex, Msg, Color, Range, Size)
  print("玩家说话内容为:"..Msg); -- 输出到 gmsv 控制台
  return 1;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
Msg 是剥离转义符之后、且在 [rerb] / /r / [version] 等命令处理之前的文本；空消息在触发点之前就被过滤掉，不会进入本回调。
