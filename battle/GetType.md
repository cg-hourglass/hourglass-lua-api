<!-- Generated. DO NOT EDIT. -->
# GetType

## Battle.GetType(BattleIndex)

### 函数功能

获取战斗类型，如普通战、PVP 战等。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

战斗类型，参照战斗类型常量；战斗index非法返回 -1。

## 参考实例

```lua
if Battle.GetType(TM_BattleIndex) == %战斗_PVP% then
    print("pvp battle");
end
```

### 备注

可用的战斗类型常量：%战斗_普通%（1）、%战斗_PVP%（2）、%战斗_观战%（3）、%战斗_BOSS战%（5）。

实际取值还有 0（无）、4（停泊地）、6（最终 BOSS）、7（DP 战）四个，
常量表中没有对应常量，写判断时请留默认分支。
