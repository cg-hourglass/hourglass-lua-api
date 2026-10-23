<!-- Generated. DO NOT EDIT. -->
# RegLoginGateEvent

## NL.RegLoginGateEvent(Dofile, FuncName)

### 函数功能

注册玩家点击客户端“登出回记录点”时触发的 Lua 函数，可以拦截该操作。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## LoginGateEventCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 发起登出的玩家对象index，由引擎传入。

### 返回值

返回0阻止本次登出（角色留在世界里）；返回非0放行。未注册、解析失败或调用出错时默认放行。

## 参考实例

```lua
NL.RegLoginGateEvent(nil, "MyLoginGateEvent");

function MyLoginGateEvent(CharIndex)
  NLG.SystemMessage(CharIndex, "现在不能登出回记录点。");
  return 0; -- 返回0会阻止这次登出
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
名字里虽然带 Login，但它守的是登出：回调返回 0 会拦截这次登出，放行请返回 1。
