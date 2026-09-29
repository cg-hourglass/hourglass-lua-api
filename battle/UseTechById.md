<!-- Generated. DO NOT EDIT. -->
# UseTechById

## Battle.UseTechById(CharIndex, TechId, Target)

### 函数功能

让对象直接按 tech id 施放战斗技能，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index。
- TechId: [数值型](../appendix/数值型.md) 技能 ID，即 gmsv 的 tech.txt 中定义的 tech id。
- Target: [数值型](../appendix/数值型.md) 施法目标在战场中的位置。

### 返回值

1 技能成功发出，0 失败。

## 参考实例

```lua
if Battle.IsWaitingCommand(index) == 1 then
    Battle.UseTechById(index, 9609, 11); -- 直接按 tech id 施放
end
```

### 备注

与 Battle.UseTech 不同，本函数不做技能栏解析，也不检查武器装备类型，只检查技能等级需求、
目标范围合法性和加速检测的时间闸门。

目标位置会按技能的目标类型自动改写：单体技能保持原值；范围技能加 20；单列技能改写为
40（下方）或 41（上方）；全体技能改写为 42。改写后如果落在该技能允许的区间之外，
本次施放判定失败。

失败时并不是什么都不做：只要时间闸门已经放行，引擎会替对象下达一次
%战斗指令_无%（相当于放弃本回合），然后返回 0。
