<!-- Generated. DO NOT EDIT. -->
# FindTitleIndex

## Char.FindTitleIndex(CharIndex, TitleID)

### 函数功能

查找玩家是否拥有指定 ID 的称号，并返回其称号栏位置。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- TitleID: [数值型](../appendix/数值型.md) 称号 ID。

### 返回值

该称号所在的称号栏位置（0-47）；没有该称号、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
if Char.FindTitleIndex(Player, 100) == -1 then
    NLG.TalkToCli(Player, -1, "你还没有这个称号。");
end
```

### 备注

TitleID 传 -1 会直接短路返回 -1，不做扫描。称号栏总数本版本是 48。
