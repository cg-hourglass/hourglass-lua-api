<!-- Generated. DO NOT EDIT. -->
# RegMakeItemStringEvent

## NL.RegMakeItemStringEvent(Dofile, FuncName)

### 函数功能

注册生成道具介绍文字时触发的 Lua 函数，可以改写道具说明文本。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## MakeItemStringCallBack(CharIndex, ItemSlot, ItemIndex, ItemText, TextLen, TextMaxLen)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 查看道具的玩家对象index，由引擎传入。
- ItemSlot: [数值型](../appendix/数值型.md) 该道具在玩家身上的栏位号，由引擎传入。
- ItemIndex: [数值型](../appendix/数值型.md) 道具的对象index，由引擎传入。
- ItemText: [字符串](../appendix/字符串.md) 服务器已经拼好的道具属性介绍文字，由引擎传入。
- TextLen: [数值型](../appendix/数值型.md) ItemText 的长度（按脚本编码的字节数计），由引擎传入。
- TextMaxLen: [数值型](../appendix/数值型.md) 介绍文字缓冲区的最大长度，当前为 1024。由引擎传入。

### 返回值

返回新的介绍文字（字符串），引擎会用它覆盖原缓冲区；返回数值也会被当成字符串写回。返回其它类型则保持原文不变。

## 参考实例

```lua
NL.RegMakeItemStringEvent(nil, "MyMakeItemStringEvent");

function MyMakeItemStringEvent(CharIndex, ItemSlot, ItemIndex, ItemText, TextLen, TextMaxLen)
  return ItemText.."|这是脚本追加的说明";
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
TextLen 与 TextMaxLen 都按脚本编码（GBK 或 BIG5）的字节数计量，脚本按这两个数字给自己的改写留预算。
返回的文字会被截断到 TextMaxLen-1 字节；本服务端的截断落在完整字符边界上，
不会像旧版那样按字节硬切出半个汉字、导致整个道具封包编码失败。
只有玩家查看自己身上的道具时才会触发；商店列表等没有角色上下文的调用不会进入本回调。
