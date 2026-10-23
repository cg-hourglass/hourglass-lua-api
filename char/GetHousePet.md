<!-- Generated. DO NOT EDIT. -->
# GetHousePet

## Char.GetHousePet(CharIndex, Slot)

### 函数功能

获取玩家出租屋中指定位置的宠物对象index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 出租屋宠物栏位置，本版本范围 0-4。

### 返回值

该位置宠物的对象index；位置为空、位置越界、宠物已失效、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Pet = Char.GetHousePet(Player, 0);
```

### 备注

位置上限本版本是 5，即 0-4。
本函数失败时写进服务端日志的文案沿袭旧版，用的是银行宠物栏那一支的措辞，
排查时请以实际调用的函数为准，不要以为是银行那一支出了问题。
