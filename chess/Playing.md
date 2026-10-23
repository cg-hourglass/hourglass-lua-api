<!-- Generated. DO NOT EDIT. -->
# Playing

## Chess.Playing(CharIndex)

### 函数功能

查询某角色当前正在看的图鉴棋局回放。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 角色索引。

### 返回值

回放 ID；不在回放中时为 nil。

## 参考实例

```lua
if Chess.Playing(charIndex) then return end
```
