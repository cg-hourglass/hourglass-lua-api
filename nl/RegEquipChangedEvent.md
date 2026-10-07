<!-- Generated. DO NOT EDIT. -->
# RegEquipChangedEvent

## NL.RegEquipChangedEvent(Dofile, FuncName)

### 函数功能

注册玩家或其宠物的装备发生变化（穿上、卸下、互换、丢弃、限时到期、战斗损坏、被脚本删除）后触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## EquipChangedCallBack(CharIndex, PetIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家对象index；宠物装备变化时是该宠物的主人，由引擎传入。
- PetIndex: [数值型](../appendix/数值型.md) 装备变化的宠物对象index；玩家自己的装备变化时为 -1。

### 返回值

无

## 参考实例

```lua
NL.RegEquipChangedEvent(nil, "MyEquipChangedEvent");

function MyEquipChangedEvent(CharIndex, PetIndex)
  if PetIndex == -1 then
    -- 玩家自己的装备变了，此时属性已经按新装备重算
  else
    -- 玩家携带的宠物 PetIndex 的装备变了
  end
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本服务端扩展事件，原版没有。触发时机：玩家把道具移入、移出装备栏或在装备栏之间互换（包括「使用」道具直接穿上，以及战斗中换装备）；从装备栏丢弃道具；宠物装备的穿上、卸下、在宠物之间移动以及从宠物身上丢弃；装备栏里的限时道具到期消失（玩家与宠物都算）；装备在战斗中耐久归零损坏消失（玩家与宠物都算）；装备栏里的道具被 `Char.DelItem` 或 NPC 事件指令删除。
事件在属性、套装、称号都已按新装备重新计算之后触发，处理函数读到的就是最终状态。限时到期、战斗损坏、脚本删除这三种不在当场触发，而是在下一轮角色巡检（RunLoop）释放全局锁后触发，每个角色或宠物每轮最多一次。
只在背包格之间移动道具不会触发；一次操作同时改变两只宠物的装备时，每只宠物各触发一次。
