<!-- Generated. DO NOT EDIT. -->
# GetUseFpByTechId

## Battle.GetUseFpByTechId(CharIndex, TechId)

### 函数功能

查询指定对象施放某个战斗技能所需的 FP 消耗。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index，可以是玩家或宠物。
- TechId: [数值型](../appendix/数值型.md) 技能 ID，即 tech.txt 中定义的 tech id。

### 返回值

该对象施放该技能所需的 FP 值；对象无效返回 -1。

## 参考实例

```lua
local TM_Fp = Battle.GetUseFpByTechId(TM_CharIndex, 9609);
if TM_Fp >= 0 and Char.GetData(TM_CharIndex, %对象_魔%) >= TM_Fp then
    Battle.UseTechById(TM_CharIndex, 9609, 11);
end
```

### 备注

FP 消耗与对象自身状态相关（同一技能对不同对象可能给出不同结果），因此必须传入对象index而
不能只按技能查表。
