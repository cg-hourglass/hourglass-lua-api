<!-- Generated. DO NOT EDIT. -->
# ItemSlot

## Char.ItemSlot(CharIndex)

### 函数功能

统计对象道具栏中已被占用的栏位数量。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

已占用的道具栏栏位数，范围 0-20；对象指针无效时返回 -1。

## 参考实例

```lua
if Char.ItemSlot(Player) >= 20 then
    NLG.TalkToCli(Player, -1, "背包满了。");
end
```

### 备注

只统计道具栏 8-27，装备栏 0-7 不计入。这与 Char.ItemNum / HaveItem / FindItemId 扫描全部 0-27
的行为并不一致，是旧版就有的不对称，本服务端刻意原样保留。
另外这里不做道具index有效性检查，栏位里存着一个已失效的道具index也照样算作占用。
对象指针无效时会在服务端日志留下一条记录。
