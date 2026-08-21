<!-- Generated. DO NOT EDIT. -->
# RegAfterWarpEvent

## NL.RegAfterWarpEvent(Dofile, FuncName)

### 函数功能

注册玩家使用传送点时触发的 Lua 函数，比 RegWarpEvent 多带传送前后的完整坐标。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AfterWarpCallBack(CharIndex, Ori_MapId, Ori_FloorId, Ori_X, Ori_Y, Target_MapId, Target_FloorId, Target_X, Target_Y)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 被传送的对象index，由引擎传入。
- Ori_MapId: [数值型](../appendix/数值型.md) 传送前的 map id，由引擎传入。
- Ori_FloorId: [数值型](../appendix/数值型.md) 传送前的 floor id，由引擎传入。
- Ori_X: [数值型](../appendix/数值型.md) 传送前的 x 坐标，由引擎传入。
- Ori_Y: [数值型](../appendix/数值型.md) 传送前的 y 坐标，由引擎传入。
- Target_MapId: [数值型](../appendix/数值型.md) 传送后的 map id，由引擎传入。
- Target_FloorId: [数值型](../appendix/数值型.md) 传送后的 floor id，由引擎传入。
- Target_X: [数值型](../appendix/数值型.md) 传送后的 x 坐标，由引擎传入。
- Target_Y: [数值型](../appendix/数值型.md) 传送后的 y 坐标，由引擎传入。

### 返回值

返回0即可。引擎以 0 个返回值调用本函数，返回什么都不会被读取。

## 参考实例

```lua
NL.RegAfterWarpEvent(nil, "MyAfterWarpEvent");

function MyAfterWarpEvent(CharIndex, Ori_MapId, Ori_FloorId, Ori_X, Ori_Y, Target_MapId, Target_FloorId, Target_X, Target_Y)
  print("玩家"..CharIndex.."从"..Ori_FloorId.."传送到了"..Target_FloorId);
  return 0;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
名字虽然叫 AfterWarp，触发点其实在角色的 MapId/Floor/X/Y 真正写入之前：在回调里用 Char.GetData 读坐标拿到的仍是旧位置，新位置只在参数里。
