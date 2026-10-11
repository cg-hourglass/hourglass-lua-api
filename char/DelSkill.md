<!-- Generated. DO NOT EDIT. -->
# DelSkill

## Char.DelSkill(CharIndex, SkillID)

### 函数功能

删除玩家的指定技能。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- SkillID: [数值型](../appendix/数值型.md) 技能 ID，对应 skill.txt 中的 id。

### 返回值

成功返回该技能原本所在的技能栏位置。
玩家没有这个技能、技能 ID 未登记、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
Char.DelSkill(Player, 1);
```

### 备注

清空后该栏位恢复成初始状态：技能 ID 为 -1、等级为 1、经验为 0，之后可以被 Char.AddSkill 复用。
