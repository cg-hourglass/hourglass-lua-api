<!-- Generated. DO NOT EDIT. -->
# SetRemoteNpc

## NL.SetRemoteNpc(NpcIndex, RemoteEnabled)

### 函数功能

设置 NPC 的远程模式，开启后该 NPC 可以不受距离限制被触发。

### 参数说明

- NpcIndex: [数值型](../appendix/数值型.md) NPC 的对象index。
- RemoteEnabled: [数值型](../appendix/数值型.md) 是否开启远程支持。0 关闭，1 开启（传入任何非 0 值都按开启处理）。

### 返回值

返回该 NPC 新的远程模式状态（0 或 1）。目标是玩家、宠物或敌人时返回 -1；找不到对应的 Lua NPC 时也返回 -1。

## 参考实例

```lua
local ret = NL.SetRemoteNpc(TestNPC, 1);
NLG.SystemMessage(CharIndex, "远程NPC模式:"..ret);
```

### 备注

只有 Lua 创建的 NPC 才带这个标志位；对其它角色调用会返回 -1。
