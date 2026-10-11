<!-- Generated. DO NOT EDIT. -->
# Get

## Agent.Get(Cdkey)

### 函数功能

获取已召出代理角色的对象index。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号。

### 返回值

代理已召出时返回它的对象index，否则（未召出、正在召出或不存在）返回 -1。

## 参考实例

```lua
local charIndex = Agent.Get(cdkey);
if charIndex >= 0 then
  -- 代理在地图上
end
```

### 备注

只读。本函数是本服务端新增的接口，C 版 gmsv 没有。
