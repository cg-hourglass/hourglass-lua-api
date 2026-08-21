<!-- Generated. DO NOT EDIT. -->
# ItemsetGetData

## Data.ItemsetGetData(ItemsetIndex, DataPos)

### 函数功能

获取指定索引的道具模板在某个信息栏位上的值。

### 参数说明

- ItemsetIndex: [数值型](../appendix/数值型.md) 道具模板的索引（来自 Data.ItemsetGetIndex）。
- DataPos: [数值型](../appendix/数值型.md) 道具的相关常量：0~1999 为整数栏位，2000~3999 为字符串栏位，
4000~5999 为工作用整数栏位。

### 返回值

返回相应的值（整数/工作整数栏位返回数值，字符串栏位返回字符串）；索引无效或 DataPos 越界时打印告警并返回 nil。

## 参考实例

```lua
local attack = Data.ItemsetGetData(itemsetIndex, %道具_攻击%);
```

### 备注

工作整数带（4000~5999）目前恒定返回 0，不代表这个带位承载有意义的
数据。
