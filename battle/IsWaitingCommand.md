<!-- Generated. DO NOT EDIT. -->
# IsWaitingCommand

## Battle.IsWaitingCommand(CharIndex)

### 函数功能

判断对象是否正处于战斗中的等待输入指令状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index，可以是玩家、宠物或敌人。

### 返回值

1 表示正在等待指令，0 表示不是；对象无效或战斗index非法返回 -1。

## 参考实例

```lua
if Battle.IsWaitingCommand(TM_CharIndex) == 1 then
    Battle.ActionSelect(TM_CharIndex, %战斗指令_攻击%, 11, -1);
end
```

### 备注

基础条件是对象的战斗状态为 %战斗状态_命令等待%。若服务器开启了加速外挂检测，还额外
要求当前时间已经到达本回合允许行动的时刻，否则同样返回 0。
因此在开启该项检测的服务器上，本函数会在回合刚开始的一小段时间内返回 0，脚本应循环
重试而不要只判断一次。
