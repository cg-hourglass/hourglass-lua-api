<!-- Generated. DO NOT EDIT. -->
# ChatStyleReady

## NLG.ChatStyleReady(CharIndex, CatalogID)

### 函数功能

Mark the negotiated chat catalog as installed for this character and connection.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) The same currently online player that called ChatStyleHello.
- CatalogID: [字符串](../appendix/字符串.md) The exact catalog_id returned by ChatStyleHello.

### 返回值

true on success; otherwise nil, error.

## 参考实例

```lua
assert(NLG.ChatStyleReady(player, catalog.catalog_id));
```

### 备注

The client installs the catalog before requesting Ready. The server enables readiness before returning true. Readiness is bound to the actual connection and character lifetime, not a reusable numeric session ID, and is cleared on detach, cleanup, and session reassignment. Repeated Ready is idempotent. Sender membership/readiness is required to preserve an incoming style: known but nonready styles become fallback_color, unknown reserved styles become white, and the message continues through the original chat path. Readiness loss during EVENT_TALK likewise downgrades rather than dropping the message. Recipients without readiness receive fallback_color independently.
