<!-- Generated. DO NOT EDIT. -->
# Talk

## NLG.Talk(TalkerIndex, Msg, FontColor, Area, FontSize)

### 函数功能

让指定角色通过完整对话管线说一句话——与玩家客户端发出的对话封包走同一入口，会经过对话事件、连坐指令（聊天魔法）等处理，而不是像 TalkToCli 那样直接下发 TK 封包。

### 参数说明

- TalkerIndex: [数值型](../appendix/数值型.md) 说话者的对象index。
- Msg: [字符串](../appendix/字符串.md) 说话内容；超过253字节（legacy编码）会被自动截断，截断点保证落在字符边界上。
- FontColor: [数值型](../appendix/数值型.md) 字体颜色，默认为0（白色）。 [可为空]
- Area: [数值型](../appendix/数值型.md) 说话范围参数，默认为0。 [可为空]
- FontSize: [数值型](../appendix/数值型.md) 字体大小，默认为0。 [可为空]

### 返回值

TalkerIndex有效返回 0；无效返回 -1。

## 参考实例

```lua
NLG.Talk(playerIndex, "/help", 0, 0, 0); -- 让玩家像自己在聊天框输入一样触发指令解析
```

### 备注

本函数实际只对玩家类型的 TalkerIndex 生效：TalkerIndex 是NPC/宠物/敌人时同样返回 0（看起来“成功”），但内部不会执行任何对话逻辑——完整对话管线本身要求说话者是玩家，这是沿袭旧版就有的限制，不是遗漏。
