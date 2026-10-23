<!-- Generated. DO NOT EDIT. -->
# Sha256Hex

## Crypto.Sha256Hex(Text)

### 函数功能

计算字符串原始字节的 SHA-256，返回小写十六进制串。

### 参数说明

- Text: [字符串](../appendix/字符串.md) 待哈希的字符串，按原始字节处理，不做任何编码转换，可含 \0 与繁体字节。

### 返回值

64 个字符的小写十六进制字符串。

## 参考实例

```lua
local commit = Crypto.Sha256Hex(seed .. "|" .. result);
```

### 备注

参数不是字符串（数字不会被自动转换）时抛出参数错误。
