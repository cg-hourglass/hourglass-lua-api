<!-- Generated. DO NOT EDIT. -->
# Set

## Setup.Set(ConfigName, ConfigValue)

### 函数功能

修改服务端当前进程内某配置项在内存中的数值；不改写配置文件本身，重启后修改效果消失。

### 参数说明

- ConfigName: [字符串](../appendix/字符串.md) 配置项名称，可用键见附录[Setup 配置键](../appendix/setup配置键.md)。
- ConfigValue: [字符串](../appendix/字符串.md) 要写入的新值。

### 返回值

成功返回写入后的当前值（与 Setup.Get 读到的一致）；键名未登记时返回 -1。

## 参考实例

```lua
local ret = Setup.Set("char_free_healer_level", "100"); -- 将免费恢复hp等级的上限调整为100级
```

### 备注

本版本保留了以下历史行为，未做“修正”：
- 数值型配置项写入字符串 "ON" 或 "OFF" 效果完全相同，都会把该项写成 1；不存在“OFF 会清零/关闭”这回事。
- 写入其它非 "ON"/"OFF" 的字符串时，按“最长可解析的数字前缀”规则解析，解析失败一律按 0 处理；字符串型配置项没有这个限制，只按声明的字节长度截断保存。
- 部分配置项（各类地图/IP 列表型的 stallshop_map_0N、dual_map_0N、gate_tunnel_ip1..10 等切片型配置，以及个别本版本尚未接入对应字段的配置项）当前未接入本注册表，一律按未知键处理，Get/Set 都返回 -1；完整清单以附录[Setup 配置键](../appendix/setup配置键.md)为准。
- Setup.Set 直接写在服务端当前运行的实时配置对象上；个别子系统在启动时会另外快照一份配置（例如战斗反作弊参数），这些子系统感知不到运行期通过 Setup.Set 做的修改。
