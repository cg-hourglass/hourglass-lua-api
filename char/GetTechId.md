<!-- Generated. DO NOT EDIT. -->
# GetTechId

## Char.GetTechId(CharIndex, SkillIndex, TechIndex)

### 函数功能

获取对象某个技能栏位置下指定招式位置的招式 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- SkillIndex: [数值型](../appendix/数值型.md) 技能栏位置；对宠物而言是宠物技能的位置，必须小于 10。
- TechIndex: [数值型](../appendix/数值型.md) 招式位置，取值 0-14；对宠物无效，会被忽略。

### 返回值

对应的招式 ID；对象类型不支持、下标越界或该位置没有招式时返回 -1。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 1);
local TechId = Char.GetTechId(Player, Slot, 0);
```

### 备注

玩家读的是技能栏 SkillIndex 下第 TechIndex 个招式；宠物读的是第 SkillIndex 个宠物技能，
要求 SkillIndex 小于 10，此时 TechIndex 被忽略。玩家与宠物以外的对象类型一律返回 -1。
TechIndex 的合法范围本版本是 0-14。
所有失败分支在本服务端都稳定返回 -1；旧版有几条分支不压返回值，脚本会读到未定义的残留值。
