<!-- Generated. DO NOT EDIT. -->
# PartyNum

## Char.PartyNum(CharIndex)

### 函数功能

获取对象所在队伍的成员人数。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

队伍人数；对象既不是玩家也不是可组队 NPC 时返回 -1；对象指针无效时也返回 -1。

## 参考实例

```lua
local Num = Char.PartyNum(Player);
if Num > 1 then
    NLG.TalkToCli(Player, -1, "请先解散队伍。");
end
```

### 备注

没有组队的玩家返回的是 1（队伍里只有自己），不是 -1；
-1 只出现在对象指针无效或对象类型既不是玩家也不是可组队 NPC 的情况下。
类型不符时还会在服务端日志留下一条记录。
