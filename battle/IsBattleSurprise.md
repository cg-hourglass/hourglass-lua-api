<!-- Generated. DO NOT EDIT. -->
# IsBattleSurprise

## Battle.IsBattleSurprise(BattleIndex)

### 函数功能

判断战斗是否存在先制（偷袭）方。

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，为 Encount、PVE 或 PVP 函数的返回值。

### 返回值

2 表示上方队列（10-19 位置）先制，1 表示下方队列（0-9 位置）先制，0 表示双方都没有先制；战斗index非法也返回 0。

## 参考实例

```lua
if Battle.IsBattleSurprise(TM_BattleIndex) == 2 then
    print("被敌方偷袭");
end
```
