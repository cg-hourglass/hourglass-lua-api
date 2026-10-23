<!-- Generated. DO NOT EDIT. -->
# GetPartyMode

## Char.GetPartyMode(CharIndex)

### 函数功能

获取对象当前的组队状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

0 没有组队，1 队长，2 队员，3 宠物跟随；对象指针无效时返回 -1。

## 参考实例

```lua
if Char.GetPartyMode(Player) == 1 then
    NLG.TalkToCli(Player, -1, "你是队长。");
end
```

### 备注

直接读 work 区的 PartyMode 字段，不限制对象类型，宠物与 NPC 也能读。
对象指针无效时会在服务端日志留下一条记录。
