<!-- Generated. DO NOT EDIT. -->
# UpItem

## Item.UpItem(CharIndex, Slot)

### 函数功能

向该角色关联的客户端发送指定道具槽位的数据封包，强制刷新道具栏显示。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index。
- Slot: [数值型](../appendix/数值型.md) A slot to refresh. Passing -1 refreshes all effective player slots (default 28, up to 248), preserving the legacy nonplayer range. Expanded full refreshes combine complete original I records under the existing byte budget.

### 返回值

目标对象无效返回 -1；正常返回 nil。

## 参考实例

```lua
Item.UpItem(player, -1); -- Refresh the full effective player item range.
```
