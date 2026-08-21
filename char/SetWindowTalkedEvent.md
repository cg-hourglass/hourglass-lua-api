<!-- Generated. DO NOT EDIT. -->
# SetWindowTalkedEvent

## Char.SetWindowTalkedEvent(Dofile, FuncName, CharIndex)

### 函数功能

为对象index登记“对话框交互”事件的 Lua 回调函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调就写在当前文件里时传 nil 即可。
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名。
- CharIndex: [数值型](../appendix/数值型.md) 登记事件的对象index，通常是 NPC。

### 返回值

登记状态码——1 成功，-1 第二个参数不是字符串（视为注销），-2 函数名没有解析到一个函数。
对象index无法解析时返回 -1。

## CharWindowTalkedCallBack(CharIndex, TalkerCharIndex, SeqNo, Select, Data)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象index，由引擎传入，一般是 NPC。
- TalkerCharIndex: [数值型](../appendix/数值型.md) 触发事件的对象index，由引擎传入，一般是玩家。
- SeqNo: [数值型](../appendix/数值型.md) 来源对话框的 ID，与 NLG.ShowWindowTalked 中的定义一一对应。
- Select: [数值型](../appendix/数值型.md) 玩家按下的按钮值，或选择框中被选中项的值。
- Data: [字符串](../appendix/字符串.md) 客户端回传的数据，具体含义随窗口类型而不同。

### 返回值

无返回值。

## 参考实例

```lua
Char.SetWindowTalkedEvent(nil, "MyWindowTalked", NpcIndex);
```

### 备注

已经挂上 Lua 处理函数后再登记一次是完全的空操作，连函数名都不会刷新。
