<!-- Generated. DO NOT EDIT. -->
# HasGuild

## Char.HasGuild(CharIndex)

### 函数功能

检测对象是否已经加入家族。

### 函数别名

- `Char.HaveGuild(CharIndex)`

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

已加入返回 1，未加入返回 0；对象不是玩家或指针无效时同样返回 0。

## 参考实例

```lua
if Char.HasGuild(Player) == 0 then
    NLG.TalkToCli(Player, -1, "你还没有加入家族。");
end
```

### 备注

没有家族时返回的是 0 而不是 -1，请不要与 -1 比较。
别名 Char.HaveGuild 与本函数是同一个实现。
判断依据是家族 ID 不等于 -1，等价于 `Char.GetGuildID(CharIndex) ~= -1`。
