<!-- Generated. DO NOT EDIT. -->
# GetPoolItem

## Char.GetPoolItem(CharIndex, Slot)

### 函数功能

获取玩家银行中指定位置的道具index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 银行道具栏位置，本版本范围 0-39。

### 返回值

该位置的道具index；位置为空、位置越界、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
for i = 0, 39 do
    local ItemIndex = Char.GetPoolItem(Player, i);
    if ItemIndex ~= -1 then
        -- 银行该位置有道具
    end
end
```

### 备注

读的是银行（Pool）道具栏，不是出租屋。
位置上限本版本是 40，即 0-39。
对象指针无效时会在服务端日志留下一条错误记录。
