<!-- Generated. DO NOT EDIT. -->
# GetMeta

## Agent.GetMeta(Cdkey)

### 函数功能

读取代理角色的自定义数据。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号。

### 返回值

成功返回保存的字节串，未设置时为空字符串 `""`。失败返回 `nil, 错误码`：`NO_AGENT` 没有这个代理；`NOT_LOADED` 代理的控制者不在线。

## 参考实例

```lua
local meta = Agent.GetMeta(cdkey);
if meta == "" then
  meta = "rank=1";
end
```

### 备注

只读。代理不需要召出，控制者在线即可读取。
本函数是本服务端新增的接口，C 版 gmsv 没有。
