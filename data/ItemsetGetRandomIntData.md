<!-- Generated. DO NOT EDIT. -->
# ItemsetGetRandomIntData

## Data.ItemsetGetRandomIntData(ItemsetIndex, DataPos)

### 函数功能

获取指定索引的道具模板在某个整数栏位上的随机浮动区间宽度。

### 参数说明

- ItemsetIndex: [数值型](../appendix/数值型.md) 道具模板的索引（来自 Data.ItemsetGetIndex）。
- DataPos: [数值型](../appendix/数值型.md) 道具的相关常量，仅整数栏位（0~1999）有意义。

### 返回值

返回该整数栏位的随机浮动区间宽度；索引无效或 DataPos 不在整数带范围内时打印告警并返回 nil。

## 参考实例

```lua
local attack = Data.ItemsetGetData(itemsetIndex, %道具_攻击%);
local attackdiff = Data.ItemsetGetRandomIntData(itemsetIndex, %道具_攻击%);
print("道具的攻击力基础值为"..attack.."，随机偏差值为"..attackdiff.."。");
```

### 备注

itemset.txt 里很多数值型栏位（如攻击力）会同时定义一个基础值与一个
随机浮动上限，本函数取的就是这个浮动上限（宽度），实际生成道具实例时
会在 [基础值, 基础值+宽度] 区间内取随机值。
