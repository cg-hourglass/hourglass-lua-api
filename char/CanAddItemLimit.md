<!-- Generated. DO NOT EDIT. -->
# CanAddItemLimit

## Char.CanAddItemLimit(CharIndex, Delta)

### 函数功能

Check whether an additional slot grant fits in full without changing the player.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.
- Delta: [数值型](../appendix/数值型.md) Positive number of additional slots.

### 返回值

Boolean; false for invalid players, nonpositive deltas, or grants exceeding char.item_limit_max.

## 参考实例

```lua
if Char.CanAddItemLimit(player, 5) then
    Char.AddItemLimit(player, 5);
end
```

### 备注

Read-only preflight for serialized purchase callbacks; no reservation or persistence is performed.
