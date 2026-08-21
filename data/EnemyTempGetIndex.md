<!-- Generated. DO NOT EDIT. -->
# EnemyTempGetIndex

## Data.EnemyTempGetIndex(EnemyID)

### 函数功能

通过 Enemy ID 获取该 Enemy 在 enemybase.txt（怪物基础模板表）中的索引。

### 参数说明

- EnemyID: [数值型](../appendix/数值型.md) Enemy ID。

### 返回值

找到返回对应的 enemybase 索引；查无该 Enemy ID 返回 -1。

## 参考实例

```lua
local baseIndex = Data.EnemyTempGetIndex(1001);
```

### 备注

内部先在 enemy.txt 表里线性扫描匹配 Enemy ID，再取该条目在 enemybase.txt
里登记的模板索引——因此即使 Enemy ID 存在于 enemy.txt，只要它没有配置
对应的 enemybase 模板，本函数也会返回 -1（与 Data.EnemyGetIndex 是两张
不同的表，返回值不能混用）。
