<!-- Generated. DO NOT EDIT. -->
# UpItem

## Item.UpItem(CharIndex, Slot)

### 函数功能

向该角色关联的客户端发送指定道具槽位的数据封包，强制刷新道具栏显示。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index。
- Slot: [数值型](../appendix/数值型.md) 指定背包槽位（0~27）；传 -1 时刷新全部 28 个槽位。

### 返回值

目标对象无效返回 -1；正常返回 nil。

## 参考实例

```lua
Item.UpItem(player, -1); -- 刷新玩家全部道具栏
```
