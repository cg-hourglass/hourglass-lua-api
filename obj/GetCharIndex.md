<!-- Generated. DO NOT EDIT. -->
# GetCharIndex

## Obj.GetCharIndex(ObjectIndex)

### 函数功能

获取指定 Object Index 关联的 Index 栏位。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。

### 返回值

该 Object 关联的 Index；具体含义随 Obj.GetType 而定（角色对象→CharIndex，
道具对象→ItemIndex，金币对象→金额 等）。Object Index 未被使用时返回 -1。

## 参考实例

```lua
local charIndex = Obj.GetCharIndex(objIndex);
```
