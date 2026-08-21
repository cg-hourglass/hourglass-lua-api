<!-- Generated. DO NOT EDIT. -->
# SetBattleCharacterStatus

## Battle.SetBattleCharacterStatus(CharIndex, Status, Val)

### 函数功能

设置对象当前的某一项战斗状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index，可以是玩家、宠物或敌人。
- Status: [数值型](../appendix/数值型.md) 状态类型，取值与 Battle.GetBattleCharacterStatus 的状态类型说明一致。
- Val: [数值型](../appendix/数值型.md) 要写入的状态值。

### 返回值

成功返回写入的新值；对象无效、战斗index非法或状态类型不可写时返回 -1。

## 参考实例

```lua
Battle.SetBattleCharacterStatus(TM_CharIndex, %战属_等回合%, 2); -- 让对象停两回合
```

### 备注

可写的状态类型见 Battle.GetBattleCharacterStatus 的状态类型说明，但
**%战属_恢复魔法LV%（26）是只读的**：写入它不会产生任何效果，且返回 -1，这是本版本
的既有行为，脚本不要依赖写入该项来改变状态。
