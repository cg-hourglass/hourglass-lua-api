<!-- Generated. DO NOT EDIT. -->
# GivePet

## Char.GivePet(CharIndex, PetID, FullBP)

### 函数功能

按敌人模板 ID 为对象制作一只 1 级宠物，可指定是否满档。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- PetID: [数值型](../appendix/数值型.md) 宠物 ID，对应敌人模板中的编号。
- FullBP: [数值型](../appendix/数值型.md) 1 表示按模板制作满档宠物，0 或省略表示档数随机。 [可为空]

### 返回值

制作成功返回新宠物的对象index；模板不存在、宠物栏已满、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
Char.GivePet(Player, 100);      -- 档数随机
Char.GivePet(Player, 100, 1);   -- 满档
```

### 备注

与 Char.AddPet 的唯一区别就是成长档的掷点方式；FullBP 省略时两者行为一致。
对象指针无效时会在服务端日志留下一条记录。
