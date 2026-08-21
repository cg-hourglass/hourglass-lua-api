<!-- Generated. DO NOT EDIT. -->
# GetGuildTitleID

## Char.GetGuildTitleID(CharIndex)

### 函数功能

获取玩家在家族中的称号 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

家族称号 ID；没有家族、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local GuildTitle = Char.GetGuildTitleID(Player);
```

### 备注

这是家族内部的职位称号，与 Char.GetTitle 读的角色称号是两套不同的编号。
