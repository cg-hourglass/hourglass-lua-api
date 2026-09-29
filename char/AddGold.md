<!-- Generated. DO NOT EDIT. -->
# AddGold

## Char.AddGold(CharIndex, Amount)

### 函数功能

为目标对象增减金钱。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Amount: [数值型](../appendix/数值型.md) 增加的数量，负数为减少。

### 返回值

调用被受理返回 1。
Amount 的绝对值超过 char_maxgoldhave 上限，或目标不是玩家时返回 -1；对象指针无效时也返回 -1。

## 参考实例

```lua
Char.AddGold(Player, 10000);    -- 加 10000 石币
Char.AddGold(Player, -500);     -- 扣 500 石币
```

### 备注

即使返回 1，如果增减之后的总额落在 [0, char_maxgoldhave] 之外，写入会被静默丢弃，
金钱一分不变——返回 1 只代表参数合法，不代表金钱一定变了。扣钱前请先用 GetData 读金钱自行判断。
