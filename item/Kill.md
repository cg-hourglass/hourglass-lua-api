<!-- Generated. DO NOT EDIT. -->
# Kill

## Item.Kill(CharIndex, ItemIndex, Slot)

### 函数功能

删除玩家指定槽位上的道具实例，并向该玩家发送系统提示与客户端刷新。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象 index，必须是玩家类型。
- ItemIndex: [数值型](../appendix/数值型.md) 目标道具 index。
- Slot: [数值型](../appendix/数值型.md) 指定背包槽位，调用方需自行保证该槽位确实持有 ItemIndex。

### 返回值

恒定返回 nil。

## 参考实例

```lua
Item.Kill(player, item, slot);
```

### 备注

Slot 不会与 ItemIndex 的实际持有槽位做交叉校验，调用方需自行保证两者
一致；只有目标对象是玩家类型才会真的执行销毁与发系统消息，非玩家类型
或无效道具 index 时函数直接返回 nil、不做任何事。
