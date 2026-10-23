<!-- Generated. DO NOT EDIT. -->
# GetSkillNextExp

## Char.GetSkillNextExp(CharIndex, Slot)

### 函数功能

只读获取玩家技能升级所需的累计经验阈值。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index，支持玩家和伙伴。
- Slot: [数值型](../appendix/数值型.md) 从 0 开始的技能栏位置，可以先用 Char.HaveSkill 求出；不是技能ID。

### 返回值

升到下一级所需的累计经验阈值；对象无效、不是玩家、栏位越界、技能未学习或经验表缺失时返回 -1。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 61);
if Slot >= 0 then
  local Exp = Char.GetSkillExp(Player, Slot);
  local NextExp = Char.GetSkillNextExp(Player, Slot);
end
```

### 备注

本函数只读，不会增加经验、升级技能或写入存档。
返回值是累计经验阈值，不是还需获得的经验；当前经验请使用 Char.GetSkillExp。
达到全局技能等级上限时返回 99999999，与原生技能界面一致；职业技能上限不会改变此规则。
0 是有效阈值；-1 表示未知或无效，不能当作 0 使用。
