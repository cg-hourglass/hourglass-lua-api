<!-- Generated. DO NOT EDIT. -->
# LevelExpAt

## Char.LevelExpAt(CharIndex, Level)

### 函数功能

获取任意等级对应的累计经验门槛。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index；事件回调按这个对象来加工门槛。
- Level: [数值型](../appendix/数值型.md) 要查询的等级。

### 返回值

达到该等级所需的累计经验值；对象指针无效，或等级非法、超出经验表范围时返回 -1。

## 参考实例

```lua
local lv = Char.GetData(Player, %对象_等级%);
local toNext = Char.LevelExpAt(Player, lv + 1) - Char.LevelExpAt(Player, lv);
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。只读。
`Char.LevelExpAt(ci, 当前等级)` 与 `Char.LevelExp(ci)` 相等。和 `Char.LevelExp` 一样，结果会经过 NL.RegGetNextLevelExpEvent 的加工，回调收到的 Level 就是本函数的 Level 参数。
对象指针无效时会在服务端日志留下一条记录。
