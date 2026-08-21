<!-- Generated. DO NOT EDIT. -->
# FinishPlayerBattle

## Battle.FinishPlayerBattle(CharIndex)

### 函数功能

让角色直接脱离当前战斗并结束战斗流程。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index。

### 返回值

对象有效返回 1，对象无效返回 0。

## 参考实例

```lua
if Battle.GetBattleMode(index) == %战斗状态_结束% then
    Battle.FinishPlayerBattle(index); -- 战斗结束，让对象脱离战斗
end
```

### 备注

返回值只反映对象index是否有效，不反映脱战是否真正完成——引擎内部的脱战结果被忽略。
常用于离线挂机角色在 %战斗状态_结束% 后主动收尾。
