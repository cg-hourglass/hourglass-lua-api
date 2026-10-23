<!-- Generated. DO NOT EDIT. -->
# GetType

## Obj.GetType(ObjectIndex)

### 函数功能

获取指定 Object Index 的 Object 类型。

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) 目标的物件 index。

### 返回值

Object 类型：

- -1：Object Index 未被使用（对象无效）
- 0：未使用
- 1：角色（含玩家/宠物/NPC/敌人，凡挂 TypeChara 的世界对象）
- 2：道具
- 3：金币
- 4：传送点
- 5：船
- 6：码头（船坞停靠点）

## 参考实例

```lua
local objType = Obj.GetType(objIndex);
if (objType == 2) then
  NLG.SystemMessage(-1, "这是一个道具对象。");
end
```
