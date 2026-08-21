<!-- Generated. DO NOT EDIT. -->
# PetActionSelect

## Battle.PetActionSelect(CharIndex, SkillSlot, Target)

### 函数功能

让玩家的出战宠物执行一次战斗指令，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index。指令实际发送给该玩家的当前出战宠物。
- SkillSlot: [数值型](../appendix/数值型.md) 宠物技能所在的技能栏位置，从 0 开始。
- Target: [数值型](../appendix/数值型.md) 目标在战场中的位置；填 -1 或 255 表示不指定目标（宠物待命／放弃本回合）。

### 返回值

1 表示宠物成功施放了技能，0 表示未施放技能（包括改为下达空指令的情况）。

## 参考实例

```lua
if Battle.IsWaitingCommand(index) == 1 then
    Battle.PetActionSelect(index, 0, 11); -- 出战宠物用第一个技能攻击 11 号位
end
```

### 备注

第一个参数必须是玩家；角色没有出战宠物（DefaultPet 为空或宠物不可用）时直接返回 0。

以下情况会退化为给宠物下达 %战斗指令_无%，返回 0：Target 为 -1 或 255；技能栏位置上没有技能；
宠物的 FP 不足以支付该技能的战斗消耗；目标位置经技能目标类型改写后越界；技能实际施放失败。
