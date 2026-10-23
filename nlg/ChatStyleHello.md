<!-- Generated. DO NOT EDIT. -->
# ChatStyleHello

## NLG.ChatStyleHello(CharIndex, Version)

### 函数功能

Negotiate version 1 chat style capability for the current online character and connection.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) The currently online player character index.
- Version: [数值型](../appendix/数值型.md) Must be 1, supporting solid, gradient, scroll, and pulse.

### 返回值

A fresh catalog table with version, catalog_id, styles, append_cycle; otherwise nil, error.

## 参考实例

```lua
local catalog, err = NLG.ChatStyleHello(player, 1);
if catalog then
  for _, style in ipairs(catalog.styles) do
    style.name = NLG.ToUtf8(style.name):gsub(".", function(byte)
      return string.format("%02X", string.byte(byte));
    end);
  end
  catalog.name_encoding = "utf8hex";
end
```

### 备注

catalog_id is a 64-character lowercase SHA-256 hexadecimal content identifier. Names returned by this native API cross the normal Lua guest text boundary. The chatstyle RPC service must convert each name with NLG.ToUtf8, encode its bytes as uppercase hexadecimal, and add name_encoding="utf8hex" before JSON encoding. Do not send direct UTF-8 or raw guest names in JSON: the whole-payload guest text boundary and JSON escaping of Big5 backslash trail bytes can corrupt them. The client decodes the hex to UTF-8, removes name_encoding, and installs the unchanged native schema before Ready. This projection applies only to the chatstyle service; the native API does not return name_encoding. Missing catalogs report unavailable. Hello alone does not enable styled messages. Repeated Hello for the same character, connection, and catalog retains an existing ready state.
