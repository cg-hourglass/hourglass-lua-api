<!-- Generated. DO NOT EDIT. -->
# Get

## Setup.Get(ConfigName)

### 函数功能

按配置项名称读取服务端当前生效的设置值。

### 参数说明

- ConfigName: [字符串](../appendix/字符串.md) 配置项名称，可用键见附录[Setup 配置键](../appendix/setup配置键.md)。

### 返回值

该项当前的值（数值型或字符串型，取决于该配置项声明的类型）；键名未登记时返回 -1。

## 参考实例

```lua
local ret = Setup.Get("char_free_healer_level"); -- 获取免费恢复hp的等级上限
```
