<!-- Generated. DO NOT EDIT. -->
# GiveRecipe

## Char.GiveRecipe(CharIndex, RecipeId)

### 函数功能

为玩家增加指定 ID 的配方。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- RecipeId: [数值型](../appendix/数值型.md) 配方的 ID。

### 返回值

本次新学会返回 1；已经学会过、配方 ID 越界或不存在、对象不是玩家时返回 0。

## 参考实例

```lua
if Char.GiveRecipe(Player, 100) == 1 then
    NLG.TalkToCli(Player, -1, "学会了新配方。");
end
```

### 备注

只有“本次真的把标记从未拥有翻成拥有”才返回 1；重复给予同一个配方返回 0，
因此返回值可以直接当作“是不是第一次学会”来用。
成功时会把整份配方列表重新下发给客户端，并发一条系统消息。
