<!-- Generated. DO NOT EDIT. -->
# UpPet

## Pet.UpPet(PlayerIndex, PetIndex)

### 函数功能

结算宠物所有待处理的升级，并把宠物的最新状态封包发给客户端。

### 参数说明

- PlayerIndex: [数值型](../appendix/数值型.md) 宠物拥有者的对象index，必须是玩家。
- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index，必须是 PlayerIndex 名下的宠物。

### 返回值

正常返回 0；宠物不在该玩家的宠物栏中返回 -1；第一个参数不是玩家或宠物对象无效时返回 0。

## 参考实例

```lua
Char.SetData(_pet, %对象_经验%, 100000);
Pet.UpPet(_player, _pet); -- 结算升级并刷新客户端显示
```

### 备注

内部会按当前经验循环执行升级检查，每升一级都会追加成长与 AI 忠诚度变化，
随后重算战斗参数并依次下发升级、KP、KP2 与宠物技能封包。

本函数稳定返回 0，并非无返回值。
