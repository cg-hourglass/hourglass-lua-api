<!-- Generated. DO NOT EDIT. -->
# UseTech

## Battle.UseTech(CharIndex, SkillSlot, TechSlot, Target)

### 函数功能

让对象按技能栏位置施放战斗技能，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index。
- SkillSlot: [数值型](../appendix/数值型.md) 技能所在的技能栏位置。
- TechSlot: [数值型](../appendix/数值型.md) 该技能下指定等级的技能所在位置。
- Target: [数值型](../appendix/数值型.md) 施法目标在战场中的位置，有效范围 0-19，超出范围会被当作 -1（不指定目标）。

### 返回值

1 技能成功发出，0 失败。

## 参考实例

```lua
if Battle.IsWaitingCommand(index) == 1 then
    Battle.UseTech(index, 0, 0, 11);
    print("offline player use tech");
end
```

### 备注

与 Battle.UseTechById 相比，本函数多了三重检查：技能栏解析出的技能必须属于战斗系
（战斗技能、骑乘技能或战斗魔法）；技能的装备需求掩码必须与当前武器类型匹配；
在开启相关配置的 BOSS 战中禁止跳舞技能。

目标位置的改写规则与 Battle.UseTechById 相同（单体不变／范围 +20／单列 40、41／全体 42）。

技能不属于战斗系但其余检查都通过时，本函数直接返回 0，**不会**替对象下达放弃指令；
只有在技能检查失败时才会下达一次 %战斗指令_无%。
