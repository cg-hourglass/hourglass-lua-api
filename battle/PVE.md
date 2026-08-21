<!-- Generated. DO NOT EDIT. -->
# PVE

## Battle.PVE(CharIndex, CreatePtr, DoFunc, EnemyIdAr, BaseLevelAr, Flg)

### 函数功能

用 Lua 脚本直接创建一场对怪物的战斗，战斗初始化完成后可回调指定的 Lua 函数。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 遇敌玩家的对象index。
- CreatePtr: [数值型](../appendix/数值型.md) 触发战斗的对象index（战斗的 create 方，通常为 NPC）。
- DoFunc: [字符串](../appendix/字符串.md) 战斗初始化完成后调用的 Lua 全局函数名，声明格式见下方 BattleInitCallBack；不需要回调时传 nil。 [可为空]
- EnemyIdAr: [数值型](../appendix/数值型.md)[数组] 战斗中出现的怪物 ID 数组（enemy.txt 中的 ID），最多取前 10 个。该参数必须是 table。
- BaseLevelAr: [数值型](../appendix/数值型.md)[数组] 与 EnemyIdAr 一一对应的怪物等级数组，最多取前 10 个；传入非 table（如 nil）时全部怪物基础等级按 0 处理。 [可为空]
- Flg: [数值型](../appendix/数值型.md) 战斗类型标志，可省略。当前实现接收后未使用。 [可为空]

### 返回值

成功返回战斗index；失败返回负数（-1 战斗槽分配失败、-6 对象index无效、-9 对象已在战斗中）。第 4 个参数不是 table 时直接返回 -1。

## BattleInitCallBack(BattleIndex)

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 新建战斗的战斗index，由引擎传入。

### 返回值

返回一个大于 0 的战斗类型值可覆盖发给客户端的战斗类型；返回 0（或不返回）保持默认类型。

## 参考实例

```lua
local TM_EnemyIdAr = {11, 11, 11, 11, 11};
local TM_BaseLevel = {200, 200, 0, 0, 100};
-- 调用后玩家 TM_PlayPtr 将与 2 只 200 级、2 只 1 级和 1 只 100 级的穴熊对战
Battle.PVE(TM_PlayPtr, TM_NpcPtr, nil, TM_EnemyIdAr, TM_BaseLevel);

-- 带初始化回调
function MyBattleInit(TM_BattleIndex)
    Battle.SetNoRisk(TM_BattleIndex, 1);
    return 0;
end
Battle.PVE(TM_PlayPtr, TM_NpcPtr, "MyBattleInit", TM_EnemyIdAr, TM_BaseLevel, 0);
```

### 备注

本函数至少需要 5 个参数，DoFunc 与 BaseLevelAr 即使不使用也必须占位（传 nil）。

DoFunc 按名字在调用时刻解析全局表：解析不到或 pcall 失败只记录日志，战斗照常继续。

**本版本已知行为**：战斗槽已经分配之后再失败（造怪失败、入场失败等），引擎会拆掉战斗但仍然
返回那个已经作废的战斗index，因此返回值为非负数并不等于战斗一定成功创建。
判断战斗是否真的存在，请再用 Battle.IsUsing 确认。
