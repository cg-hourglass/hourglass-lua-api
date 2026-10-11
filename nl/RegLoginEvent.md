<!-- Generated. DO NOT EDIT. -->
# RegLoginEvent

## NL.RegLoginEvent(Dofile, FuncName)

### 函数功能

注册玩家登入游戏时触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽，因此可以在同一次调用里加载定义处理函数的脚本。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析，注册时不要求该函数已定义。传 nil（或任何不能转成字符串的值）即清空该事件槽，等同于取消注册。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数（触发时会再解析一次）。

## LoginEventCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 登入的玩家对象index，由引擎传入。

### 返回值

返回0即可。引擎以 0 个返回值调用本函数，返回什么都不会被读取。

## 参考实例

```lua
NL.RegLoginEvent(nil, "MyLoginEvent");

function MyLoginEvent(CharIndex)
  print(Char.GetData(CharIndex, %对象_名字%));
  return 0;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
正常登入与离线登入都会触发本事件，触发点在登入流程末尾。
