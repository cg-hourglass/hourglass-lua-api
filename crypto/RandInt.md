<!-- Generated. DO NOT EDIT. -->
# RandInt

## Crypto.RandInt(Min, Max)

### 函数功能

从系统密码学随机源取一个闭区间内的均匀随机整数。

### 参数说明

- Min: [数值型](../appendix/数值型.md) 下界（含），必须是绝对值不超过 2^53 的整数。
- Max: [数值型](../appendix/数值型.md) 上界（含），必须是绝对值不超过 2^53 的整数，且不小于 Min。

### 返回值

区间 [Min, Max] 内的随机整数，各值概率相同、无取模偏差。

## 参考实例

```lua
local roll = Crypto.RandInt(1, 6);
```

### 备注

与 NLG.Rand 不同，结果不可预测，涉及奖励结算的抽取应使用本函数。
参数不是整数（含小数、NaN、无穷、字符串）、超出 ±2^53 或 Min 大于 Max 时抛出参数错误。
