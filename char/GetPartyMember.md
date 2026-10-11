<!-- Generated. DO NOT EDIT. -->
# GetPartyMember

## Char.GetPartyMember(CharIndex, Slot)

### 函数功能

获取对象所在队伍中指定位置的成员。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 队伍中的位置，取值 0-4。

### 返回值

该位置成员的对象index；位置越界、该位置没有成员、成员已失效或对象类型不符时都返回 -1。

## 参考实例

```lua
for i = 0, Char.PartyNum(Player) - 1 do
    local Member = Char.GetPartyMember(Player, i);
    if Member ~= -1 then
        NLG.TalkToCli(Member, -1, "队伍公告。");
    end
end
```

### 备注

队伍上限本版本为 5，因此位置取值是 0-4；其它服务端上“支持 10vs10 时取值 0~9”的说法不适用于本服务端。
只有“对象类型既不是玩家也不是可组队 NPC”这一种失败会在服务端日志留下记录，
位置越界与成员失效都是静默的 -1。
