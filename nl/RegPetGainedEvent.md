<!-- Generated. DO NOT EDIT. -->
# RegPetGainedEvent

## NL.RegPetGainedEvent(Dofile, FuncName)

### 函数功能

注册玩家得到一只新携带的宠物（捕捉、交易、摆摊购买、捡起、从银行或家族仓库取出等）后触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## PetGainedCallBack(CharIndex, PetIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 得到宠物的玩家对象index，由引擎传入。
- PetIndex: [数值型](../appendix/数值型.md) 新进入宠物栏的宠物对象index。

### 返回值

无

## 参考实例

```lua
NL.RegPetGainedEvent(nil, "MyPetGainedEvent");

function MyPetGainedEvent(CharIndex, PetIndex)
  -- 宠物 PetIndex 刚进入玩家 CharIndex 的宠物栏
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本服务端扩展事件，原版没有。触发时机：宠物从玩家宠物栏之外进入宠物栏，包括战斗捕捉、`Char.AddPet` / `Char.GivePet`、GM 造宠、NPC 事件或登录钩子发放的宠物、玩家交易与脚本交易（`Pet.TradePet`）、摆摊/集市购买、从地上捡起（含宠物邮件送回的宠物）、从银行或家族仓库取出、GM 指令把仓库宠物换进宠物栏。
不在当场触发，而是在下一轮角色巡检（RunLoop）释放全局锁后触发，同一玩家的同一只宠物每轮最多一次；若触发前宠物已经离开该玩家的宠物栏（例如同一轮内又被交易走），则不触发。
宠物在自己的宠物栏之间换位、登录读档、存档恢复都不会触发；失去宠物的一方也不会触发。
