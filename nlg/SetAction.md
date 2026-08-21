<!-- Generated. DO NOT EDIT. -->
# SetAction

## NLG.SetAction(CharIndex, Action)

### 函数功能

设置对象当前的动作状态并向周围广播。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- Action: [数值型](../appendix/数值型.md) 动作编号，具体取值参考客户端动作定义。

### 返回值

成功返回 0；目标无效返回 -1。

## 参考实例

```lua
NLG.SetAction(_MeIndex, 11); -- 设置为坐下动作
```

### 备注

广播在写入 w.Action 之前发生：客户端先收到“动作变化”事件通知，服务端才把状态落到对象数据上，与原版顺序一致。
