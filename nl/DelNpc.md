<!-- Generated. DO NOT EDIT. -->
# DelNpc

## NL.DelNpc(NpcIndex)

### 函数功能

删除一个 NPC。

### 参数说明

- NpcIndex: [数值型](../appendix/数值型.md) 要删除的对象index。

### 返回值

成功返回1，失败返回0。

## 参考实例

```lua
if(TestNPC ~= nil)then
  NL.DelNpc(TestNPC);
  TestNPC = nil; -- 引擎不会帮你把变量置空
end
```

### 备注

本函数不会把传入的变量置为 nil，删除后请自行处理脚本里保存的 index。
能删除的范围是“既不是玩家也不是宠物”的任何角色：Lua 创建的 NPC、数据文件生成的普通 NPC 以及敌人都可以删；对玩家和宠物调用一律返回 0。
