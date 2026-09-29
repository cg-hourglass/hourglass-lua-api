<!-- Generated. DO NOT EDIT. -->
# RegFpConsumeEvent

## NL.RegFpConsumeEvent(Dofile, FuncName)

### 函数功能

注册消耗魔力值（FP）时触发的 Lua 函数，可以改写消耗量。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## FpConsumeEventCallBack(CharIndex, SkillId, Extra, FpCost, InBattle)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 消耗魔力的对象index；调用方没有角色上下文时传入 -1。由引擎传入。
- SkillId: [数值型](../appendix/数值型.md) 造成本次消耗的技能（Skill）ID，由引擎传入。
- Extra: [数值型](../appendix/数值型.md) 辅助信息，多数情况下是造成消耗的 tech ID；部分生产类调用点在这里传的是道具index。由引擎传入。
- FpCost: [数值型](../appendix/数值型.md) 服务器算出的魔力消耗值，由引擎传入。
- InBattle: [数值型](../appendix/数值型.md) 是否在战斗中触发。0 不在战斗中，1 在战斗中。由引擎传入。

### 返回值

返回新的魔力消耗值。不想改动就返回 FpCost（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegFpConsumeEvent(nil, "MyFpConsumeEvent");

function MyFpConsumeEvent(CharIndex, SkillId, Extra, FpCost, InBattle)
  if(InBattle == 1)then
    return 0; -- 战斗中不消耗魔力
  end
  return FpCost;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本事件是少数容忍“没有角色”的回调之一，CharIndex 可能为 -1。
Extra 多数情况下是 tech ID，但鉴定道具、刻名道具这两个生产类触发点在这个位置传的是道具index，
所以不要把它当成恒定的 tech ID 使用。
