<!-- Generated. DO NOT EDIT. -->
# GetBattleIndex

## Char.GetBattleIndex(CharIndex)

### 函数功能

获取玩家当前所在战斗的战斗index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

当前战斗index；不在战斗中、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local BattleIndex = Char.GetBattleIndex(Player);
if BattleIndex ~= -1 then
    Battle.GetPlayIndex(BattleIndex, 0);
end
```

### 备注

只有对象确实处于战斗状态时才会返回有效的战斗index；失败路径全部安静，不打印日志。
