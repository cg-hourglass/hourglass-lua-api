<!-- Generated. DO NOT EDIT. -->
# GetPoolPet

## Char.GetPoolPet(CharIndex, Slot)

### 函数功能

获取玩家银行中指定位置的宠物对象index。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。
- Slot: [数值型](../appendix/数值型.md) 银行宠物栏位置，本版本范围 0-9。

### 返回值

该位置宠物的对象index；位置为空、位置越界、宠物已失效、对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
for i = 0, 9 do
    local Pet = Char.GetPoolPet(Player, i);
    if Pet ~= -1 then
        -- 银行该位置有宠物
    end
end
```

### 备注

位置上限本版本是 10，因此取值是 0-9。
对象指针无效时会在服务端日志留下一条错误记录。
