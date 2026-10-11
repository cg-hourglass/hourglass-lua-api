<!-- Generated. DO NOT EDIT. -->
# GetCurrentBattle

## Battle.GetCurrentBattle(CharIndex)

### 函数功能

获取指定对象当前所处战斗的战斗index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

成功返回战斗index；-1 对象无效或对象记录的战斗index非法；-2 该战斗槽未在使用，或对象的战斗状态为 %战斗状态_无%。

## 参考实例

```lua
local TM_BattleIndex = Battle.GetCurrentBattle(TM_CharIndex);
if TM_BattleIndex >= 0 then
    print("turn = " .. Battle.GetTurn(TM_BattleIndex));
end
```

### 备注

这是整个 Battle 库中唯一一个会同时检查“战斗槽在用”和“对象战斗状态非空”的函数，
其余取值函数只做数组边界检查。
