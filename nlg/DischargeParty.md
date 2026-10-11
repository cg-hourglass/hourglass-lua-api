<!-- Generated. DO NOT EDIT. -->
# DischargeParty

## NLG.DischargeParty(CharIndex)

### 函数功能

解散指定对象所在的队伍。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。

### 返回值

布尔型，成功为 true，失败为 false；对象不可用时返回数值 -1。

## 参考实例

```lua
NLG.DischargeParty(_MeIndex);
```

### 备注

本函数返回的是 Lua 布尔值，不是 1/0 数值，只有指针守卫失败那一支返回的才是数值 -1；判断请用 `if NLG.DischargeParty(idx) then`，不要与数值 1 比较。
本函数与 Char.DischargeParty 是同一个实现，两处语义完全一致。
