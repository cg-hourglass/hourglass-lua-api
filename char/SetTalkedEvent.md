<!-- Generated. DO NOT EDIT. -->
# SetTalkedEvent

## Char.SetTalkedEvent(Dofile, FuncName, CharIndex)

### 函数功能

为对象index登记“被搭话”事件的 Lua 回调函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index，通常是 NPC。

### 返回值

登记状态码——1 成功，-1 第二个参数不是字符串（视为注销），-2 函数名没有解析到一个函数。
对象index无法解析时返回 -1。

## CharTalkedCallBack(CharIndex, TalkerCharIndex, Message)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入，一般是 NPC。
- TalkerCharIndex: [数值型](../appendix/数值型.md) 发起搭话的对象index，由引擎传入，一般是玩家。
- Message: [字符串](../appendix/字符串.md) 玩家说出的文本内容，由引擎传入。

### 返回值

无返回值。

## 参考实例

```lua
Char.SetTalkedEvent(nil, "MyTalked", NpcIndex);
```

### 备注

引擎内部拿到的搭话信息比传给 Lua 的多：只有 charIndex、发话者index、消息文本这三个会进入回调，
颜色与频道参数不会传递到脚本层。
已经挂上 Lua 处理函数后再登记一次是完全的空操作，连函数名都不会刷新；
要换处理函数得先用一个解析不到函数的名字注销，再重新登记。
