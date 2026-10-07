<!-- Generated. DO NOT EDIT. -->
# List

## Agent.List(ControllerIndex, Kind)

### 函数功能

列出一名控制者名下的代理角色。

### 参数说明

- ControllerIndex: [数值型](../appendix/数值型.md) 控制者的对象index，必须是真人玩家。
- Kind: [字符串](../appendix/字符串.md) 只列出该 kind 的代理；省略或 nil 时列出全部。 [可为空]

### 返回值

成功返回信息表的数组（每项与 `Agent.Info` 的返回相同），按创建时间排序；没有代理时返回空表。失败返回 `nil, "BAD_ARGS"`（ControllerIndex 不是真人玩家，或 Kind 不是字符串）或 `nil, "DB"`（登录时没能载入该控制者的登记，本次重读仍失败）。

## 参考实例

```lua
for _, info in ipairs(Agent.List(player, "partner") or {}) do
  print(info.key, info.state);
end
```

### 备注

只读。列表来自控制者登录时载入的登记，不读库；只有登录时载入失败的控制者，下一次调用会重读一次。
本函数是本服务端新增的接口，C 版 gmsv 没有。
