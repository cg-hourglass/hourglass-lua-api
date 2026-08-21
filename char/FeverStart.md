<!-- Generated. DO NOT EDIT. -->
# FeverStart

## Char.FeverStart(CharIndex)

### 函数功能

让玩家进入打卡（Fever）状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

成功返回 1，失败返回 0。

## 参考实例

```lua
Char.FeverStart(Player);
```

### 备注

已经处于打卡状态时直接返回 0，不会重新计时。
对象不是玩家或对象index无法解析时同样返回 0。
