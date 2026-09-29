<!-- Generated. DO NOT EDIT. -->
# RegPetEquipCheckEvent

## NL.RegPetEquipCheckEvent(Dofile, FuncName)

### 函数功能

注册宠物装备道具前触发的 Lua 函数，可以禁止本次装备。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## PetEquipCheckEventCallBack(CharIndex, ItemIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 要装备道具的宠物对象index；调用方没有角色上下文时传入 -1。由引擎传入。
- ItemIndex: [数值型](../appendix/数值型.md) 要装备的道具对象index，由引擎传入。

### 返回值

返回0禁止本次装备；返回非0允许。

## 参考实例

```lua
NL.RegPetEquipCheckEvent(nil, "MyPetEquipCheckEvent");

function MyPetEquipCheckEvent(CharIndex, ItemIndex)
  return 0; -- 禁止所有宠物装备道具
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
与其它可改写事件不同，本事件的默认值是常量“允许”，而不是“沿用服务器算出的值”：未注册、名字解析失败、调用出错或返回非数值时一律放行。
触发点在服务器检查“这只宠物能不能穿这件装备”的地方。本事件是少数容忍“没有角色”的回调之一，CharIndex 可能为 -1。
