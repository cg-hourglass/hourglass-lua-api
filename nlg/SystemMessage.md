<!-- Generated. DO NOT EDIT. -->
# SystemMessage

## NLG.SystemMessage(CharIndex, Message)

### 函数功能

给指定对象发送一条黄色加粗的系统公告消息。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 接收公告的对象index；传 -1 时发给当前所有在线玩家。
- Message: [字符串](../appendix/字符串.md) 要发送的公告文字。

### 返回值

成功发送给至少一个玩家时返回 1，否则返回 0（CharIndex 既不是有效玩家也不是 -1、或 -1 时服务器上没有在线玩家）。

## 参考实例

```lua
NLG.SystemMessage(-1, "服务器将在10分钟后维护。");
NLG.SystemMessage(player, "欢迎回来！");
```

### 备注

底层是 Char.SystemMsg，只对 CHAR_TYPEPLAYER 且当前有活动连线的对象生效；NPC/宠物/敌人对象index会被直接忽略并计入失败。
