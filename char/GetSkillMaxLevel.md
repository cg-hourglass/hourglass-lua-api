<!-- Generated. DO NOT EDIT. -->
# GetSkillMaxLevel

## Char.GetSkillMaxLevel(CharIndex, Slot)

### 函数功能

获取玩家指定技能栏位置上的技能在当前职业下的等级上限。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 技能栏位置，可以先用 Char.HaveSkill 求出。

### 返回值

该技能在当前职业下的最高可用等级；任何失败都返回 0。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 1);
local Max = Char.GetSkillMaxLevel(Player, Slot);
```

### 备注

失败返回的是 0 而不是 -1。对象不是玩家、指针无效、栏位越界、栏位为空、
技能未登记这几种情况全部折叠成同一个 0，与“上限本来就是 0”无法区分。
上限随职业变化，同一个技能换职业后读到的值可能不同。
