<!-- Generated. DO NOT EDIT. -->
# ActionSelect

## Battle.ActionSelect(CharIndex, Com1, Com2, Com3)

### 函数功能

让对象执行一次指定的战斗指令，必须在 Battle.IsWaitingCommand 返回 1 时调用才有效。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index，可以是玩家或宠物。
- Com1: [数值型](../appendix/数值型.md) 战斗指令，见下方指令说明。
- Com2: [数值型](../appendix/数值型.md) 指令的目标位置；对自身或无需目标时填 -1。
- Com3: [数值型](../appendix/数值型.md) 指令的附加参数；普通指令填 -1，施放战斗技能时填对应技能在 tech.txt 中的 tech id。

### 返回值

1 成功下达指令，0 失败。

## 参考实例

```lua
if Battle.IsWaitingCommand(index) == 1 then
    Battle.ActionSelect(index, %战斗指令_攻击%, 11, -1);
    print("offline player attack");
end

if Battle.IsWaitingCommand(index) == 1 then
    Battle.ActionSelect(index, %TECH_Assassin%, 11, 9609); -- 施放 10 级暗杀
    print("施放10级暗杀");
end
```

### 备注

Com1 可用的指令常量：

- %战斗指令_无%（0）什么也不做
- %战斗指令_防御%（1）防御
- %战斗指令_位置%（2）切换位置
- %战斗指令_装备%（3）更换装备
- %战斗指令_攻击%（4）攻击
- %战斗指令_逃跑%（6）逃跑
- %战斗指令_宠物出场%（7）宠物出场
- %战斗指令_宠物收回%（8）宠物收回
- %战斗指令_道具%（9）使用道具
- %战斗指令_精灵变身%（3000）精灵变身
- 战斗技能参数，如 %TECH_SpiracleShot% 表示施放乱射，所有战斗可用技能的常量都可以使用

Com2 的目标位置可以用 Battle.GetEntryPosition 或 Battle.GetTargetSelect 计算得到。

对象是玩家时走玩家指令通道，是宠物时走宠物指令通道；两者都要求对象的战斗状态是
%战斗状态_命令等待%，否则直接返回 0。对象类型既不是玩家也不是宠物（例如敌人）时始终返回 0。
