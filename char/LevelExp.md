<!-- Generated. DO NOT EDIT. -->
# LevelExp

## Char.LevelExp(CharIndex)

### 函数功能

获取对象当前等级对应的累计经验门槛。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

达到当前等级所需的累计经验值；对象指针无效、等级非法或超出经验表范围时返回 -1。

## 参考实例

```lua
local Need = Char.LevelExp(Player);
local Next = Char.LevelExpAt(Player, Char.GetData(Player, %对象_等级%) + 1);
NLG.TalkToCli(Player, -1, "升级还差 " .. (Next - Char.GetData(Player, %对象_经验%)) .. " 点经验。");
```

### 备注

返回的是「达到当前等级所需的累计经验」，不是「升到下一级所需的经验」；C 版里对应函数的名字 getNextLevelExp 容易误导。下一级的门槛要用 `Char.LevelExpAt(CharIndex, 当前等级 + 1)` 取。
这个值会经过 NL.RegGetNextLevelExpEvent 登记的事件加工，脚本可以在那里改写它，因此返回值不一定等于经验表里的原始数字。
对象指针无效时会在服务端日志留下一条记录。
