<!-- Generated. DO NOT EDIT. -->
# SelectTitle

## Char.SelectTitle(CharIndex, TitleIndex)

### 函数功能

为玩家装备指定栏位上的称号。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- TitleIndex: [数值型](../appendix/数值型.md) 称号栏位置，取值 0-47；传 -1 表示卸下当前称号。

### 返回值

调用之后实际装备的称号栏位置；对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
local Index = Char.FindTitleIndex(Player, 100);
if Index ~= -1 then
    Char.SelectTitle(Player, Index);
end
```

### 备注

TitleIndex 越界不会报错，也不会改变任何状态，只是把当前装备的栏位原样返回——
这里沿袭旧版行为，不做边界校验，因此不能靠返回值判断“装备成功”，
要确认请拿返回值与传入值比较。
玩家处于死亡状态时同样不做任何改动，直接返回当前栏位。
参数是称号栏位置而不是称号 ID；要从 ID 换算成栏位号请用 Char.FindTitleIndex。
