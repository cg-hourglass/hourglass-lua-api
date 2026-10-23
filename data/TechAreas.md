<!-- Generated. DO NOT EDIT. -->
# TechAreas

## Data.TechAreas(SkillId, MapId, Floor)

### 函数功能

查询某项技能在指定地图楼层的全部采集区域。

### 参数说明

- SkillId: [数值型](../appendix/数值型.md) 技能 ID，伐木 225、采矿 227、打猎 226。
- MapId: [数值型](../appendix/数值型.md) 地图类型，0 为固定地图、1 为随机迷宫。
- Floor: [数值型](../appendix/数值型.md) 地图编号。

### 返回值

返回数组，区域与物品字段同 Data.TechAreaAt；没有匹配区域时返回空表。

## 参考实例

```lua
local areas = Data.TechAreas(225, 0, 1000);
for _, a in ipairs(areas) do
  print(a.x1, a.y1, a.x2, a.y2, #a.items);
end
```

### 备注

只读查询本机当前有效区域，按采集区域表顺序排列；zorder 小于 0 的区域不返回，不受单格查询的 16 个重叠区域上限限制。
查询目录不代表角色当前具备采集等级、道具或采集条件，也不保证区域中心可达。
区域 id 仅在当前服务器进程内有意义，不可写入共享配置或协议；需要记录地点时使用地图类型、地图编号及坐标。
