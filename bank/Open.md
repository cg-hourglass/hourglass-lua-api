<!-- Generated. DO NOT EDIT. -->
# Open

## Bank.Open(CharIndex)

### 函数功能

Open the original bank window and establish a bank-only context.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.

### 返回值

1 for an usable player, 0 otherwise.

## 参考实例

```lua
Bank.Open(player);
```

### 备注

Scripts control access. Movement, warp, battle, logout and disconnect invalidate the context. No bank rights are granted.
