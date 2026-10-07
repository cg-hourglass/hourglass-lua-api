<!-- Generated. DO NOT EDIT. -->
# SetTimeLimit

## Item.SetTimeLimit(CharIndex, ItemIndex, Time)

### 函数功能

设置或清除道具实例的时限属性。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index。
- ItemIndex: [数值型](../appendix/数值型.md) 目标道具 index，传 -1 时函数不做任何事。
- Time: [数值型](../appendix/数值型.md) 时限秒数；大于 0 时设置为「当前时间 + Time 秒」后到期，小于等于 0 时清除时限。

### 返回值

对象无效时返回 -1；正常返回 nil。

## 参考实例

```lua
Item.SetTimeLimit(player, item, 100); -- 100秒后道具时限到。
Item.SetTimeLimit(player, item, -1); -- 将时限道具的时限取消。
```

### 备注

时限的绝对到期时间戳取自服务器每 tick 缓存的当前时间，不是每次调用都
重新读系统时钟。
