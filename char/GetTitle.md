<!-- Generated. DO NOT EDIT. -->
# GetTitle

## Char.GetTitle(CharIndex)

### 函数功能

获取玩家当前装备的称号 ID。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

称号表中的称号 ID；没有装备称号、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local TitleID = Char.GetTitle(Player);
if TitleID ~= -1 then
    NLG.TalkToCli(Player, -1, "当前称号 ID 是 " .. TitleID);
end
```

### 备注

返回的是称号表中的 ID，不是称号栏位置；要把 ID 换成栏位号请用 Char.FindTitleIndex，
要按栏位号装备请用 Char.SelectTitle。失败路径全部安静，不打印日志。
