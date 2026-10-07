<!-- Generated. DO NOT EDIT. -->
# SetHeadIcon

## NLG.SetHeadIcon(CharIndex, IconNo)

### 函数功能

设置对象头顶显示的状态图标（如采集、生产等技能进行中的提示）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- IconNo: [数值型](../appendix/数值型.md) 图标编号，具体范围随客户端版本而定，常见范围大致是0-15。

### 返回值

成功返回 0，目标无效返回 -1。

## 参考实例

```lua
NLG.SetHeadIcon(_MeIndex, 3);
```

### 备注

底层与设置技能使用中图标是同一套逻辑：既广播一次动作事件（附带图标编号作为选项），也把编号写进对象的内部技能状态字段。
