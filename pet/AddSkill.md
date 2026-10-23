<!-- Generated. DO NOT EDIT. -->
# AddSkill

## Pet.AddSkill(PetIndex, SkillID)

### 函数功能

给宠物增加一个新技能，宠物技能栏未满时生效。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index；敌人对象同样适用。
- SkillID: [数值型](../appendix/数值型.md) 技能 ID，即 tech.txt 中定义的 ID。

### 返回值

成功增加返回 1，技能栏已满或对象既不是宠物也不是敌人返回 0。

## 参考实例

```lua
Pet.AddSkill(_pet, 7300); -- 让宠物 _pet 学会指定技能
```

### 备注

技能写入宠物技能窗口内第一个空槽（槽内值为 -1 的位置）。技能窗口的大小取自宠物自身的
技能栏数量，与宠物成长有关，并非固定 10 格。
