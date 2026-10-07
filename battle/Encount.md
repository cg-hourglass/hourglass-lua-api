<!-- Generated. DO NOT EDIT. -->
# Encount

## Battle.Encount(NpcIndex, CharIndex, Data)

### 函数功能

触发一场遇敌战斗；两参数形式为原地遇敌，三参数形式把 NPC 重新初始化为立敌（stand enemy）后发起战斗。

### 参数说明

- NpcIndex: [数值型](../appendix/数值型.md) 触发战斗一方的对象index，通常为 NPC。两参数形式下该对象只做有效性检查，不参与战斗构建。
- CharIndex: [数值型](../appendix/数值型.md) 遇敌玩家的对象index，战斗为该对象创建。
- Data: [字符串](../appendix/字符串.md) 立敌事件字符串，包含敌人队列等信息，格式等同于 GMSV 自身脚本的 encount 参数。省略时走原地遇敌。 [可为空]

### 返回值

成功返回该玩家的战斗index（即 CharIndex 的 BattleIndex）；失败返回 -1。

## 参考实例

```lua
-- 三参数：把 NPC 重新初始化为立敌并发起战斗
Battle.Encount(_NPC, _Player, "3|0,20003,43,7||0|||||0|10007|||||||||");

-- 两参数：让 _Player 在当前位置原地遇敌
Battle.Encount(_Player, _Player);
```

### 备注

参数顺序：第一个参数是 NPC（触发方），第二个参数是玩家。

两参数形式内部固定对第二个参数所指对象发起原地遇敌，第一个参数除有效性检查外不被使用；
因此“两个参数传同一个对象”与“传不同对象”的结果相同。当前位置不可遇敌时返回 -1。

三参数形式依赖立敌接缝是否已配置；若服务器未接线该接缝，会记录一条日志并返回 -1。
