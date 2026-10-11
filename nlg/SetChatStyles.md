<!-- Generated. DO NOT EDIT. -->
# SetChatStyles

## NLG.SetChatStyles(Catalog)

### 函数功能

Register the immutable native chat text style catalog.

### 参数说明

- Catalog: [表](../appendix/表.md) A declarative version 1 catalog with styles and append_cycle arrays.

### 返回值

true on success; nil, error on invalid input, budget overflow, or frozen catalog mutation.

## 参考实例

```lua
assert(NLG.SetChatStyles{
  version = 1,
  styles = {{id = 1, name = "Rainbow", fallback_color = 2,
    fill = {kind = "gradient", colors = {0xff0000, 0x0000ff},
      spread_px = 128, repeat_mode = "repeat"},
    animation = {kind = "scroll", period_ms = 4000}}},
  append_cycle = {1}
});
```

### 备注

Exactly version, styles, and append_cycle are required. Empty arrays are allowed (the existing JSON transport encodes empty Lua tables as {}). At most 32 styles; IDs are unique integers 1..65535; name is a nonempty string of at most 48 UTF-8 bytes through the normal guest text boundary; ASCII control characters below 0x20 and DEL are rejected. fallback_color is one of 0,1,2,3,5,6,7,8,9. Every unknown field, missing field, fractional integer, sparse array, invalid cycle reference, and duplicate cycle reference is rejected.
A solid fill has exactly kind="solid" and color=0xRRGGBB. A gradient has exactly kind="gradient", colors (2..8 RGB integers), spread_px (integer 16..512), and repeat_mode ("repeat" or "clamp"). Optional animation has exactly kind ("scroll" or "pulse") and period_ms (integer 1000..30000). No functions or executable values are accepted; table reads do not invoke metatables.
Native canonical catalog JSON, including catalog_id, must fit 6000 bytes. Registration also checks the ASCII-only RPC projection with uppercase hex UTF-8 names and name_encoding="utf8hex": the complete chatstyle|hello|9999999999|1/1|{"ok":CATALOG} frame must fit 8000 bytes after protocol escaping. The first successful ChatStyleHello freezes the catalog process-wide. Identical registrations remain idempotent; hot reload is not supported. No catalog is installed by default.
