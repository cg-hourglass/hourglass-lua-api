<!-- Generated. DO NOT EDIT. -->
# SetWalkPreEvent

## Char.SetWalkPreEvent(Dofile, FuncName, CharIndex)

### 函数功能

为对象index登记“行走前”事件的 Lua 回调函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index。

### 返回值

登记状态码——1 表示脚本已加载且函数名解析成功，-1 表示第二个参数不是字符串（视为注销），
-2 表示函数名没有解析到一个函数。对象index无法解析时返回 -1。

## CharWalkPreCallBack(CharIndex, Dir, Mode)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入。
- Dir: [数值型](../appendix/数值型.md) 本次行走的方向，由引擎传入。
- Mode: [数值型](../appendix/数值型.md) 本次行走的模式，由引擎传入。

### 返回值

依次返回 Mode、Dir、是否放行（布尔）三个值；引擎从栈顶往回读，所以顺序是反的。

## 参考实例

```lua
Char.SetWalkPreEvent(nil, "MyWalkPre", NpcIndex);
```

### 备注

本槽位在本服务端只做登记，不会触发：登记的函数名会被完整记录下来，但行走流程不会回调它。
同族登记器都是“只保存一层前驱”：已经挂上 Lua 处理函数后再登记一次是完全的空操作，连函数名都不刷新。
