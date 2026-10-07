<!-- Generated. DO NOT EDIT. -->
# RegGetLoginPointEvent

## NL.RegGetLoginPointEvent(Dofile, FuncName)

### 函数功能

注册玩家登入时读取登录点信息触发的 Lua 函数，可用来实现原地登录。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## GetLoginPointEventCallBack(CharIndex, MapID, FloorID, X, Y)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 正在登入的玩家对象index，由引擎传入。
- MapID: [数值型](../appendix/数值型.md) 服务器算出的登录 map id，由引擎传入。
- FloorID: [数值型](../appendix/数值型.md) 服务器算出的登录 floor id，由引擎传入。
- X: [数值型](../appendix/数值型.md) 服务器算出的登录 x 坐标，由引擎传入。
- Y: [数值型](../appendix/数值型.md) 服务器算出的登录 y 坐标，由引擎传入。

### 返回值

无返回值。引擎以 0 个返回值调用本函数，返回什么都不会被读取。要改变登录位置必须在回调里同步用 Char.SetData 改写角色坐标。

## 参考实例

```lua
NL.RegGetLoginPointEvent(nil, "MyGetLoginPointEvent");

function MyGetLoginPointEvent(CharIndex, MapID, FloorID, X, Y)
  -- 直接改写角色坐标即可，不需要 warp，也不需要 return
  Char.SetData(CharIndex, %对象_地图编号%, 1000);
  Char.SetData(CharIndex, %对象_X坐标%, 235);
  Char.SetData(CharIndex, %对象_Y坐标%, 83);
  return 0;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
引擎不会从回调里读回坐标：无论返回数值还是返回 table，登录点都不会因此改变。
要改写登录位置，必须在回调里同步用 Char.SetData 改角色坐标。
正常登入与离线登入两条路径都会触发。
