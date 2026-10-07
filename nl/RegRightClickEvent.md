<!-- Generated. DO NOT EDIT. -->
# RegRightClickEvent

## NL.RegRightClickEvent(Dofile, FuncName)

### 函数功能

注册玩家右键点击另一名玩家时触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## RightClickCallBack(CharIndex, TargetCharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 发起右键点击的玩家对象index，由引擎传入。
- TargetCharIndex: [数值型](../appendix/数值型.md) 被右键点击的玩家对象index，由引擎传入。

### 返回值

返回0即可。引擎以 0 个返回值调用本函数，返回什么都不会被读取，无法用来拦截。

## 参考实例

```lua
NL.RegRightClickEvent(nil, "MyRightClickEvent");

function MyRightClickEvent(CharIndex, TargetCharIndex)
  NLG.SystemMessage(TargetCharIndex, CharIndex.." 刚才戳了你一下");
  return 0;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
被点击的目标必须是玩家。本事件纯通知，回调的返回值不会被读取，不能用于拦截。
