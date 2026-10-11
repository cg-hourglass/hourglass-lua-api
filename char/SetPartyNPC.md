<!-- Generated. DO NOT EDIT. -->
# SetPartyNPC

## Char.SetPartyNPC(CharIndex, Mode)

### 函数功能

把 NPC 设为可组队的随行 NPC。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Mode: [数值型](../appendix/数值型.md) 组队模式，0 为禁止组队，1 为可以组队。

### 返回值

设置后的组队模式，也就是传入的 Mode；对象类型排在敌人之下（玩家、宠物等）或指针无效时返回 -1。

## 参考实例

```lua
Char.SetPartyNPC(NpcIndex, 1);
```

### 备注

调用后会把对象的类型翻成可组队 NPC 并向周围广播新的外观数据，这个类型翻转不会因为 Mode 传 0 而回退。
组队标记只有 NPC 类型的对象才有存储位置；对敌人或宠物类型仍会执行类型翻转，
但标记无处保存，函数照样把 Mode 原样返回。
