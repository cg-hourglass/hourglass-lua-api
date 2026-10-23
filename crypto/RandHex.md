<!-- Generated. DO NOT EDIT. -->
# RandHex

## Crypto.RandHex(NBytes)

### 函数功能

取指定字节数的密码学随机数据，返回其小写十六进制串。

### 参数说明

- NBytes: [数值型](../appendix/数值型.md) 随机字节数，取值 1~64。

### 返回值

长度为 NBytes×2 的小写十六进制字符串。

## 参考实例

```lua
local seed = Crypto.RandHex(32);
```

### 备注

NBytes 不是 1~64 的整数时抛出参数错误。
