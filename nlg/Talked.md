<!-- Generated. DO NOT EDIT. -->
# Talked

## NLG.Talked(Type, CharIndex, TargetCharIndex)

### 函数功能

调用引擎内置的银行/窗口治疗师/伤病医生三种 NPC 对话模板之一，是通往这几个legacy系统的桥接函数，不是通用的对话钩子。

### 参数说明

- Type: [数值型](../appendix/数值型.md) 内置模板编号，0=银行（数据刷新）、1=窗口治疗师、2=伤病医生。
- CharIndex: [数值型](../appendix/数值型.md) 自身对象index，多数情况下是 NPC。
- TargetCharIndex: [数值型](../appendix/数值型.md) 目标对象index，必须是玩家。

### 返回值

固定返回 1，不携带成功/失败信息。

## 参考实例

```lua
NLG.Talked(0, _MeIndex, playerIndex); -- 触发银行数据刷新
```

### 备注

本函数不是“0表示成功，其他表示失败”，而是无论对象是否有效、Type 是否命中 0/1/2 中的一个，一律固定返回 1；返回值不能用来判断调用是否真的生效。
TargetCharIndex 必须是玩家类型，否则内部直接跳过，只是仍然返回 1。
