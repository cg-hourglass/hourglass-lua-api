<!-- Generated. DO NOT EDIT. -->
# SetSkillLevel

## Char.SetSkillLevel(CharIndex, Slot, Level)

### 函数功能

设置玩家指定技能栏位置上的技能等级。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 技能栏位置，可以先用 Char.HaveSkill 求出。
- Level: [数值型](../appendix/数值型.md) 新的技能等级。

### 返回值

写入成功返回 1，写入被拒绝返回 0；栏位越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Slot = Char.HaveSkill(Player, 1);
Char.SetSkillLevel(Player, Slot, 10);
```

### 备注

返回的不是“新的等级”，而是这次设置的布尔结果（1 或 0）。
写入后会重算派生招式并向客户端重发技能数据。
