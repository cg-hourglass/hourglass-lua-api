<!-- Generated. DO NOT EDIT. -->
# CheckTalkRange

## NLG.CheckTalkRange(CharIndex, TargetCharIndex)

### 函数功能

检查两个对象是否处于可对话的位置关系（大致等价于“面对面且相距不超过2格”）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 自身对象index。
- TargetCharIndex: [数值型](../appendix/数值型.md) 目标对象index。

### 返回值

可以交谈返回 1，不可以返回 0。

## 参考实例

```lua
if NLG.CheckTalkRange(_MeIndex, playerIndex) == 1 then
  NLG.ShowTalked(playerIndex, _MeIndex);
end
```

### 备注

精确规则：当双方互相朝向对方（面对面判定，检测半径2格）时，只有在两者实际距离超过2格才判为不可对话；如果不满足互相面对面，则只有当 TargetCharIndex 正朝向 CharIndex、且间隔1格时才判为可对话，其余情况都不可对话。两个对象不在同一地图楼层或坐标重合时同样判为不可对话。
