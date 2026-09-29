<!-- Generated. DO NOT EDIT. -->
# ShowWindowTalked

## NLG.ShowWindowTalked(ToIndex, WinTalkIndex, WindowType, ButtonType, SeqNo, Data)

### 函数功能

生成并向目标对象发送一个对话框封包。

### 参数说明

- ToIndex: [数值型](../appendix/数值型.md) 接收对话框的目标对象index。
- WinTalkIndex: [数值型](../appendix/数值型.md) 生成对话框一方的对象index，一般是 NPC；该对象的对象index会作为对话框的“来源”下发给客户端。
- WindowType: [数值型](../appendix/数值型.md) 对话框类型编号。
- ButtonType: [数值型](../appendix/数值型.md) 对话框包含的按钮类型编号。
- SeqNo: [数值型](../appendix/数值型.md) 自定义序号，用于在后续的对话框回调里识别是哪一次 ShowWindowTalked 触发的响应。
- Data: [字符串](../appendix/字符串.md) 对话框内容，格式随 WindowType 不同而不同。

### 返回值

成功返回 0；ToIndex 或 WinTalkIndex 不是有效对象、或 Data 参数无法转换为字符串时返回 -1。

## 参考实例

```lua
NLG.ShowWindowTalked(Player, _MeIndex, 1, 0, 1, "欢迎光临，请选择：\\c继续\\c离开");
```

### 备注

本函数只负责下发窗口，不注册任何回调；玩家点击按钮/选择项后的响应通过 `Char.SetWindowTalkedEvent` 为 WinTalkIndex（一般是 NPC）登记的回调函数接收，回调签名为 CharWindowTalkedCallBack(CharIndex, TalkerCharIndex, SeqNo, Select, Data)，其中 SeqNo 与这里传入的值一一对应。
