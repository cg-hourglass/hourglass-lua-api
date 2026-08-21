<!-- Generated. DO NOT EDIT. -->
# RegPetRideImageEvent

## NL.RegPetRideImageEvent(Dofile, FuncName)

### 函数功能

注册服务器处理骑宠图档时触发的 Lua 函数，可以改写显示的骑宠图档。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## PetRideImageEventCallBack(CharIndex, PetRideImage)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 触发事件的对象index，由引擎传入。
- PetRideImage: [数值型](../appendix/数值型.md) 触发时的骑宠图档 id；没有骑宠时为 -1。由引擎传入。

### 返回值

返回需要显示的骑宠图档 id，或直接返回 PetRideImage 保持原样（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegPetRideImageEvent(nil, "MyPetRideImageEvent");

function MyPetRideImageEvent(CharIndex, PetRideImage)
  if(PetRideImage == -1)then
    return -1; -- 没有骑宠就保持原样
  end
  return PetRideImage;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
玩家角色（非战斗）与战斗中的所有角色都会触发。
只有两个参数进入 Lua：控制“要不要广播骑宠动作”的那个内部开关不会传给脚本。返回 -1 时服务器会走重置分支。
