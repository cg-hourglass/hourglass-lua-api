<!-- Generated. DO NOT EDIT. -->
# CanTalk

## NLG.CanTalk(CharIndex, TargetCharIndex)

### 函数功能

判断玩家当前是否可以与目标 NPC 交谈（在 CheckTalkRange 的几何判定基础上，额外拒绝不可见/停用的 NPC）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 被交谈一方的对象index（通常是 NPC）；若其外观图形编号为 0（不可见/已停用），无论几何关系如何都判为不可交谈。
- TargetCharIndex: [数值型](../appendix/数值型.md) 发起交谈一方的对象index（通常是玩家）。

### 返回值

是（Lua 布尔值 true）或否（false）。

## 参考实例

```lua
if NLG.CanTalk(_MeIndex, playerIndex) then
  NLG.ShowTalked(playerIndex, _MeIndex);
end
```

### 备注

本函数返回的是 Lua 布尔值，不是 1/0 数值——判断请用 `== true`/`if ... then`，不要与数值 1 比较。
几何判定规则与 CheckTalkRange 相同（互相面对面且距离不超过2格，或对方朝向自己且间隔1格），额外叠加外观图形编号的可见性检查。
两个对象参数的指针检查失败时会额外写一条日志，不影响返回值。
