<!-- Generated. DO NOT EDIT. -->
# SkillInfo

## Data.SkillInfo(SkillId, JobId)

### 函数功能

查询某个职业下某项技能的最高等级与技能栏占用。

### 参数说明

- SkillId: [数值型](../appendix/数值型.md) 技能 ID。
- JobId: [数值型](../appendix/数值型.md) 职业 ID。

### 返回值

找到时返回表 {id, name, max_lv, cost}：name 为技能名称（字符串），max_lv 为该职业在此技能上的最高等级，cost 为该职业学习此技能占用的技能栏数；技能或职业 ID 无效返回 nil。

## 参考实例

```lua
local s = Data.SkillInfo(225, jobId);
if s then print(s.name, s.max_lv, s.cost) end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。只读，不修改任何数据。

max_lv 回答的是「这个职业在这项技能上最高几级」：职业出现在该技能的职业列表里时取列表中的上限；职业存在但不在列表里时，取技能的默认最高等级（defaultmaxlevel）。它**不**回答「这个职业能不能学这项技能」，不要用它判断可学性。

cost 是学习这项技能要占用的技能栏数：启用新技能栏规则时按职业所属的系（Data.JobInfo 的 ancestry）和技能计算，否则取技能表里的固定占用值。
