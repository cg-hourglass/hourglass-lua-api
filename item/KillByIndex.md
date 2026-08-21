<!-- Generated. DO NOT EDIT. -->
# KillByIndex

## Item.KillByIndex(ItemIndex)

### 函数功能

仅凭道具 index 销毁一个道具实例（自动在持有者的 28 个背包槽位中定位）。

### 参数说明

- ItemIndex: [数值型](../appendix/数值型.md) 目标道具 index。

### 返回值

恒定返回 nil。

## 参考实例

```lua
Item.KillByIndex(item);
```

### 备注

行为上是 Item.Kill 的「不需要调用方提供槽位」版本：先扫描持有者的
0~27 号槽位定位 ItemIndex 所在槽位，找到则走与 Item.Kill 相同的销毁
流程（含系统消息，仅当持有者是玩家）；如果道具存在但没有任何角色的
槽位持有它（游离道具），则只记录一条审计日志并释放该道具实例，不发
系统消息。持有者不是玩家、或道具 index 无效时函数直接返回 nil、不做
任何事。
