<!-- Generated. DO NOT EDIT. -->
# GetFrontChar

## NLG.GetFrontChar(CharIndex, CharType)

### 函数功能

获取对象面前一格内、符合指定类型条件的所有对象数量和对象index列表。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 基准对象index，以其朝向为准，取正前方一格。
- CharType: [数值型](../appendix/数值型.md) 类型过滤条件，见下方“参数补充说明”；本版本常量表中没有对应的 %对象类型_x% 系列常量，请直接传数值。

### 返回值

返回两个值——第一个是数量，第二个是从下标1开始的 Lua table（对象index列表）。

## 参考实例

```lua
local num, playertbl = NLG.GetFrontChar(index, 0); -- 0 = 不过滤类型
NLG.SystemMessage(index, "面前有"..num.."个对象。");
for i = 1, num do
  NLG.SystemMessage(index, "对象index："..playertbl[i]);
end
```

### 备注

本版本常量表中没有对应的 %对象类型_全部/人/怪/宠/NPC% 系列常量，脚本里只能直接写数值，过滤规则如下：
CharType=0 时不过滤，返回该格上所有已注册的对象（含各类NPC）；CharType 为1/2/3 时精确匹配对象的类型（1=玩家、2=敌人、3=宠物）；CharType>=4 时只保留类型编号**小于** CharType 的对象，类型编号大于等于 CharType 的对象（多数NPC子类型编号从4起步）反而会被排除——这个分支与直觉相反（不是“取NPC”，而是“排除掉大于等于该阈值的类型”），是沿袭旧版的既有行为；CharType为负数时不匹配任何分支，恒返回空表。
单格最多收集128个，超过后会按下标截断到127个。
