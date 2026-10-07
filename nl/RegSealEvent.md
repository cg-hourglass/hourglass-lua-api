<!-- Generated. DO NOT EDIT. -->
# RegSealEvent

## NL.RegSealEvent(Dofile, FuncName)

### 函数功能

注册玩家封印宠物时触发的 Lua 函数，可以改写封印结果。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## SealEventCallBack(CharIndex, TargetCharIndex, Ret)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 使用封印卡的玩家对象index，由引擎传入。
- TargetCharIndex: [数值型](../appendix/数值型.md) 被封印对象的对象index，由引擎传入。
- Ret: [数值型](../appendix/数值型.md) 服务器判定出的封印结果，小于等于 0 为失败、大于 0 为成功，具体取值见备注。由引擎传入。

### 返回值

返回新的封印结果，会原样覆盖服务器的判定值且不做范围检查。不想改动就返回 Ret（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegSealEvent(nil, "MySealEvent");

function MySealEvent(CharIndex, TargetCharIndex, Ret)
  return 1; -- 封印永远成功
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
只在战斗中使用封印卡时触发。
Ret 的失败取值：-1 被封印对象类型错误；-2 被封印对象不能作为宠物；-3 玩家宠物栏位不足；-4 玩家等级不足；-5 目标是召唤出来的而非野生的；-6 玩家没有该宠物的图鉴；-7 封印卡道具不存在；-8 使用的道具不是封印卡；-9 封印卡没有参数设置；-10 封印卡种族不正确；-11 不能封印邪魔系宠物；小于等于 -100 表示随机几率不足，还原几率的公式为 abs(Ret/100)-1。
第二个参数传入的是被封印角色的对象index，不是敌人队列下标。
