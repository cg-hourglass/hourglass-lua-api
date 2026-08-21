<!-- Generated. DO NOT EDIT. -->
# RegGetNextLevelExpEvent

## NL.RegGetNextLevelExpEvent(Dofile, FuncName)

### 函数功能

注册读取升到下一级所需经验时触发的 Lua 函数，可以改写经验曲线。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## GetNextLevelExpEventCallBack(CharIndex, Level, Exp)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 查询经验的对象index；调用方没有角色上下文时传入 -1。由引擎传入。
- Level: [数值型](../appendix/数值型.md) 当前等级，由引擎传入。
- Exp: [数值型](../appendix/数值型.md) 服务器算出的所需经验，由引擎传入。

### 返回值

返回新的所需经验。不想改动就返回 Exp（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegGetNextLevelExpEvent(nil, "MyGetNextLevelExpEvent");

function MyGetNextLevelExpEvent(CharIndex, Level, Exp)
  return math.floor(Exp / 2); -- 升级所需经验减半
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
触发点在服务器查询等级经验门槛的地方，Char.LevelExp 的结果也会经过本事件加工。
本事件是少数容忍“没有角色”的回调之一，CharIndex 可能为 -1，脚本必须先判断再用它去查角色数据。
