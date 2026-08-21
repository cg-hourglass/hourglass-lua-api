<!-- Generated. DO NOT EDIT. -->
# JoinParty

## Char.JoinParty(CharIndex, TargetCharIndex)

### 函数功能

让对象加入指定目标所在的队伍。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- TargetCharIndex: [数值型](../appendix/数值型.md) 要加入的队伍中某位队员或队长的对象index。

### 返回值

固定返回 0，不反映成功与否。

## 参考实例

```lua
Char.JoinParty(Player, LeaderIndex);
```

### 备注

所有分支都返回 0，包括守卫失败的那一支——返回值完全不携带信息。
要确认是否真的入队，请随后用 Char.GetPartyMode 或 Char.PartyNum 复查。
玩家与玩家之间走常规的组队流程；在开启随行 NPC 组队的版本上，
类型为可组队 NPC 且组队标记为 1 的 NPC 也可以作为任意一方参与组队。
