<!-- Generated. DO NOT EDIT. -->
# TalkToFloor

## NLG.TalkToFloor(Map, Floor, TalkerIndex, Msg, FontColor, FontSize)

### 函数功能

让一名角色对指定地图+楼层上的所有在线玩家说话，走直接 TK 封包通道。

### 函数别名

- `NLG.TalkToMap(Map, Floor, TalkerIndex, Msg, FontColor, FontSize)`
- `NLG.Say2Map(Map, Floor, TalkerIndex, Msg, FontColor, FontSize)`

### 参数说明

- Map: [数值型](../appendix/数值型.md) 说话目标的地图类型，0为固定地图，1为随机地图。
- Floor: [数值型](../appendix/数值型.md) 说话目标的地图编号。
- TalkerIndex: [数值型](../appendix/数值型.md) 说话者的对象index，用于在消息前缀上显示名字；传 -1 时不带说话人前缀（旁白）。
- Msg: [字符串](../appendix/字符串.md) 说话内容。
- FontColor: [数值型](../appendix/数值型.md) 字体颜色，省略时为 0（白色）。 [可为空]
- FontSize: [数值型](../appendix/数值型.md) 该参数被引擎接受但直接忽略，实际发送时字体大小固定为 0（默认大小）。 [可为空]

### 返回值

该地图楼层上至少有一名玩家收到消息时返回 0；TalkerIndex 给了但不是有效角色、或 Msg 参数无法转换为字符串时返回 -1；地图楼层上没有玩家收到时返回 -2。

## 参考实例

```lua
NLG.TalkToFloor(0, 1000, _MeIndex, "This is from lua!!!", 4, 0); -- 对所有在法兰城的玩家说话
NLG.TalkToFloor(0, 1000, -1, "This is from lua!!!", 4, 0); -- 不带说话人名字
```

### 备注

函数别名：`NLG.TalkToMap(...)`、`NLG.Say2Map(...)`，参数与语义完全相同。
与 TalkToCli 不同：这里的第 6 个参数（FontSize）虽然被参数个数检查接受，但实现里从未读取它，实际发送时永远使用默认字体大小（数值 0）——传了非 0 的 FontSize 也不会生效，这是本版本的既有行为，不是遗漏。
