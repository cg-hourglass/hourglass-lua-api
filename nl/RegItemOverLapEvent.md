<!-- Generated. DO NOT EDIT. -->
# RegItemOverLapEvent

## NL.RegItemOverLapEvent(Dofile, FuncName)

### 函数功能

注册道具栏内把一个道具拖到另一个道具上时触发的 Lua 函数，可以拦截这次移动。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## ItemOverLapEventCallBack(CharIndex, FromItemIndex, TargetItemIndex, Num)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 操作道具的玩家对象index，由引擎传入。
- FromItemIndex: [数值型](../appendix/数值型.md) 被拖动的道具对象index，由引擎传入。
- TargetItemIndex: [数值型](../appendix/数值型.md) 被覆盖的目标道具对象index，由引擎传入。
- Num: [数值型](../appendix/数值型.md) 被拖动的道具数量，由引擎传入。

### 返回值

返回非0表示脚本已自行处理，服务器中止本次移动；返回0让服务器继续执行默认的移动逻辑。未注册、解析失败或调用出错时默认返回 0（放行）。

## 参考实例

```lua
NL.RegItemOverLapEvent(nil, "MyItemOverLapEvent");

function MyItemOverLapEvent(CharIndex, FromItemIndex, TargetItemIndex, Num)
  if(TargetItemIndex == -1)then
    return 0; -- 目标栏位为空，交给服务器自己处理
  end
  return 1; -- 已经自行处理，阻止服务器移动道具
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
两个触发点：客户端的移动道具封包，以及 NLG.MoveItem——后者是同步触发，在回调里再调用 NLG.MoveItem 会递归，引擎没有任何保护。
