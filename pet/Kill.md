<!-- Generated. DO NOT EDIT. -->
# Kill

## Pet.Kill(PlayerIndex, PetIndex)

### 函数功能

从指定玩家身上删除指定宠物，宠物对象随之销毁。

### 参数说明

- PlayerIndex: [数值型](../appendix/数值型.md) 宠物拥有者的对象index，必须是玩家。
- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index。

### 返回值

成功返回 1；目标不是宠物、拥有者不是玩家，或该宠物不在拥有者的宠物栏中时返回 0。

## 参考实例

```lua
if Pet.Kill(_player, _pet) == 1 then
    print("宠物已删除");
end
```

### 备注

执行顺序：写一条宠物日志（含 CDKey、宠物名、等级与坐标）→ 清空宠物栏槽位 →
若该宠物是散步宠物则复位散步状态并向周围广播 → 下发宠物状态 KP 封包 → 释放宠物对象槽。

本操作不可撤销，且会立即销毁宠物对象；调用之后不要再用原来的 PetIndex 访问该宠物。
