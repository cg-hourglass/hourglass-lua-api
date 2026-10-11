<!-- Generated. DO NOT EDIT. -->
# GetStatusString

## Item.GetStatusString(ItemIndex, ViewerIndex)

### 函数功能

生成道具的原生状态串，供扩展客户端的原生道具浮框使用（摆摊扩展）。

### 参数说明

- ItemIndex: [数值型](../appendix/数值型.md) 道具index。
- ViewerIndex: [数值型](../appendix/数值型.md) 查看者的对象index，必须是玩家；状态串里的标志位按查看者计算。

### 返回值

道具状态串；道具或查看者无效时返回 nil。格式与背包、摊位浏览下发给客户端的道具串相同，只是去掉了开头的栏位号，共 13 段，以 `|` 分隔：
`名称|颜色|说明|图号|可用场合|战斗可用|对象|等级|标志|道具ID|类型|堆叠数|备注`（文字段已按协议转义；堆叠上限为 1 的道具堆叠数写 0）。

## 参考实例

```lua
local status = Item.GetStatusString(item, player);
if status then
  -- 通过扩展协议下发给客户端，由客户端显示原生道具浮框
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
与原生摊位浏览不同，标志位（例如“可以装备”）按查看者而不是道具持有者计算；生成时同样会触发 NL.RegMakeItemStringEvent 注册的事件。
