<!-- Generated. DO NOT EDIT. -->
# GetSkillExp

## Char.GetSkillExp(CharIndex, Slot)

### 函数功能

获取玩家指定技能栏位置上的技能经验。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 技能栏位置，可以先用 Char.HaveSkill 求出。

### 返回值

该位置技能的经验值；栏位越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 1);
local Exp = Char.GetSkillExp(Player, Slot);
```

### 备注

栏位上界取角色自身的技能栏上限。
本函数不判断该栏位上到底有没有技能，只有栏位越界才会返回 -1；
要先确认栏位有效，请配合 Char.GetSkillID 使用。被 Char.DelSkill 清空过的栏位经验会归 0。
