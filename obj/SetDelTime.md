<!-- Generated. DO NOT EDIT. -->
# SetDelTime

## Obj.SetDelTime(ObjectIndex, Value)

### 函数功能

设置指定 Object 的删除时间。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。
- Value: [数值型](../appendix/数值型.md) 新的删除时间 timestamp。

### 返回值

设置前的旧删除时间；Object Index 未被使用时返回 -1。

## 参考实例

```lua
local oldDelTime = Obj.SetDelTime(objIndex, 0);
```
