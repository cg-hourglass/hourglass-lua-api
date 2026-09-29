<!-- Generated. DO NOT EDIT. -->
# OfflineLogin

## Offline.OfflineLogin(Cdkey, RegistNumber)

### 函数功能

以离线模式登录指定帐号的角色（不建立客户端连线），默认离线挂机时长按登录流程另行设定。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 帐号 CDKey。
- RegistNumber: [数值型](../appendix/数值型.md) 登录角色的 regist number（角色槽位序号）。

### 返回值

0 表示未能把登录请求交给后台处理（例如离线登录钩子未接入）；1 表示已经
把工作交给后台处理。返回 1 只表示请求已受理，不代表角色此刻已经加载
完成——真正的登录是异步的（走 DB 管线在运行循环中完成），调用方不能
假设返回后角色立即可操作。

## 参考实例

```lua
Offline.OfflineLogin("ABCD1234EFGH5678", 0);
```

### 备注

本函数本身不设置离线挂机时长——只是把角色读档工作投递给后台处理，
读档完成后角色以正常登录状态出现，离线挂机时长需要之后再调用
`Offline.SetOfflinePlayer` 显式设置。本函数与 `Debug.OfflineLogin` 是
同一实现（不在本文档范围）。
