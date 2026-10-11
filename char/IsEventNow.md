<!-- Generated. DO NOT EDIT. -->
# IsEventNow

## Char.IsEventNow(CharIndex, EventFlg)

### 函数功能

检测对象的指定 NowEvent 任务旗标是否已经置位。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- EventFlg: [数值型](../appendix/数值型.md) 任务旗标编号。

### 返回值

布尔型，旗标已置位为 true，否则为 false；对象index无法解析时同样返回 false。

## 参考实例

```lua
if Char.IsEventNow(Player, 211) then
    NLG.TalkToCli(Player, -1, "任务进行中。");
end
```

### 备注

与 Char.NowEvent 的两参数形式读同一个旗标位，但本函数返回布尔值，NowEvent 返回 0/1 数值。
守卫只判断对象指针是否存在，不做完整的可用性检查。
