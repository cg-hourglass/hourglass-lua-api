<!-- Generated. DO NOT EDIT. -->
# SetEvtNow

## Char.SetEvtNow(CharIndex, EventFlg)

### 函数功能

批量置位对象的 NowEvent 任务旗标。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- EventFlg: [数值型](../appendix/数值型.md)[数组] 要置位的任务旗标编号，可以从第二个参数起一次传入多个。

### 返回值

最后一个被处理的旗标编号；对象指针无效时返回 -1。

## 参考实例

```lua
Char.SetEvtNow(Player, 211);        -- 标记 211 号任务已接取
Char.SetEvtNow(Player, 211, 212);
```

### 备注

参数总数被限制在 2 到 20 之间，一次最多置位 19 个旗标。
