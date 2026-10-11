<!-- Generated. DO NOT EDIT. -->
# ShowTalked

## NLG.ShowTalked(PlayerIndex, NpcIndex)

### 函数功能

触发一个对象自身注册的对话模板函数，并把另一个对象当作发起对话的一方传入。

### 参数说明

- PlayerIndex: [数值型](../appendix/数值型.md) 作为“发起对话者”身份传入回调的对象index，通常是玩家。
- NpcIndex: [数值型](../appendix/数值型.md) 其自身注册的 Talked 回调会被实际调用的对象index，通常是 NPC；若该对象没有注册回调则什么都不会发生。

### 返回值

参数无效返回 -1，其余情况固定返回 0。

## 参考实例

```lua
NLG.ShowTalked(playerIndex, _MeIndex);
```

### 备注

调用形状是 NpcIndex 自身 functable 里的 Talked 回调（如果有安装的话），以空消息、白色、字体大小1、PlayerIndex 作为“说话人”身份触发，通常用来主动弹出 NpcIndex 的对话窗口。只有指针安装了回调才会真正执行；未安装时不报错，也返回0。
