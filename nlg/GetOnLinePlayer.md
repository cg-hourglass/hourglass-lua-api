<!-- Generated. DO NOT EDIT. -->
# GetOnLinePlayer

## NLG.GetOnLinePlayer()

### 函数功能

获取当前全服在线玩家总数。

### 函数别名

- `NLG.GetPlayerNum()`

### 参数说明

无参数。

### 返回值

当前在线玩家数（大于等于0的整数）。

## 参考实例

```lua
local num = NLG.GetOnLinePlayer();
```

### 备注

函数别名：`NLG.GetPlayerNum()`，参数与语义完全相同。
本函数没有失败返回 -1 的分支，恒为非负整数。
