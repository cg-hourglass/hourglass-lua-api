<!-- Generated. DO NOT EDIT. -->
# GetAvatarParts

## NLG.GetAvatarParts(CharIndex)

### 函数功能

读取玩家或宠物当前的覆盖件编号。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

一个从下标1开始的 Lua table，元素为覆盖件编号（递增）；没有覆盖件时返回空 table；目标无效时返回 nil。

## 参考实例

```lua
local parts = NLG.GetAvatarParts(player);
for i = 1, #parts do
  print(parts[i]);
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
