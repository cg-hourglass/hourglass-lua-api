<!-- Generated. DO NOT EDIT. -->
# SetType

## Obj.SetType(ObjectIndex, Value)

### 函数功能

设置指定 Object Index 的 Object 类型。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。
- Value: [数值型](../appendix/数值型.md) 新的 Object 类型，取值 0~6：

- 0：未使用
- 1：角色
- 2：道具
- 3：金币
- 4：传送点
- 5：船
- 6：码头（船坞停靠点）

### 返回值

设置前的旧类型值；Object Index 未被使用时返回 -1。写入不做取值范围校验。

## 参考实例

```lua
local oldType = Obj.SetType(objIndex, 0);
```
