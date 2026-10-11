<!-- Generated. DO NOT EDIT. -->
# RegAfterBattleExitEvent

## NL.RegAfterBattleExitEvent(Dofile, FuncName)

### 函数功能

注册玩家战斗状态清除（回到地图、可以正常操作）后触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AfterBattleExitCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 离开战斗的玩家对象index，由引擎传入。

### 返回值

无

## 参考实例

```lua
NL.RegAfterBattleExitEvent(nil, "MyAfterBattleExitEvent");

function MyAfterBattleExitEvent(CharIndex)
  NLG.SortItem(CharIndex); -- 战斗中无法整理背包，这里已经可以
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本服务端扩展事件，原版没有。战斗结束（RegBattleOverEvent）、离开战斗（RegBattleExitEvent）时角色仍处于战斗状态，背包整理等操作会被拒绝；本事件在玩家客户端确认退出战斗、战斗状态清除之后触发，此时本场战斗的掉落已经在背包里。
每位玩家各触发一次；观战结束同样触发，PVP 与普通战斗不区分，需要时请在 RegBattleOverEvent 里自行记录。玩家在战斗中断线则不会触发。
