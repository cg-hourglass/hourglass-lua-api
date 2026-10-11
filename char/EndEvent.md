<!-- Generated. DO NOT EDIT. -->
# EndEvent

## Char.EndEvent(CharIndex, Flg, Value)

### 函数功能

读取或设置对象的 EndEvent 任务旗标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Flg: [数值型](../appendix/数值型.md) 任务旗标编号。
- Value: [数值型](../appendix/数值型.md) 省略时为读取；传 0 清除该旗标的 EndEvent 状态，传 1 置位。 [可为空]

### 返回值

两参数形式返回旗标状态 0 或 1。
三参数形式无论置位还是清除都返回 0。
对象指针无效时返回 -1；三参数形式下 Value 既不是 0 也不是 1 时打印日志并返回 nil。

## 参考实例

```lua
Char.EndEvent(Player, 211);      -- 返回玩家 211 号旗标是否为 EndEvent 状态
Char.EndEvent(Player, 211, 1);   -- 设置 211 号旗标为 EndEvent 状态
Char.EndEvent(Player, 211, 0);   -- 取消 211 号旗标的 EndEvent 状态
```

### 备注

与 Char.NowEvent 形状一致，区别只在旗标的哪一半：这里读写的是 EndEvent 位。
三参数形式的返回值恒为 0，不代表成败。
