<!-- Generated. DO NOT EDIT. -->
# GiveItem

## Char.GiveItem(CharIndex, ItemID, Amount, Mute)

### 函数功能

给予目标对象指定 ID 的道具。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。
- Amount: [数值型](../appendix/数值型.md) 给予的数量，默认 1。 [可为空]
- Mute: [数值型](../appendix/数值型.md) 是否显示获得道具的提示，0 显示、1 不显示，默认 0。 [可为空]

### 返回值

最后一个被创建出来的道具index；对象指针无效时返回 -1。

## 参考实例

```lua
Char.GiveItem(Player, 10001);          -- 给一个 10001 号道具
Char.GiveItem(Player, 10001, 5, 1);    -- 静默给 5 个
```

### 备注

道具会按自身的堆叠上限自动堆叠。背包放不下时会静默少给，但返回值仍是最后一个成功创建的道具index，
因此返回值不能用来判断是否全部给足；要确认结果请随后用 Char.ItemNum 复查数量。
