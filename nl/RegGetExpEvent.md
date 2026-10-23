<!-- Generated. DO NOT EDIT. -->
# RegGetExpEvent

## NL.RegGetExpEvent(Dofile, FuncName)

### 函数功能

注册对象获得战斗经验时触发的 Lua 函数，可以改写实际获得的经验值。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## GetExpEventCallBack(CharIndex, Exp)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 获得经验的对象index（玩家或宠物），由引擎传入。
- Exp: [数值型](../appendix/数值型.md) 服务器算出的经验值，由引擎传入。

### 返回值

返回新的经验值。不想改动就返回 Exp，或者不写 return（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegGetExpEvent(nil, "MyGetExpEvent");

function MyGetExpEvent(CharIndex, Exp)
  return Exp * 2; -- 所有对象获得的经验双倍
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
只对玩家和宠物触发，敌人与 NPC 即使装了处理函数也不会进入 Lua。
返回值会写回角色的本场获得经验字段，而决斗点（DP）以该字段为基数计算，所以改经验会连带改动决斗点。
