<!-- Generated. DO NOT EDIT. -->
# LevelExp

## Char.LevelExp(CharIndex)

### 函数功能

获取对象当前等级对应的升级经验门槛。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

该等级对应的经验值；等级非法或超出经验表范围时返回 -1；对象指针无效时返回 -1。

## 参考实例

```lua
local Need = Char.LevelExp(Player);
NLG.TalkToCli(Player, -1, "升级需要 " .. Need .. " 点经验。");
```

### 备注

取的是“当前等级对应的经验门槛”，具体含义取决于服务端使用的经验表是
“达到本级所需累计经验”还是“升到下一级所需经验”。
这个值还会经过 NL.RegGetNextLevelExpEvent 登记的事件加工，
脚本可以在那里改写它，因此本函数的返回值不一定等于经验表里的原始数字。
对象指针无效时会在服务端日志留下一条记录。
