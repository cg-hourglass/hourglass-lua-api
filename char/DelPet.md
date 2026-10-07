<!-- Generated. DO NOT EDIT. -->
# DelPet

## Char.DelPet(CharIndex, PetID, Level, LevelSetting)

### 函数功能

删除对象身上第一只满足条件的宠物。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- PetID: [数值型](../appendix/数值型.md) 宠物 ID，对应敌人模板中的编号。
- Level: [数值型](../appendix/数值型.md) 用于比对的宠物等级。
- LevelSetting: [数值型](../appendix/数值型.md) 0 表示删除一只等级小于等于 Level 的宠物，1 表示要求等级恰好等于 Level，默认 0。 [可为空]

### 返回值

成功删除返回 0；没有匹配的宠物、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
Char.DelPet(Player, 100, 10);      -- 删掉一只 10 级以下的 100 号宠物
Char.DelPet(Player, 100, 10, 1);   -- 只删恰好 10 级的
```

### 备注

注意成功的返回值是 0 而不是 1，失败才是 -1，与同族其他函数的约定相反。
一次调用只删一只；LevelSetting 传 0 和 1 以外的值时不会匹配到任何宠物，直接返回 -1。
删除时会一并清理放牧状态与骑乘状态、写入宠物日志。
对象指针无效时会在服务端日志留下一条记录。
