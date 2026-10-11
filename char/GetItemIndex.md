<!-- Generated. DO NOT EDIT. -->
# GetItemIndex

## Char.GetItemIndex(CharIndex, Slot)

### 函数功能

读取对象指定道具栏位上的道具index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 道具栏位置，取值 0-27，其中 0-7 为装备栏，8-27 为道具栏。

### 返回值

该栏位上的道具index。
-1 表示对象指针无效，-2 表示该栏位没有有效道具，-3 表示栏位号超出 0-27 范围。

## 参考实例

```lua
for i = 8, 27 do
    local ItemIndex = Char.GetItemIndex(Player, i);
    if ItemIndex >= 0 then
        -- 该栏位有道具
    end
end
```

### 备注

-3 分支会在服务端日志留下一条记录，-1 与 -2 分支保持安静。
三个负值含义不同，判断“有没有道具”时请用 `>= 0` 而不是 `~= -1`。
