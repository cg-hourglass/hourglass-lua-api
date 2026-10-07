<!-- Generated. DO NOT EDIT. -->
# RegAvatarExpiredEvent

## NL.RegAvatarExpiredEvent(Dofile, FuncName)

### 函数功能

注册玩家或其携带宠物的限时外观授权（tbl_avatar_grant）到期并被引擎删除后触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AvatarExpiredCallBack(CharIndex, PetIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index；宠物的授权到期时是携带该宠物的玩家。
- PetIndex: [数值型](../appendix/数值型.md) 授权到期的宠物对象index；玩家自己的授权到期时为 -1。

### 返回值

无

## 参考实例

```lua
NL.RegAvatarExpiredEvent(nil, "MyAvatarExpiredEvent");

function MyAvatarExpiredEvent(CharIndex, PetIndex)
  if PetIndex >= 0 then
    -- 宠物 PetIndex（由玩家 CharIndex 携带）的限时外观到期
  else
    -- 玩家 CharIndex 自己的限时外观到期
  end
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本服务端扩展事件，原版没有。限时授权（`NLG.AvatarGrant` 的 Expire 大于 0）由引擎负责到期：在线玩家与其携带宠物最早的到期时间记在内存里，由限时道具同一个角色巡检循环检查；到期后引擎删除该玩家或宠物所有已到期（Expire 不大于当前时间）的授权行，再触发本事件，脚本据此重新计算外观。
不在当场触发，而是在下一轮角色巡检（RunLoop）释放全局锁后触发，同一玩家（或同一只宠物）每轮最多一次；若确实没有删除任何行（例如授权已被续期或已被脚本撤销），或触发前宠物已经离开该玩家的宠物栏，则不触发。
登录时读取玩家与携带宠物的限时授权；宠物进入宠物栏（见 `NL.RegPetGainedEvent`）时读取该宠物的限时授权；`NLG.AvatarGrant` 写入限时授权时即时生效。离线期间到期的授权在登录后的第一次检查时删除并触发本事件。宠物仓库、宠物屋里的宠物不检查。
