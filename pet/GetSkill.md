<!-- Generated. DO NOT EDIT. -->
# GetSkill

## Pet.GetSkill(PetIndex, SkillSlot)

### 函数功能

获取宠物指定位置上的技能 ID。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- SkillSlot: [数值型](../appendix/数值型.md) 技能槽位置，从 0 开始计算。

### 返回值

成功返回技能 ID；槽位为空、超出技能窗口，或对象既不是宠物也不是敌人时返回 -1。

## 参考实例

```lua
local TM_Skill = Pet.GetSkill(_pet, 0); -- 获取宠物 _pet 第一个技能的 ID
if TM_Skill ~= -1 then
    print("skill = " .. TM_Skill);
end
```
