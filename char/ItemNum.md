<!-- Generated. DO NOT EDIT. -->
# ItemNum

## Char.ItemNum(CharIndex, ItemID)

### 函数功能

统计对象身上指定 ID 道具的总数量。

### 函数别名

- `Char.HaveItemNum(CharIndex, ItemID)`

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。

### 返回值

拥有的总数量，没有则返回 0；对象指针无效时返回 -1。

## 参考实例

```lua
if Char.ItemNum(Player, 10001) >= 3 then
    Char.DelItem(Player, 10001, 3);
end
```

### 备注

扫描 0-27 全部栏位，装备栏 0-7 同样计入；可堆叠道具按堆叠数累加，其余每格记 1。
“没有该道具”返回 0，“对象指针无效”返回 -1，这两者要分开判断。
别名 Char.HaveItemNum 与本函数是同一个实现。
