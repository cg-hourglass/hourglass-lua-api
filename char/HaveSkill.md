<!-- Generated. DO NOT EDIT. -->
# HaveSkill

## Char.HaveSkill(CharIndex, SkillID)

### 函数功能

获取玩家指定技能所在的技能栏位置。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- SkillID: [数值型](../appendix/数值型.md) 技能 ID，对应 skill.txt 中的 id。

### 返回值

技能所在的技能栏位置；玩家没有该技能、技能 ID 未登记、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 1);
if Slot ~= -1 then
    Char.GetSkillLevel(Player, Slot);
end
```

### 备注

技能表里查不到的 ID 会在扫描开始之前就返回 -1。
