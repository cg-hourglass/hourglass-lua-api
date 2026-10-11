<!-- Generated. DO NOT EDIT. -->
# RegBattlePVPMaxHpEvent

## NL.RegBattlePVPMaxHpEvent(Dofile, FuncName)

### 函数功能

注册 PK 战斗初始化角色最大生命值时触发的 Lua 函数，可以改写该上限。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## BattlePVPMaxHpEventCallBack(CharIndex, BattleIndex, CurrentHp)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 参战对象的对象index，由引擎传入。
- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，由引擎传入。
- CurrentHp: [数值型](../appendix/数值型.md) 服务器算出的当前生命上限，由引擎传入。

### 返回值

返回新的生命上限。不想改动就返回 CurrentHp（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegBattlePVPMaxHpEvent(nil, "MyBattlePVPMaxHpEvent");

function MyBattlePVPMaxHpEvent(CharIndex, BattleIndex, CurrentHp)
  return CurrentHp * 2; -- 所有参战对象生命上限双倍
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
参战的所有对象都会触发，包括玩家和宠物，请自行用 CharIndex 判断类型。
两组触发点：战斗入场登记；以及决斗模式（BattleDuel）开启时的属性合规计算——后者就是 PvP 血量归一化的钩子。
