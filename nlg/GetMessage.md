<!-- Generated. DO NOT EDIT. -->
# GetMessage

## NLG.GetMessage(MessageId)

### 函数功能

按ID读取旧版 msg.txt 消息表里的一条文字（不是 langmsg 多语言目录）。

### 参数说明

- MessageId: [数值型](../appendix/数值型.md) 消息ID。

### 返回值

对应的消息文字；ID不存在时返回空字符串。

## 参考实例

```lua
local text = NLG.GetMessage(100);
```
