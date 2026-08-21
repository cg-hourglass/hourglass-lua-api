<!-- Generated. DO NOT EDIT. -->
# AddPet

## Char.AddPet(CharIndex, PetID)

### 函数功能

按敌人模板 ID 为对象制作一只 1 级宠物并加入宠物栏，成长档随机。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- PetID: [数值型](../appendix/数值型.md) 宠物 ID，对应敌人模板中的编号。

### 返回值

制作成功返回新宠物的对象index；模板不存在、宠物栏已满、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Pet = Char.AddPet(Player, 100);
if Pet ~= -1 then
    Char.SetData(Pet, %对象_名字%, "小跟班");
end
```

### 备注

成长档走普通随机；要制作满档宠物请用 Char.GivePet 并把 FullBP 传 1。
对象指针无效时会在服务端日志留下一条记录。
