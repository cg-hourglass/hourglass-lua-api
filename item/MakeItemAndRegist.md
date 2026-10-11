<!-- Generated. DO NOT EDIT. -->
# MakeItemAndRegist

## Item.MakeItemAndRegist(ItemId, ItemCount)

### 函数功能

创建一个未挂靠任何角色的游离道具实例，并返回其 ItemIndex。

### 参数说明

- ItemId: [数值型](../appendix/数值型.md) 要创建的道具模板 ID。
- ItemCount: [数值型](../appendix/数值型.md) 期望的堆叠数量；小于等于 0 时按 1 处理，超过该道具的最大堆叠上限时会被夹到上限。

### 返回值

创建成功返回新道具实例的 ItemIndex；失败返回 -1。

## 参考实例

```lua
local newItem = Item.MakeItemAndRegist(10001, 5);
```

### 备注

创建出的道具不属于任何角色，需要脚本自行用 Item.TradeItem 或角色相关
API 交给玩家。
