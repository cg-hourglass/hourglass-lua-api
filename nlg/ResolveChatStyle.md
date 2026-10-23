<!-- Generated. DO NOT EDIT. -->
# ResolveChatStyle

## NLG.ResolveChatStyle(CharIndex, StyleID, CatalogID)

### 函数功能

Validate a style reference against a character's current negotiated catalog.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) The current sender or intended recipient, supplied by the server.
- StyleID: [数值型](../appendix/数值型.md) Registered style ID, 1..65535.
- CatalogID: [字符串](../appendix/字符串.md) The exact catalog identity captured with this message.

### 返回值

A fresh table {style_id, catalog_id, color}, where color is the canonical legacy fallback; otherwise nil, error.

## 参考实例

```lua
local ref = NLG.ResolveChatStyle(player, message.style_id, message.catalog_id);
if ref then
  message["c"] = ref.color;
end
```

### 备注

This read-only operation never calls Hello, freezes a catalog, or enables readiness. It requires an online player with the same live connection and a ready catalog matching CatalogID, and membership of StyleID in that catalog. It is reusable for styled danmaku send validation and per-recipient live/history delivery. Failure must degrade the display to the stored classic fallback without reinterpreting the ID in another catalog. Resolve each recipient separately; never trust a client-provided fallback when resolution succeeds. Old APIs and normal chat packet signatures are unchanged.
