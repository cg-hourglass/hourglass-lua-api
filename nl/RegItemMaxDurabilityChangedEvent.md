<!-- Generated. DO NOT EDIT. -->
# RegItemMaxDurabilityChangedEvent

## NL.RegItemMaxDurabilityChangedEvent(Dofile, FuncName)

### 函数功能

注册道具最大耐久度变化时触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## ItemMaxDurabilityChangedCallBack(ItemIndex, OldDurability, NewDurability, ChangedValue)

### 参数说明

- ItemIndex: [数值型](../appendix/数值型.md) 发生变化的道具对象index，由引擎传入。
- OldDurability: [数值型](../appendix/数值型.md) 变化前的最大耐久度，由引擎传入。
- NewDurability: [数值型](../appendix/数值型.md) 变化后的最大耐久度，由引擎传入。
- ChangedValue: [数值型](../appendix/数值型.md) 变化量，等于 NewDurability - OldDurability，由引擎传入。

### 返回值

返回0即可。引擎以 0 个返回值调用本函数，返回什么都不会被读取。

## 参考实例

```lua
NL.RegItemMaxDurabilityChangedEvent(nil, "MyItemMaxDurabilityChangedEvent");

function MyItemMaxDurabilityChangedEvent(ItemIndex, OldDurability, NewDurability, ChangedValue)
  print("道具"..ItemIndex.."最大耐久变化了"..ChangedValue);
  return 0;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
形状与 RegItemDurabilityChangedEvent 完全一致，只是监听的字段换成最大耐久度；同样可以在回调里用 Item.SetData 改写而不会递归。
