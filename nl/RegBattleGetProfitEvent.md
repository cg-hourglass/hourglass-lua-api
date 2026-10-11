<!-- Generated. DO NOT EDIT. -->
# RegBattleGetProfitEvent

## NL.RegBattleGetProfitEvent(Dofile, FuncName)

### 函数功能

注册战斗结算发放奖励时触发的 Lua 函数，可以改写掉落道具或决斗点。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## BattleGetProfitCallBack(BattleIndex, Side, Pos, CharIndex, ProfitType, Profit)

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，由引擎传入。
- Side: [数值型](../appendix/数值型.md) 领取奖励一方的阵营编号，由引擎传入。
- Pos: [数值型](../appendix/数值型.md) 领取奖励角色在阵营中的位置，由引擎传入。
- CharIndex: [数值型](../appendix/数值型.md) 领取奖励的角色对象index，由引擎传入。
- ProfitType: [数值型](../appendix/数值型.md) 奖励类型。-1 经验（已定义但从不触发）；-2 决斗点（DP）；0~2 三个道具槽位。由引擎传入。
- Profit: [数值型](../appendix/数值型.md) 对应类型的值：DP 类型时是数值，道具类型时是道具对象index，没有道具掉落时为 -1。由引擎传入。

### 返回值

返回新的值。DP 类型返回新的数值；道具类型返回新的道具对象index（可用 Item.MakeItemAndRegist 创建）。不想改动就返回 Profit（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegBattleGetProfitEvent(nil, "MyBattleGetProfitEvent");

function MyBattleGetProfitEvent(BattleIndex, Side, Pos, CharIndex, ProfitType, Profit)
  if(ProfitType == 0)then
    print(CharIndex.."在战斗中获得了道具"..Profit);
    local newItemIndex = Item.MakeItemAndRegist(1000, 1);
    return newItemIndex; -- 把战利品替换成 item id 为 1000 的道具
  end
  return Profit;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
两个触发点：战斗结算发放道具掉落（ProfitType 0~2），以及发放决斗点（ProfitType -2）。
道具类型时返回一个不同的道具index，服务器会销毁原来的掉落物并改发脚本给出的那一个：这里返回垃圾值会破坏道具状态，务必返回合法的道具index。
