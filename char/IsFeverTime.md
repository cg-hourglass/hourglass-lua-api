<!-- Generated. DO NOT EDIT. -->
# IsFeverTime

## Char.IsFeverTime(CharIndex)

### 函数功能

检测玩家是否处于打卡（Fever）状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

在打卡状态返回 1，否则返回 0。

## 参考实例

```lua
if Char.IsFeverTime(Player) == 1 then
    NLG.TalkToCli(Player, -1, "打卡中。");
end
```

### 备注

本函数不做指针守卫：对象不是玩家或对象index无法解析时同样返回 0，
与“确实不在打卡”无法区分。
