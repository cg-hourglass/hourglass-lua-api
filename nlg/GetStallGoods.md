<!-- Generated. DO NOT EDIT. -->
# GetStallGoods

## NLG.GetStallGoods(CharIndex)

### 函数功能

读取一个摊位上正在出售的道具和宠物（摆摊扩展）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 摊主的对象index。

### 返回值

对象不是正在摆摊的玩家时返回 nil；否则返回
`{items = {{slot = 背包栏位, item = 道具index, gold = 魔币价, token = 代币价}, ...}, pets = {{slot = 宠物栏位, pet = 宠物对象index, gold = 魔币价, token = 代币价}, ...}}`，
items 与 pets 都是从下标 1 开始、按栏位顺序排列的 table，可能为空。

## 参考实例

```lua
local goods = NLG.GetStallGoods(seller);
if goods then
  for _, g in ipairs(goods.items) do
    print(g.slot, Item.GetData(g.item, %道具_名字%), g.gold, g.token);
  end
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
只列出魔币价或代币价大于 0、并且栏位上确实有东西的商品；不可上架的道具不会出现。价格 0 表示该商品不接受这种货币。
道具和宠物的详细数据请用 Item.GetData / Char.GetData 自己读取；需要原生浮框用的状态串时用 Item.GetStatusString / Char.GetPetStatusString。
