<!-- Generated. DO NOT EDIT. -->
# TradeItem

## Item.TradeItem(FromCharIndex, TargetCharIndex, ItemIndex)

### 函数功能

将一个玩家的道具实例转移给另一个玩家的背包（不弹交易窗口，直接转移）。

### 参数说明

- FromCharIndex: [数值型](../appendix/数值型.md) 道具当前持有者的对象 index，必须是玩家类型。
- TargetCharIndex: [数值型](../appendix/数值型.md) 接收道具的对象 index，必须是玩家类型。
- ItemIndex: [数值型](../appendix/数值型.md) 指定道具 index。

### 返回值

负数表示失败，非负数表示成功且为道具在接收者背包中落位的槽位序号
（从 `CHAR_STARTITEMARRAY` 起算，非从 0 开始的原始槽位下标）。

- `-1`：参数错误（FromCharIndex/TargetCharIndex 不是有效的玩家、或
  ItemIndex 无效）
- `-2`：道具不属于 FromCharIndex
- `-3`：TargetCharIndex 身上无空位

## 参考实例

```lua
local slot = Item.TradeItem(fromPlayer, toPlayer, item);
if (slot < 0) then
  NLG.SystemMessage(-1, "道具转移失败："..slot);
end
```

### 备注

成功路径会重算双方的属性加成、下发 CP/CP2/组队数据同步封包，并各写
一条审计记录。
