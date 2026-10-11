<!-- Generated. DO NOT EDIT. -->
# DelItem

## Char.DelItem(CharIndex, ItemID, Amount, ShowMessage)

### 函数功能

删除目标对象身上指定 ID 的道具。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- ItemID: [数值型](../appendix/数值型.md) 道具 ID，对应 item.txt 中的编号。
- Amount: [数值型](../appendix/数值型.md) 要删除的数量，默认 1。 [可为空]
- ShowMessage: [数值型](../appendix/数值型.md) 是否显示删除道具的提示，1 显示、0 不显示，默认 1。 [可为空]

### 返回值

成功删除返回 1；数量不足以扣满、扫描不到目标道具时返回 0；对象指针无效时返回 -1。

## 参考实例

```lua
Char.DelItem(Player, 10001);
Char.DelItem(Player, 10001, 3, 0);   -- 静默删掉 3 个
```

### 备注

Amount 传入小于等于 0 时会被强制改成 1。
扫描覆盖 0-27 全部栏位，装备栏 0-7 也在内；可堆叠道具先扣堆叠数，扣不完才整格删除。
删除完成后会重算属性、重发道具栏与角色数据。
