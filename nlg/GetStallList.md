<!-- Generated. DO NOT EDIT. -->
# GetStallList

## NLG.GetStallList()

### 函数功能

列出当前所有开着的摊位（包括离线摊位），用于集市索引（摆摊扩展）。

### 参数说明

无参数。

### 返回值

从下标 1 开始的 table，按摊位槽顺序排列，每个元素是：
`{char = 摊主对象index, name = 摊位名称, msg = 摊位留言, offline = 摊主当前没有在线连接时为 true, offline_opt = 摊主已开启离线摆摊时为 true, rev = 版本号}`。
没有摊位时返回空 table。

## 参考实例

```lua
for _, stall in ipairs(NLG.GetStallList()) do
  if Cache[stall.char] == nil or Cache[stall.char].rev ~= stall.rev then
    Cache[stall.char] = {rev = stall.rev, goods = NLG.GetStallGoods(stall.char)};
  end
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
rev 在开摊、每成交一笔、收摊时各加 1，并且在同一个摊主身上一直递增（收摊后重新开摊也不会归零），集市只需要重新读取 rev 变化了的摊位。
offline_opt 是 NLG.SetStallOffline 设置的开关，收摊时清除；它的变化不会改变 rev。
