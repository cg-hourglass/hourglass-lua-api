<!-- Generated. DO NOT EDIT. -->
# GetDelTime

## Obj.GetDelTime(ObjectIndex)

### 函数功能

获取指定 Object 的删除时间。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。

### 返回值

删除时间的 timestamp；Object Index 未被使用时返回 -1。

## 参考实例

```lua
local delTime = Obj.GetDelTime(objIndex);
```
