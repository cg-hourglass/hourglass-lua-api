<!-- Generated. DO NOT EDIT. -->
# TradePet

## Pet.TradePet(FromCharIndex, TargetCharIndex, PetSlot)

### 函数功能

把玩家指定宠物栏位上的宠物转移给另一个玩家。

### 参数说明

- FromCharIndex: [数值型](../appendix/数值型.md) 转出方玩家的对象index。
- TargetCharIndex: [数值型](../appendix/数值型.md) 接收方玩家的对象index。
- PetSlot: [数值型](../appendix/数值型.md) 转出方宠物栏位置，取值 0-4。

### 返回值

成功返回宠物在接收方宠物栏中的位置（0-4）；失败返回负数，含义见备注。

## 参考实例

```lua
local TM_Slot = Pet.TradePet(_from, _to, 0);
if TM_Slot >= 0 then
    print("宠物已转移到对方第 " .. TM_Slot .. " 号栏位");
end
```

### 备注

失败码：

- `-1`：参数错误——任一对象不是玩家、PetSlot 越界，或该栏位上没有宠物
- `-2`：该宠物的主人指针并不指向 FromCharIndex（不是真正的拥有者）
- `-3`：接收方宠物栏已满
- `-4`：等级不符（宠物等级比接收方等级高 5 级以上）

“身上位置无宠物”这种情况由前置参数校验拦下，返回 -1；-2 专门表示主人指针不匹配。

另外，成功时**返回值可能是 0**（接收方第一个栏位），所以判定成功要用 `>= 0`，
不要用“正数表示成功”来判断。

转移过程会处理散步宠物与骑乘状态的复位、重新分配宠物序号、改写主人 CDKey 与名字，
并把宠物状态重置为休息，同时给双方下发宠物栏封包。
