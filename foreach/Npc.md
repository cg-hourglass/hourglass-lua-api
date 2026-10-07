<!-- Generated. DO NOT EDIT. -->
# Npc

## Foreach.Npc(NpcFunction)

### 函数功能

对当前地图上所有 NPC 类角色依次执行指定的回调函数（不含玩家/宠物/敌人/传送点）。

### 参数说明

- NpcFunction: [函数型](../appendix/函数型.md) 对每个 NPC 调用一次的 Lua 函数，签名见 NpcFunction。

### 返回值

成功调用（回调没有报错）的次数。

## NpcFunction(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) NPC 角色的对象 index，由引擎按角色数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 NpcFunction
function MyForeachNpc(CharIndex)
  print("MyForeachNpc: "..CharIndex.." called")
  return 0
end

Foreach.Npc(MyForeachNpc); -- 对所有 NPC 角色批量执行 NpcFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。这里的"NPC"是排除法定义：
角色类型不属于 WARP/PLAYER/PET/ENEMY 的都算 NPC。
