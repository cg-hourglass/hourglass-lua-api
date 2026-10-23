<!-- Generated. DO NOT EDIT. -->
# GetGuildID

## Char.GetGuildID(CharIndex)

### 函数功能

获取玩家所属家族的 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

家族 ID；没有家族时返回 -1；对象不是玩家或指针无效时也返回 -1。

## 参考实例

```lua
local GuildID = Char.GetGuildID(Player);
if GuildID == -1 then
    NLG.TalkToCli(Player, -1, "你还没有加入家族。");
end
```

### 备注

“没有家族”和“对象无效”都是 -1，无法区分；需要先确认对象类型时请配合 Char.HasGuild 使用。
