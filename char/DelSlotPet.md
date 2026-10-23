<!-- Generated. DO NOT EDIT. -->
# DelSlotPet

## Char.DelSlotPet(CharIndex, Slot)

### 函数功能

删除对象指定宠物栏位上的宠物。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 宠物栏位置，范围 0-4。

### 返回值

成功删除返回 1；栏位为空、栏位越界或对象不是玩家时返回 0；对象指针无效时返回 -1。

## 参考实例

```lua
Char.DelSlotPet(Player, 0);
```

### 备注

与 Char.DelPet 一样会清理放牧与骑乘状态并写入宠物日志，只是按栏位而不是按 ID 选目标。
对象指针无效时会在服务端日志留下一条记录。
