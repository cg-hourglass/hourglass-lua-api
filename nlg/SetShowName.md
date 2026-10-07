<!-- Generated. DO NOT EDIT. -->
# SetShowName

## NLG.SetShowName(CharIndex, ONOFF)

### 函数功能

设置 NPC/宠物/敌人对象是否像玩家一样在头顶显示名字。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index；必须不是玩家类型。
- ONOFF: [数值型](../appendix/数值型.md) 0（关闭）或1（开启）。

### 返回值

成功时返回刚设置的当前状态（0或1）；目标是玩家或无效对象时返回 -1。

## 参考实例

```lua
NLG.SetShowName(_MeIndex, 1);
```

### 备注

玩家对象一律被拒绝（不能通过本函数更改玩家的名字显示）。成功后会向周围重新广播一次该对象数据，并发送一次“待机”动作观察事件。
