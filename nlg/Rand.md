<!-- Generated. DO NOT EDIT. -->
# Rand

## NLG.Rand(min, max)

### 函数功能

生成一个指定范围内（含两端）的随机整数，使用服务器自身的随机数源。

### 参数说明

- min: [数值型](../appendix/数值型.md) 随机数下限（含）。
- max: [数值型](../appendix/数值型.md) 随机数上限（含）。

### 返回值

[min, max] 闭区间内的一个随机整数。

## 参考实例

```lua
local dmg = NLG.Rand(1, 100);
```
