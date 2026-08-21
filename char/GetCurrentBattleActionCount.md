<!-- Generated. DO NOT EDIT. -->
# GetCurrentBattleActionCount

## Char.GetCurrentBattleActionCount(CharIndex)

### 函数功能

获取玩家在当前战斗回合内已提交的战斗指令数量。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

已提交的战斗指令数；对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
if Char.GetCurrentBattleActionCount(Player) > 1 then
    -- 一个回合提交了多条指令，可疑
end
```

### 备注

计数由战斗模块的反外挂计数器提供，读到的是战斗模块自己维护的实时值。
