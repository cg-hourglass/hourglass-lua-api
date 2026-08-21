<!-- Generated. DO NOT EDIT. -->
# SetLoopEvent

## Char.SetLoopEvent(Dofile, FuncName, CharIndex, Interval)

### 函数功能

为对象index登记循环事件的 Lua 回调函数，每隔指定间隔触发一次。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index。
- Interval: [数值型](../appendix/数值型.md) 循环间隔，单位毫秒。

### 返回值

两个返回值。第一个是登记状态码——1 成功，-1 第二个参数不是字符串（视为注销），
-2 函数名没有解析到一个函数。第二个是本次登记之前的循环间隔，只有在这次调用真正完成挂载时
才是旧的间隔值，重复登记或注销时是 -1。
对象未通过可用性检查时只返回一个 -1。

## CharLoopCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入。

### 返回值

返回一个整数；引擎会读取但不使用它，返回 0 即可。

## 参考实例

```lua
local Status, OldInterval = Char.SetLoopEvent(nil, "MyLoop", NpcIndex, 1000);
```

### 备注

本函数是这一族登记器里唯一要求对象通过完整可用性检查的，其余几个只判断对象指针非空。
它也是唯一支持“重复登记”的：已经挂上 Lua 处理函数时再调一次，不会重新做函数表交换，
只刷新循环间隔和函数名，原本保存的前驱处理函数保持不变。
