<!-- Generated. DO NOT EDIT. -->
# GetString

## NLG.GetString(String, Token, Pos)

### 函数功能

以给定分隔符集合切分字符串，取切分结果里第Pos个（从0开始）token。

### 参数说明

- String: [字符串](../appendix/字符串.md) 要切分的字符串。
- Token: [字符串](../appendix/字符串.md) 分隔符字符集合（不是固定分隔串），比如"|"或"-|"；集合内任意一个字符都会被当作分隔符。
- Pos: [数值型](../appendix/数值型.md) 要取第几个切分结果，从0开始计数。

### 返回值

第Pos个切分结果；Pos为负数、Token集合里的任一字符从未在String里出现过（子串检测失败）、或Pos超出实际切分出的token数量时都返回 nil。

## 参考实例

```lua
local s = NLG.GetString("a|b|c|d", "|", 1); -- 返回 "b"
```

### 备注

有两个容易踩坑的地方：其一，切分之前会先做一次 `String 是否包含 Token 这个子串` 的前置检测（不是逐字符检测），例如 GetString("a-b", "-|", 0) 因为 "a-b" 不包含子串"-|"而直接返回 nil，即使 "-" 本身是分隔符集合里的一个字符；其二，连续多个分隔符会被合并成一个分隔，字符串开头的分隔符会被跳过，因此永远不会切出空字符串token（这是沿袭旧版标准切分函数的语义）。
Token 为空字符串时不做特殊处理：等价于把整个String当成一个token（Pos=0返回整个字符串，其余Pos返回nil），与旧版行为一致。
