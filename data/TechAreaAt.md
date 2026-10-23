<!-- Generated. DO NOT EDIT. -->
# TechAreaAt

## Data.TechAreaAt(SkillId, Floor, X, Y)

### 函数功能

查询某项技能在某个格子上可采集的区域（techarea）。

### 参数说明

- SkillId: [数值型](../appendix/数值型.md) 技能 ID。
- Floor: [数值型](../appendix/数值型.md) 楼层（地图 ID）。
- X: [数值型](../appendix/数值型.md) 格子的 X 坐标。
- Y: [数值型](../appendix/数值型.md) 格子的 Y 坐标。

### 返回值

返回数组，每个元素是一个覆盖该格子的区域，按 techarea 表顺序排列；没有区域时返回空表 `{}`（不是 nil）。区域字段：`id` techarea 表的 id 列；`skill` 技能 ID；`name` 区域名称；`floor` 楼层；`x1`、`y1`、`x2`、`y2` 区域的矩形范围；`zorder` 叠放顺序；`failed` 基础采集失败概率；`need_item` 需要持有的道具 ID（大于 0 时，玩家背包里没有这个道具就不会从该区域采到物品）；`items` 区域内可采到的物品数组，每项 `{id, name, prob, level}`（物品 ID、名称、权重、物品等级），与实际采集一样，不在物品表里、物品等级不大于 0 或权重不大于 0 的物品会被略过（这些物品永远采不到）。

## 参考实例

```lua
local areas = Data.TechAreaAt(skillId, floor, x, y);
for _, a in ipairs(areas) do
  print(a.name, a.failed, #a.items);
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。只读，不修改任何数据。
查询用的是采集技能同一个查找函数和同样的 16 个区域上限，且只查普通地图（mapId 为 0），不含迷宫类地图。zorder 小于 0 的区域不参与采集，也不会返回。
一个格子可能被多个区域覆盖；实际采集时服务端取所有覆盖区域中符合条件的候选物品的并集来抽取，脚本估算某格能采到什么时也应按并集处理，而不是只看第一个区域。
`id` 只在当前这台服务器、当前这个进程里有意义：它是各部署自己的 techarea 表编号，不同服务器之间不一致。不要把它写进共享的配置、meta 或协议里，需要记录地点时记录楼层与坐标。
