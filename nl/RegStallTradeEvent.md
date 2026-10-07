<!-- Generated. DO NOT EDIT. -->
# RegStallTradeEvent

## NL.RegStallTradeEvent(Dofile, FuncName)

### 函数功能

注册摆摊交易时触发的 Lua 函数，可以自行处理金钱结算或直接拒绝交易。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## StallTradeEventCallBack(BuyerIndex, SellerIndex, TradeType, Price, BuyIndex, IsPreCheck, Currency, TokenPrice, SellerOffline)

### 参数说明

- BuyerIndex: [数值型](../appendix/数值型.md) 买家的对象index，由引擎传入。
- SellerIndex: [数值型](../appendix/数值型.md) 卖家（摊主）的对象index，由引擎传入。
- TradeType: [数值型](../appendix/数值型.md) 交易类型，由引擎传入。
- Price: [数值型](../appendix/数值型.md) 本次交易的价格，由引擎传入。
- BuyIndex: [数值型](../appendix/数值型.md) 购买的摊位商品序号，由引擎传入。
- IsPreCheck: [数值型](../appendix/数值型.md) 是否处于预检查阶段。1 表示预检查，0 表示实际交易。由引擎传入。
- Currency: [数值型](../appendix/数值型.md) 买家支付的货币，1 为魔币，2 为代币（摆摊扩展新增）。玩家在摊位窗口里的购买总是 1。
- TokenPrice: [数值型](../appendix/数值型.md) 该商品的代币价，没有代币价时为 0（摆摊扩展新增）。Price 始终是魔币价。
- SellerOffline: [数值型](../appendix/数值型.md) 摊主当前没有在线连接（离线摊位）时为 1，否则为 0（摆摊扩展新增）。

### 返回值

返回0让服务器执行自己的金钱结算逻辑；返回1表示脚本已经自行处理了金钱，服务器不再结算；返回-1拒绝这笔交易（只在预检查阶段有意义）。未注册、名字解析失败、买卖双方无效或调用出错时一律按 0 处理；唯一的例外是预检查返回 1 之后、实际交易阶段调用出错：此时脚本可能已经扣过一部分钱，服务器按「脚本已结算」处理（不再执行自己的金钱结算），并记一条错误日志供人工核对。Currency 为 2 时，预检查阶段只有返回 1 才会成交（返回 0 或 -1 都拒绝），实际交易阶段由脚本扣除买家的代币并支付给摊主，服务器不会结算任何金钱。

## 参考实例

```lua
NL.RegStallTradeEvent(nil, "MyStallTradeEvent");

function MyStallTradeEvent(BuyerIndex, SellerIndex, TradeType, Price, BuyIndex, IsPreCheck, Currency, TokenPrice, SellerOffline)
  if(Currency == 2)then
    if(IsPreCheck == 1)then
      return Char.ItemNum(BuyerIndex, 900) >= TokenPrice and 1 or -1;
    end
    Char.DelItem(BuyerIndex, 900, TokenPrice);
    Char.GiveItem(SellerIndex, 900, TokenPrice);
    return 1;
  end
  if(IsPreCheck == 1)then
    if(Price > 1000000)then
      return -1; -- 预检查阶段拒绝这笔交易
    end
    return 0;
  end
  return 0; -- 交给服务器自己的金钱结算逻辑
end
```

### 备注

每次成交的预检查与实际交易调用发生在同一个原子过程里，中间只有道具或宠物的转移，其它交易不会插进来；所以预检查阶段确认过的余额在实际交易阶段仍然有效。
处理函数里可以直接对买家和摊主调用 Char.DelItem、Char.GiveItem、Char.AddGold、Item.SetData、Field.Set 等函数完成结算。
最后三个参数是摆摊扩展追加的，只写前六个参数的旧脚本不受影响。
同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
三个触发点：一次预检查（IsPreCheck=1）与两次实际交易（IsPreCheck=0）。
买卖双方都必须是有效角色，否则引擎记一条诊断日志并按默认值 0 返回。
