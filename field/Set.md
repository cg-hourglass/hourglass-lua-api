<!-- Generated. DO NOT EDIT. -->
# Set

## Field.Set(CharIndex, Field, Value)

### 函数功能

设置指定 Field 的值；名称首字符前缀规则与 Field.Get 相同。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的[对象index](../appendix/对象index.md)，仅玩家对象有效；当 Field 以 "@" 开头时该参数被忽略。
- Field: [字符串](../appendix/字符串.md) 数据栏名称，可带 "#" 或 "@" 前缀，详见[说明](guide.md)。
- Value: [字符串](../appendix/字符串.md) 要写入的值；传 nil 等价于写入空字符串，即清空该 Field 的值（键本身仍保留，之后还能再次匹配到）。 [可为空]

### 返回值

当前该层已登记的 Field 数量（是一个数值，不是布尔值）；Field 名为空、或 CharIndex 不是可用的玩家对象时返回 -1。三层各自的容量上限：@层128、#层与裸层各192；超出上限后对新名字的 Set 会静默失败，仍返回当前登记数量不变。

## 参考实例

```lua
Field.Set(chrPtr1, "LOCALVAR1", "100");
```

### 备注

- Set 返回该层当前的注册计数（一个数值）；失败时返回 -1，调用方应通过返回值是否为 -1 判断成败，而不是假设没有返回值。
- 本版本对已存在的名字 Set 是原地覆盖；对不存在的新名字总是追加新槽位（不会复用曾经被清空的旧槽位），直到该层的容量上限。
