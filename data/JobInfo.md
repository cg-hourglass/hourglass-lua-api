<!-- Generated. DO NOT EDIT. -->
# JobInfo

## Data.JobInfo(JobId)

### 函数功能

按职业 ID 查询职业的名称与所属的系。

### 参数说明

- JobId: [数值型](../appendix/数值型.md) 职业 ID。

### 返回值

找到时返回表 {id, name, ancestry}：name 为职业名称（字符串），ancestry 为该职业所属的系的 ID；职业 ID 不存在返回 nil。

## 参考实例

```lua
local j = Data.JobInfo(jobId);
if j then print(j.name, j.ancestry) end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。只读，不修改任何数据。
`Data.SkillInfo` 的 cost 按 ancestry 计算，需要给某个职业算技能栏占用时可以用本函数先确认职业存在。
