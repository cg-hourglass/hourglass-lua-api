<!-- Generated. DO NOT EDIT. -->
# EnemyGetData

## Data.EnemyGetData(EnemyIndex, DataPos)

### 函数功能

获取指定索引的怪物出场表条目（enemy.txt）在某个信息栏位上的值。

### 参数说明

- EnemyIndex: [数值型](../appendix/数值型.md) Enemy 文件的索引（来自 Data.EnemyGetIndex）。
- DataPos: [数值型](../appendix/数值型.md) Enemy 的相关常量：整数栏位与字符串栏位两个带（分界为 LUA_DATALINE1），具体边界请查看附录。

### 返回值

返回相应的值（整数栏位返回数值，字符串栏位返回字符串）；索引无效或 DataPos 越界时打印告警并返回 nil。

## 参考实例

```lua
local enemyName = Data.EnemyGetData(enemyIndex, 2000);
```

### 备注

与 Data.EnemyTempGetData 一样只有整数、字符串两个带，没有工作整数带。
索引参数如果传入 nil，会被静默转换成 0 再做校验，不会单独报参数错误。
