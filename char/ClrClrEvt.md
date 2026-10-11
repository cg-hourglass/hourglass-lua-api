<!-- Generated. DO NOT EDIT. -->
# ClrClrEvt

## Char.ClrClrEvt(CharIndex, EventFlg)

### 函数功能

批量同时清除对象的 NowEvent 与 EndEvent 任务旗标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- EventFlg: [数值型](../appendix/数值型.md)[数组] 要清除的任务旗标编号，可以从第二个参数起一次传入多个。

### 返回值

最后一个被处理的旗标编号；对象指针无效时返回 -1。

## 参考实例

```lua
Char.ClrClrEvt(Player, 211);        -- 把 211 号任务彻底重置
Char.ClrClrEvt(Player, 211, 212);
```

### 备注

这是把一个任务旗标彻底重置回“没接过”状态的写法：NowEvent 与 EndEvent 两半都会被清掉。
参数总数被限制在 2 到 20 之间，一次最多清 19 个旗标。
