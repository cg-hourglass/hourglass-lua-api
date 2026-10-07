<!-- Generated. DO NOT EDIT. -->
# GetSkillID

## Char.GetSkillID(CharIndex, Slot)

### 函数功能

获取玩家指定技能栏位置上的技能 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 技能栏位置，不能超过角色自身的技能栏数量。

### 返回值

该位置上的技能 ID；空栏位、栏位越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
for i = 0, 14 do
    local SkillID = Char.GetSkillID(Player, i);
    if SkillID ~= -1 then
        -- 该栏位有技能
    end
end
```

### 备注

栏位上界取角色自身的技能栏上限，不是固定的 15。
