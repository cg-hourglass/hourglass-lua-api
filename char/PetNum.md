<!-- Generated. DO NOT EDIT. -->
# PetNum

## Char.PetNum(CharIndex)

### 函数功能

统计对象携带的宠物数量。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

宠物数量，范围 0-5；对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
if Char.PetNum(Player) >= 5 then
    NLG.TalkToCli(Player, -1, "宠物栏已满。");
end
```

### 备注

只统计五个宠物栏中指针非空的格子，不做可用性检查——已失效但指针还在的宠物也会被计入，
这点与 Char.GetPet 不同，是沿袭旧版的行为差异，刻意保留。
