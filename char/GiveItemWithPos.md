<!-- Generated. DO NOT EDIT. -->
# GiveItemWithPos

## Char.GiveItemWithPos(CharIndex, ItemID, ItemPos, Amount, Mute)

### 函数功能

在指定道具栏位上给予目标对象道具。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。
- ItemPos: [数值型](../appendix/数值型.md) 道具要放入的栏位，取值 0-27。
- Amount: [数值型](../appendix/数值型.md) 道具的堆叠数量，默认 1。 [可为空]
- Mute: [数值型](../appendix/数值型.md) 是否显示获得道具的提示，0 显示、1 不显示，默认 0。 [可为空]

### 返回值

新创建出来的道具index；对象指针无效或 ItemPos 越界时返回 -1。

## 参考实例

```lua
Char.GiveItemWithPos(Player, 10001, 8);        -- 放进道具栏第一格
Char.GiveItemWithPos(Player, 10001, 8, 5, 1);  -- 静默放入 5 个的堆叠
```

### 备注

会先销毁 ItemPos 上原有的道具（对玩家还会发一条系统消息并写入道具日志），再把新道具放进去。
ItemPos 的合法范围是 0-27。
对象指针无效时会在服务端日志留下一条记录。
因为强制指定了栏位，一次只会产生一个道具实例，Amount 只影响该实例的堆叠数。
