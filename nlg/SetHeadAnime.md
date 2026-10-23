<!-- Generated. DO NOT EDIT. -->
# SetHeadAnime

## NLG.SetHeadAnime(CharIndex, AnimeId)

### 函数功能

使用扩展 Anime 显示玩家的地图头顶状态方块。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象 index；不支持 NPC 或宠物。
- AnimeId: [数值型](../appendix/数值型.md) 已导入客户端资源的 A-EXT Anime ID，范围 200000..2147483647；0 清除。

### 返回值

成功返回 0，目标或 AnimeId 无效返回 -1。

## 参考实例

```lua
NLG.SetHeadAnime(playerIndex, 536871168);
-- Clear when the activity ends.
NLG.SetHeadAnime(playerIndex, 0);
```

### 备注

需要支持扩展头顶动画的客户端和相应 Anime 资源；仅负责显示，不启动技能或改变玩法。
沿用 CHAR_ACTSKILL 和 SkillUse（Char.GetData 的 8111），同步本人和附近玩家，并在视野重入时重发。
与 SetHeadIcon 共用同一槽位，不叠加。脚本必须管理开始/结束与断线清理；清理前应检查 8111 仍为自己设置的值，避免清除其他技能。
原生战斗/观战/摆摊等状态保留原来的显示优先级；客户端缺少资源时隐藏，不替换成其他角色图像。
不支持未升级的原版客户端：旧客户端会把大 ID 当数组下标；发布时必须同步升级客户端。
