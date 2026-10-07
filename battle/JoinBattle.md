<!-- Generated. DO NOT EDIT. -->
# JoinBattle

## Battle.JoinBattle(CharIndex1, CharIndex2)

### 函数功能

让一个不在战斗中的玩家加入另一个玩家的战斗（战斗中途救援参战）。

### 参数说明

- CharIndex1: [数值型](../appendix/数值型.md) 已经在战斗中的玩家对象index。
- CharIndex2: [数值型](../appendix/数值型.md) 不在战斗中的玩家对象index，即被拉进战斗的一方。

### 返回值

1 成功；0 战斗引擎拒绝参战；-1 对象index无效，或双方的战斗状态不满足要求。

## 参考实例

```lua
if Battle.JoinBattle(TM_Fighter, TM_Helper) == 1 then
    print("救援参战成功");
end
```

### 备注

前置条件：CharIndex1 的战斗状态必须不是 %战斗状态_无%，CharIndex2 的战斗状态必须是 %战斗状态_无%。

**1 为成功**，不是“0 为成功”，判断请勿写反。
