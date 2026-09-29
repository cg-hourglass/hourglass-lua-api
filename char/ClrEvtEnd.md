<!-- Generated. DO NOT EDIT. -->
# ClrEvtEnd

## Char.ClrEvtEnd(CharIndex, EventFlg)

### 函数功能

批量清除对象的 EndEvent 任务旗标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- EventFlg: [数值型](../appendix/数值型.md)[数组] 要清除的任务旗标编号，可以从第二个参数起一次传入多个。

### 返回值

最后一个被处理的旗标编号；对象指针无效时返回 -1。

## 参考实例

```lua
Char.ClrEvtEnd(Player, 211);
Char.ClrEvtEnd(Player, 211, 212, 213);   -- 一次清掉三个旗标
```

### 备注

参数总数被限制在 2 到 20 之间，也就是一次最多清 19 个旗标。
函数按参数顺序逐个执行清除，返回值只是最后一个旗标编号，不代表操作成败。
