<!-- Generated. DO NOT EDIT. -->
# GetBattleMode

## Battle.GetBattleMode(CharIndex)

### 函数功能

获取对象当前的战斗状态。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 对象index。

### 返回值

战斗状态常量；对象无效返回 -1。

## 参考实例

```lua
if Battle.GetBattleMode(index) == %战斗状态_结束% then
    Battle.FinishPlayerBattle(index); -- 战斗结束，让对象脱离战斗
end
```

### 备注

战斗状态常量：

- %战斗状态_无%（0）
- %战斗状态_初始化%（1）
- %战斗状态_命令等待%（2）
- %战斗状态_命令执行%（3）
- %战斗状态_战斗%（4）
- %战斗状态_死亡%（5）
- %战斗状态_结束%（6）

本函数直接读取对象身上的状态字段，**不校验对象是否真的在一场有效战斗里**，
因此拿到非 %战斗状态_无% 的值并不保证 Battle.GetCurrentBattle 也能成功。

实际取值还有 7-10 四个（BOSS、观战初始化、骑乘、结束），常量表中没有对应常量。
因此逐一对比上述 7 个常量并不能穷尽所有返回值，写判断时请留默认分支。
