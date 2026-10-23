<!-- Generated. DO NOT EDIT. -->
# SetX

## Obj.SetX(ObjectIndex, Value)

### 函数功能

设置指定 Object Index 的 X 坐标。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。
- Value: [数值型](../appendix/数值型.md) 新的 X 坐标。

### 返回值

设置前的旧 X 坐标；Object Index 未被使用时返回 -1。

## 参考实例

```lua
local oldX = Obj.SetX(objIndex, 100);
```
