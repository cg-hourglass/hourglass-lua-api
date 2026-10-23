<!-- Generated. DO NOT EDIT. -->
# NowEvent

## Char.NowEvent(CharIndex, Flg, Value)

### 函数功能

读取或设置对象的 NowEvent 任务旗标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Flg: [数值型](../appendix/数值型.md) 任务旗标编号。
- Value: [数值型](../appendix/数值型.md) 省略时为读取；传 0 清除该旗标的 NowEvent 状态，传 1 置位。 [可为空]

### 返回值

两参数形式返回旗标状态 0 或 1。
三参数形式无论置位还是清除都固定返回 0。
对象指针无效时返回 -1；三参数形式下 Value 既不是 0 也不是 1 时打印日志并返回 nil。

## 参考实例

```lua
Char.NowEvent(Player, 211);      -- 返回玩家 211 号旗标是否为 NowEvent 状态
Char.NowEvent(Player, 211, 1);   -- 设置 211 号旗标为 NowEvent 状态
Char.NowEvent(Player, 211, 0);   -- 取消 211 号旗标的 NowEvent 状态
```

### 备注

三参数形式固定返回 0，这只是沿袭旧版行为的一个残留值，不代表操作成功。
要判断旗标最终状态，请另外用两参数形式或 Char.IsEventNow 复查。
