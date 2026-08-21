<!-- Generated. DO NOT EDIT. -->
# ItemsetGetIndex

## Data.ItemsetGetIndex(ItemID)

### 函数功能

通过道具 ID 获取该道具在 ITEMSET.txt（道具模板表）中的索引。

### 参数说明

- ItemID: [数值型](../appendix/数值型.md) 道具 ID。

### 返回值

存在则返回该道具在索引文件中的 index，用于 Data.ItemsetGetData 和 Data.ItemsetGetRandomIntData；不存在返回 -1。

## 参考实例

```lua
local itemsetIndex = Data.ItemsetGetIndex(10001);
```

### 备注

本服务端的道具模板索引直接使用道具 ID 本身作为 index（不是「加载顺序
序号」）；调用方不应对该 index 的具体数值做任何假设，只应把它当作
不透明句柄传给另外两个 Data.Itemset* 函数。
