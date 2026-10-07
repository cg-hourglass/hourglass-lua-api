<!-- Generated. DO NOT EDIT. -->
# RegHeadCoverEvent

## NL.RegHeadCoverEvent(Dofile, FuncName)

### 函数功能

注册生成角色头饰效果时触发的 Lua 函数，可以在不装备头饰道具的前提下指定头饰图档。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## HeadCoverEventCallBack(CharIndex, CurrentHeadCoverImage)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 正在被序列化的对象index，由引擎传入。
- CurrentHeadCoverImage: [数值型](../appendix/数值型.md) 该对象当前的头饰图档 id，由引擎传入。

### 返回值

返回新的头饰图档 id。不想改动就返回 CurrentHeadCoverImage（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegHeadCoverEvent(nil, "MyHeadCoverEvent");

-- 所有玩家和宠物都戴上小鸭子帽
function MyHeadCoverEvent(CharIndex, CurrentHeadCoverImage)
  return 114186;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
玩家和宠物都会触发，可用来做节日效果、或在没有宠物装备的版本里搭配宠物 UUID 做宠物头饰系统。
本事件有 25 处触发点，全部位于角色数据组包路径上，属于服务端最热的路径之一；处理函数必须非常轻量。
RegPetRideImageEvent 的回调内部会广播骑宠动作，从而嵌套触发本事件，注意不要写出互相递归的处理函数。
