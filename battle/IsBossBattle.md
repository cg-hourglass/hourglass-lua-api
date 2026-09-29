<!-- Generated. DO NOT EDIT. -->
# IsBossBattle

## Battle.IsBossBattle(BattleIndex)

### 函数功能

判断战斗是否是 BOSS 战。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

1 是 BOSS 战，0 不是；战斗index非法也返回 0。

## 参考实例

```lua
if Battle.IsBossBattle(TM_BattleIndex) == 1 then
    print("boss battle");
end
```

### 备注

与其他取值函数不同，本函数在战斗index非法时静默返回 0，不返回 -1，也不打印错误日志。
