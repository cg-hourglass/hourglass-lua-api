<!-- Generated. DO NOT EDIT. -->
# RegEquipmentLevelEvent

## NL.RegEquipmentLevelEvent(Dofile, FuncName)

### 函数功能

注册读取装备使用所需等级时触发的 Lua 函数，可以改写该等级要求。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## EquipmentLevelEventCallBack(CharIndex, ItemIndex, ItemLevel, EquipLevel)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 尝试装备道具的对象index，由引擎传入。
- ItemIndex: [数值型](../appendix/数值型.md) 道具的对象index，由引擎传入。
- ItemLevel: [数值型](../appendix/数值型.md) 道具等级，由引擎传入。
- EquipLevel: [数值型](../appendix/数值型.md) 装备原本要求的使用等级，由引擎传入。

### 返回值

返回新的所需等级。不想改动就返回 EquipLevel（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegEquipmentLevelEvent(nil, "MyEquipmentLevelEvent");

function MyEquipmentLevelEvent(CharIndex, ItemIndex, ItemLevel, EquipLevel)
  return 1; -- 所有装备都可以 1 级使用
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
触发点在服务器检查“这件装备能不能穿”的地方，并且只在道具等级大于 0 时才触发。
