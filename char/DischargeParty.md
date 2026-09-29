<!-- Generated. DO NOT EDIT. -->
# DischargeParty

## Char.DischargeParty(CharIndex)

### 函数功能

解散对象所在的队伍。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

布尔型，成功为 true，失败为 false；对象不可用时返回数值 -1。

## 参考实例

```lua
Char.DischargeParty(Player);
```

### 备注

本函数返回的是 Lua 布尔值，不是 1/0 数值，只有指针守卫失败那一支返回的才是数值 -1。
判断时请用 `if Char.DischargeParty(Player) then` 而不是与 1 比较。
NLG 命名空间下挂着同名同实现的函数，两者完全等价。
