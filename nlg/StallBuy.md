<!-- Generated. DO NOT EDIT. -->
# StallBuy

## NLG.StallBuy(Buyer, Seller, BuyId, Currency, ExpectPrice)

### 函数功能

远程购买某个摊位上的一件商品，不要求买家站在摊位旁边（摆摊扩展）。

### 参数说明

- Buyer: [数值型](../appendix/数值型.md) 买家的对象index，必须是玩家。
- Seller: [数值型](../appendix/数值型.md) 摊主的对象index。
- BuyId: [数值型](../appendix/数值型.md) 使用 GetStallGoods 返回的 buy_id。低五宠0~4；高宠真实槽5~19使用256~270；道具8到卖家有效背包容量减一（最多247）。5~7、248~255、271以上无效。
- Currency: [数值型](../appendix/数值型.md) 支付货币，1 为魔币，2 为代币。
- ExpectPrice: [数值型](../appendix/数值型.md) 买家看到的价格（所选货币的价格）；与当前价格不一致时不成交。

### 返回值

结果码，沿用原生购买的编号并新增 13：
0 成功；1 找不到摊主；2 对方没有在摆摊；3 买家背包已满；4 买家宠物栏已满；5 买家魔币不足；6 该商品已售出或不接受这种货币；7 摊主收款后会超过金钱上限；8 道具已失效或不可上架；10 宠物已失效；11/12 宠物转移失败；13 价格已变动；100 其它失败（远程购买未开启、参数无效、买家就是摊主、买家自己正在摆摊、买家在战斗/组队/观战/交易中、宠物等级比买家高太多、交易事件拒绝等）。

## 参考实例

```lua
local sig = NLG.StallBuy(player, seller, 8, 1, 500);
if sig == 13 then
  NLG.SystemMessage(player, "价格已变动，请刷新后再买。");
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有，需要配置 `stall.remote_buy` 打开，否则一律返回 100。
复用原购买核心及 NL.RegStallTradeEvent 事件，不检查距离、不需要先打开摊位窗口。高宠编号256~270仅本 Lua API 接受，原生 wAo 拒绝这些编号。
Currency 为 2（代币）时还需要配置 `stall.token_price` 打开，并且交易事件在预检查阶段必须返回 1，否则不成交；代币的扣除与支付完全由交易事件处理，服务器不会动任何人的魔币。没有注册交易事件时，代币购买一律失败。
