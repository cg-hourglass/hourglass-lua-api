<!-- Generated. DO NOT EDIT. -->
# SetItemPutEvent

## Char.SetItemPutEvent(Dofile, FuncName, CharIndex)

### 函数功能

为对象index登记“有道具被丢在附近”事件的 Lua 回调函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index，通常是 NPC。

### 返回值

登记状态码——1 成功，-1 第二个参数不是字符串（视为注销），-2 函数名没有解析到一个函数。
对象index无法解析时返回 -1。

## CharItemPutCallBack(CharIndex, ItemIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入，一般是 NPC。
- ItemIndex: [数值型](../appendix/数值型.md) 被丢下的道具index，由引擎传入。

### 返回值

返回一个布尔值。真值表示这次投放已被回调消化掉，服务端不再走默认的落地处理；
假值（nil 或 false）表示交回服务端按常规处理。

## 参考实例

```lua
Char.SetItemPutEvent(nil, "MyItemPut", NpcIndex);
```

### 备注

引擎按 Lua 的真值规则读这个返回值，而 Lua 里数字 0 也是真值——想让服务端继续处理，
必须返回 nil 或 false，返回 0 等同于“已消化”。这一点与直觉相反，是沿袭旧版的行为。
