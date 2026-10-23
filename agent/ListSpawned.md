<!-- Generated. DO NOT EDIT. -->
# ListSpawned

## Agent.ListSpawned(Kind)

### 函数功能

列出全服已召出代理角色的对象index。

### 参数说明

- Kind: [字符串](../appendix/字符串.md) 只列出该 kind 的代理；省略时列出全部。 [可为空]

### 返回值

对象index 的数组，从小到大排序；没有时返回空表。

## 参考实例

```lua
for _, charIndex in ipairs(Agent.ListSpawned("partner")) do
  -- 每个在地图上的伙伴
end
```

### 备注

只读。本函数是本服务端新增的接口，C 版 gmsv 没有。
