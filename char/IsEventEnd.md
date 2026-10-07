<!-- Generated. DO NOT EDIT. -->
# IsEventEnd

## Char.IsEventEnd(CharIndex, EventFlg)

### 函数功能

检测对象的指定 EndEvent 任务旗标是否已经置位。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- EventFlg: [数值型](../appendix/数值型.md) 任务旗标编号。

### 返回值

布尔型，旗标已置位为 true，否则为 false；对象index无法解析时同样返回 false。

## 参考实例

```lua
if Char.IsEventEnd(Player, 211) then
    NLG.TalkToCli(Player, -1, "这个任务你已经做完了。");
end
```

### 备注

本函数与 Char.EndEvent 的两参数形式读的是同一个旗标位，但返回类型不同：
这里是 Lua 布尔值，Char.EndEvent 返回的是 0/1 数值。
守卫只判断对象指针是否存在，不做完整的可用性检查，因此一个已注册但不可用的对象仍然能读到旗标。
