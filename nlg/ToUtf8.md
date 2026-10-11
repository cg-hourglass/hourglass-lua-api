<!-- Generated. DO NOT EDIT. -->
# ToUtf8

## NLG.ToUtf8(Text)

### 函数功能

把服务端运行时编码（Big5 或 GBK）的字符串转换成 UTF-8，是 NLG.FromUtf8 的逆操作。

### 参数说明

- Text: [字符串](../appendix/字符串.md) 运行时编码的字符串，例如玩家输入或其它接口返回的文本。

### 返回值

UTF-8 字符串；Text 不是字符串或含有运行时编码无法解码的字节时返回 nil。

## 参考实例

```lua
local name = NLG.ToUtf8(Char.GetData(player, %对象_名字%));
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
纯 ASCII 文本原样返回。
