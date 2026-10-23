<!-- Generated. DO NOT EDIT. -->
# AddSkill

## Char.AddSkill(CharIndex, SkillID, SkillExp)

### 函数功能

为玩家增加指定技能，可同时播种初始经验。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- SkillID: [数值型](../appendix/数值型.md) 技能 ID，对应 skill.txt 中的 id。
- SkillExp: [数值型](../appendix/数值型.md) 技能的初始经验值，省略时为 0。 [可为空]

### 返回值

成功返回新占用的技能栏位置（从 0 开始）。
技能 ID 不存在、剩余技能槽位不足、没有空栏位、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
Char.AddSkill(Player, 1);
Char.AddSkill(Player, 1, 1000);   -- 带 1000 点初始经验
```

### 备注

占位检查按技能表里登记的占位需求计算：剩余槽位预算不够时直接返回 -1，不会挤掉已有技能。
SkillExp 大于 0 时经验会走正式的技能经验写入流程，可能连带把技能等级顶上去。
