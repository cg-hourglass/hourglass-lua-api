<!-- Generated. DO NOT EDIT. -->
# GetItemRef

## Char.GetItemRef(CharIndex, Slot)

### 函数功能

返回当前携带栏道具的精确 runtime allocation identity（不经过 Lua number）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 已加载玩家或代理对象 index。
- Slot: [数值型](../appendix/数值型.md) 绝对携带栏位，包含装备；范围由 Char.GetBagSlotRange 决定。

### 返回值

道具返回十进制字符串，空栏返回空字符串；无效参数或状态返回 nil, BAD_ARGS/STATE。

## 参考实例

```lua
local ref, code = Char.GetItemRef(player, 8);
if ref == nil then print("reference failed: " .. code); end
```

### 备注

identity 只标识本次分配，不是道具 ID、持久化 ID、客户端 carry-view ref 或数量版本。不得转为 tonumber。
部分堆叠改变数量但保留 allocation identity；提交操作时应同时发送 expect_count。
