<!-- Generated. DO NOT EDIT. -->
# SetPreOverEvent

## Char.SetPreOverEvent(Dofile, FuncName, CharIndex)

### 函数功能

为对象index登记“覆盖其他对象前”事件的 Lua 回调函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index。

### 返回值

登记状态码——1 成功，-1 第二个参数不是字符串（视为注销），-2 函数名没有解析到一个函数。
对象index无法解析时返回 -1。

## PreOverEventCallBack(CharIndex, TargetCharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入。
- TargetCharIndex: [数值型](../appendix/数值型.md) 被覆盖的目标对象index，由引擎传入。

### 返回值

无返回值。

## 参考实例

```lua
Char.SetPreOverEvent(nil, "MyPreOver", NpcIndex);
```

### 备注

本槽位在本服务端只做登记，不会触发，函数名会被记录但流程不会回调它。
已经挂上 Lua 处理函数后再登记一次是空操作。
