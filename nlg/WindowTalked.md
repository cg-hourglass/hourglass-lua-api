<!-- Generated. DO NOT EDIT. -->
# WindowTalked

## NLG.WindowTalked(Type, CharIndex, TargetCharIndex, SeqNo, Select, Data)

### 函数功能

Talked 的窗口交互半区，配合内置银行/窗口治疗师/伤病医生对话框的按钮响应使用。

### 参数说明

- Type: [数值型](../appendix/数值型.md) 内置模板编号，0=银行、1=窗口治疗师、2=伤病医生。
- CharIndex: [数值型](../appendix/数值型.md) 自身对象index，多数情况下是 NPC。
- TargetCharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。
- SeqNo: [数值型](../appendix/数值型.md) 来源对话框的序号。
- Select: [数值型](../appendix/数值型.md) 玩家按下的按钮值或选中项的值。
- Data: [字符串](../appendix/字符串.md) 客户端回传的数据。

### 返回值

固定返回 1，不携带成功/失败信息。

## 参考实例

```lua
NLG.WindowTalked(0, _MeIndex, playerIndex, 339, 0, "");
```

### 备注

本函数固定返回 1，不是“0表示成功，其他表示失败”。
Type=0（银行）只在 SeqNo==339 且 Select==0 时才真正触发处理，其余组合直接忽略；TargetCharIndex 必须是玩家类型，否则整个调用直接跳过（仍返回1）。
