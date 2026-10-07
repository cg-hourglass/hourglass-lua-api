<!-- Generated. DO NOT EDIT. -->
# GetCurrentBattleTechActionCount

## Char.GetCurrentBattleTechActionCount(CharIndex)

### 函数功能

获取玩家在当前战斗回合内已提交的技能指令数量。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

已提交的技能指令数，正常情况下是 0 或 1；对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
if Char.GetCurrentBattleTechActionCount(Player) > 1 then
    -- 超过 1 会触发反外挂系统
end
```

### 备注

计数由战斗模块维护，读到的是实时值。
