<!-- Generated. DO NOT EDIT. -->
# WatchBattle

## NLG.WatchBattle(CharIndex, TargetCharIndex)

### 函数功能

让一名对象进入观战状态，观看另一名对象当前所在的战斗。

### 函数别名

- `NLG.WatchEntry(CharIndex, TargetCharIndex)`

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 发起观战的对象index（观战者）。
- TargetCharIndex: [数值型](../appendix/数值型.md) 被观战的对象index（必须当前正在战斗中）。

### 返回值

成功返回 0，失败（含两个对象任一无效、或目标当前没有可观战的战斗）返回 -1。

## 参考实例

```lua
NLG.WatchBattle(playerIndex, targetIndex);
```

### 备注

函数别名：`NLG.WatchEntry(...)`，参数与语义完全相同。
成功时返回的是 0，不是 1，判断成功请用 `== 0`。
