<!-- Generated. DO NOT EDIT. -->
# FeverStop

## Char.FeverStop(CharIndex)

### 函数功能

结束玩家的打卡（Fever）状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

成功返回 1，失败返回 0。

## 参考实例

```lua
Char.FeverStop(Player);
```

### 备注

不在打卡状态时直接返回 0。对象不是玩家或对象index无法解析时同样返回 0。
