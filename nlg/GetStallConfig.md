<!-- Generated. DO NOT EDIT. -->
# GetStallConfig

## NLG.GetStallConfig()

### 函数功能

读取服务端当前生效的摆摊配置开关（摆摊扩展）。

### 参数说明

无参数。

### 返回值

`{enabled = 摆摊是否开启, token_price = 是否允许代币价, token_price_max = 代币价上限, save_after_trade = 每笔成交后是否存盘, remote_buy = 是否允许 NLG.StallBuy 远程购买, offline_enabled = 是否允许离线摆摊, offline_max_hours = 离线摆摊最长小时数, tax = 成交税率}`。
布尔值为 true/false，tax 是小数（配置 `stall.tax`，0.05 即 5%，原生金币成交扣 floor(价格 × tax)），其余为整数。

## 参考实例

```lua
local cfg = NLG.GetStallConfig();
if not cfg.remote_buy then
  NLG.SystemMessage(player, "集市暂未开放远程购买。");
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
返回的是启动时读入并校正后的值（例如 token_price_max 不是正数时按默认值，开启离线摆摊时 save_after_trade 强制为 true），与服务器实际使用的一致，脚本不需要自己再写一份开关。
每次调用返回一个新的 table，修改它不会影响服务器的配置。
