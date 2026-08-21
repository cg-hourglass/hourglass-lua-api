<!-- Generated. DO NOT EDIT. -->
# SetMap

## Obj.SetMap(ObjectIndex, Value)

### 函数功能

设置指定 Object Index 的 Map ID。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。
- Value: [数值型](../appendix/数值型.md) 新的 Map ID。

### 返回值

设置前的旧 Map ID；Object Index 未被使用时返回 -1。

## 参考实例

```lua
local oldMap = Obj.SetMap(objIndex, 0);
```
