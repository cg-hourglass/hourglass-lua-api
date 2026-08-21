<!-- Generated. DO NOT EDIT. -->
# LevelUp

## Pet.LevelUp(PlayerIndex, PetSlot)

### 函数功能

让玩家指定宠物栏位上的宠物提升 1 级。

### 参数说明

- PlayerIndex: [数值型](../appendix/数值型.md) 目标玩家的对象index。
- PetSlot: [数值型](../appendix/数值型.md) 宠物栏位置，取值 0-4。

### 返回值

true 表示成功，false 表示失败（对象不是玩家、PetSlot 越界，或该栏位上不是可用宠物）。

## 参考实例

```lua
if Pet.LevelUp(_player, 0) then
    print("宠物升了一级");
end
```

### 备注

返回值是 Lua 的[布尔型](../appendix/布尔型.md)（true/false），不是 0/1，不要用 `== 1` 判断。

升级后会追加一次 AI 忠诚度成长（+500），下发升级封包并重算战斗参数。

本函数按宠物栏位置直接取宠物，不做主人反向指针校验。
