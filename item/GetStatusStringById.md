<!-- Generated. DO NOT EDIT. -->
# GetStatusStringById

## Item.GetStatusStringById(ItemId, ViewerIndex)

### 函数功能

按道具ID生成一个新道具的原生状态串，用于商城等还没有实例的场合（摆摊扩展）。

### 参数说明

- ItemId: [数值型](../appendix/数值型.md) 道具ID（itemset 编号）。
- ViewerIndex: [数值型](../appendix/数值型.md) 查看者的对象index，必须是玩家。

### 返回值

格式与 Item.GetStatusString 相同的状态串；道具ID无效或查看者无效时返回 nil。

## 参考实例

```lua
local status = Item.GetStatusStringById(18000, player);
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
内部按道具模板临时生成一个实例，取完状态串立即释放，不会进入任何背包；显示的内容与玩家刚获得这件道具时相同。
