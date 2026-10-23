<!-- Generated. DO NOT EDIT. -->
# HmacSha256Hex

## Crypto.HmacSha256Hex(Key, Message)

### 函数功能

计算 HMAC-SHA256，返回小写十六进制串。

### 参数说明

- Key: [字符串](../appendix/字符串.md) 密钥，按原始字节处理。
- Message: [字符串](../appendix/字符串.md) 消息，按原始字节处理。

### 返回值

64 个字符的小写十六进制字符串。

## 参考实例

```lua
local tag = Crypto.HmacSha256Hex(secret, round .. ":" .. seed);
```

### 备注

任一参数不是字符串时抛出参数错误。
