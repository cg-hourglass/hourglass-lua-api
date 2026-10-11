<!-- Generated. DO NOT EDIT. -->
# EnemyTempGetData

## Data.EnemyTempGetData(EnemyTempIndex, DataPos)

### 函数功能

获取指定索引的怪物基础模板（enemybase.txt）在某个信息栏位上的值。

### 参数说明

- EnemyTempIndex: [数值型](../appendix/数值型.md) Enemybase 文件的索引（来自 Data.EnemyTempGetIndex）。
- DataPos: [数值型](../appendix/数值型.md) Enemybase 的相关常量：整数栏位与字符串栏位两个带（分界为 LUA_DATALINE1），具体边界请查看附录。

### 返回值

返回相应的值（整数栏位返回数值，字符串栏位返回字符串）；索引无效或 DataPos 越界时打印告警并返回 nil。

## 参考实例

```lua
local hp = Data.EnemyTempGetData(baseIndex, 0);
```

### 备注

与 Data.ItemsetGetData 不同，Enemybase 只有整数、字符串两个带，没有
第三个工作整数带；DataPos 落在第三带的位置会直接走「打印告警并返回
nil」的分支。
