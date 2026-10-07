<!-- Generated. DO NOT EDIT. -->
# TechInfo

## Data.TechInfo(TechId)

### 函数功能

按 tech id 查询技能（tech.txt）条目的基本信息。

### 参数说明

- TechId: [数值型](../appendix/数值型.md) tech id，即 tech.txt 中定义的 id。

### 返回值

找到时返回表 {id, skill, name, fp, need_lv, target, func}：skill 为所属技能 ID，name 为 tech 名称（字符串），fp 为消耗的 FP，need_lv 为所需技能等级，target 为目标标志（0x08 自身、0x10 己方、0x20 敌方，范围位 0x40/0x80/0x100/0x200），func 为路由函数名（例如 "TECH_Lumb"）；tech id 不存在返回 nil。

## 参考实例

```lua
local t = Data.TechInfo(9609);
if t then print(t.name, t.func, t.need_lv) end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。只读，不修改任何数据。
