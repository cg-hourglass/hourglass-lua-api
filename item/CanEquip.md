<!-- Generated. DO NOT EDIT. -->
# CanEquip

## Item.CanEquip(CharIndex, ItemIndex)

### 函数功能

查询角色能把一件道具装备在哪些装备栏（只读，不发任何提示）。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 角色的对象index。
- ItemIndex: [数值型](../appendix/数值型.md) 道具index。

### 返回值

两个值：栏位掩码和原因。掩码的第 i 位为 1 表示可以装在装备栏 i（0-7）；
掩码为 0 时，原因是 `"job"`（职业不符）、`"level"`（等级不足）或 `"weapon"`（道具本身不能装备，例如未鉴定），
道具不属于任何装备栏时原因是空字符串。可以装备时原因是空字符串。对象或道具无效时返回 0 和空字符串。

## 参考实例

```lua
local mask, why = Item.CanEquip(player, item);
if mask == 0 then
    print("cannot equip: " .. why);
elseif bit32.band(mask, 1) ~= 0 then
    -- 可以装在 0 号装备栏
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
判断与手动换装时的装备检查相同，但不考虑目标栏是否已有装备，也不考虑双手武器与盾牌之类的搭配。
