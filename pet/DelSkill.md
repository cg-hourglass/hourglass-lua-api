<!-- Generated. DO NOT EDIT. -->
# DelSkill

## Pet.DelSkill(PetIndex, SkillSlot)

### 函数功能

删除宠物指定位置上的技能。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- SkillSlot: [数值型](../appendix/数值型.md) 技能槽位置，从 0 开始计算。

### 返回值

对象是宠物或敌人时返回 1，否则返回 0。

## 参考实例

```lua
Pet.DelSkill(_pet, 0); -- 让宠物 _pet 忘记第一个技能
```

### 备注

返回 1 **不代表真的删掉了技能**：只要对象是宠物或敌人就返回 1，而 SkillSlot 超出宠物
技能窗口（含负数）时会跳过写入，不产生任何效果。
