<!-- Generated. DO NOT EDIT. -->
# EnemyGetIndex

## Data.EnemyGetIndex(EnemyID)

### 函数功能

通过 Enemy ID 获取该 Enemy 在 enemy.txt（怪物出场表）中的索引。

### 参数说明

- EnemyID: [数值型](../appendix/数值型.md) Enemy ID。

### 返回值

找到返回对应的索引（数组下标）；查无该 Enemy ID 返回 -1。

## 参考实例

```lua
local enemyIndex = Data.EnemyGetIndex(1001);
```
