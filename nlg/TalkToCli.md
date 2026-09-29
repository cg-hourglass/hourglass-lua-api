<!-- Generated. DO NOT EDIT. -->
# TalkToCli

## NLG.TalkToCli(ToIndex, TalkerIndex, Msg, FontColor, FontSize)

### 函数功能

让一名角色对指定对象（或全服）说话，走直接 TK 封包通道，不经过对话事件/连坐指令解析。

### 函数别名

- `NLG.Say(ToIndex, TalkerIndex, Msg, FontColor, FontSize)`

### 参数说明

- ToIndex: [数值型](../appendix/数值型.md) 说话目标的对象index；传 -1 时对全服在线玩家广播。
- TalkerIndex: [数值型](../appendix/数值型.md) 说话者的对象index，用于在消息前缀上显示名字；传 -1 时不带说话人前缀（旁白）。
- Msg: [字符串](../appendix/字符串.md) 说话内容。
- FontColor: [数值型](../appendix/数值型.md) 字体颜色，省略时为 0（白色）。 [可为空]
- FontSize: [数值型](../appendix/数值型.md) 字体大小，省略时为 0。 [可为空]

### 返回值

成功发送返回 0；目标不是有效玩家（或全服当前没有任何在线玩家）返回 -2；Msg 参数无法转换为字符串时返回 -1。

## 参考实例

```lua
NLG.TalkToCli(-1, _MeIndex, "This is from lua!!!", 4, 0); -- 对所有玩家以黄色字体说话
NLG.TalkToCli(_toIndex, _MeIndex, "Hello Lua!!!"); -- 对_toIndex玩家以默认白色字说话
```

### 备注

函数别名：`NLG.Say(...)`，参数与语义完全相同。
Say/Talk 系列的说话人前缀由引擎统一逻辑追加；如果说话人是玩家且当前处于“中毒/口齿不清”状态（SickLevel 命中概率），前缀会替换成随机的胡话而不是玩家名字，这是沿袭旧版的既有行为，不是bug。
FontColor 落在 MIC（+1000）或家族频道（+2000）色段时，服务器会把消息前缀替换成对应格式（如 [MIC]）并把颜色减去偏移量再发送，脚本一般不需要用到这两个特殊色段。
