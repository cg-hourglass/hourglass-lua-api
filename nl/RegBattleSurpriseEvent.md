<!-- Generated. DO NOT EDIT. -->
# RegBattleSurpriseEvent

## NL.RegBattleSurpriseEvent(Dofile, FuncName)

### 函数功能

注册战斗偷袭判定时触发的 Lua 函数，可以改写偷袭结果。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## BattleSurpriseEventCallBack(BattleIndex, SurpriseSide)

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，由引擎传入。
- SurpriseSide: [数值型](../appendix/数值型.md) 服务器判定出的偷袭方。0 = 无偷袭；1 = 敌方被偷袭；2 = 玩家方被偷袭。由引擎传入。

### 返回值

返回新的偷袭设置（0、1、2）。不想改动就返回 SurpriseSide（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegBattleSurpriseEvent(nil, "MyBattleSurpriseEvent");

function MyBattleSurpriseEvent(BattleIndex, SurpriseSide)
  return 1; -- 永远由敌方被偷袭
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
每场战斗在初始化时只触发一次，时机早于 RegBattleStartEvent。
本服务端的这个注册函数可以像其它事件一样用 nil 取消注册，传 nil 是安全的；
历史版本的同名函数在这里有缺陷，反注册分支走不到、传 nil 还会崩溃。
