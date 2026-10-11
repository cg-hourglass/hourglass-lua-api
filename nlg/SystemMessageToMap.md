<!-- Generated. DO NOT EDIT. -->
# SystemMessageToMap

## NLG.SystemMessageToMap(MapID, FloorID, Message)

### 函数功能

给指定地图上的所有在线玩家发送一条黄色加粗的系统公告消息。

### 参数说明

- MapID: [数值型](../appendix/数值型.md) 目标地图类型，0为固定地图，1为随机地图。
- FloorID: [数值型](../appendix/数值型.md) 地图编号。
- Message: [字符串](../appendix/字符串.md) 要发送的公告文字。

### 返回值

该地图上至少有一名玩家收到消息时返回 1，否则返回 0。

## 参考实例

```lua
NLG.SystemMessageToMap(0, 1000, "法兰城即将举办活动！");
```
