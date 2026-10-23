<!-- Generated. DO NOT EDIT. -->
# GetObject

## Obj.GetObject(MapId, FloorId, X, Y)

### 函数功能

获取指定地图坐标上的 Object Index 列表。

### 参数说明

- MapId: [数值型](../appendix/数值型.md) 坐标所在的 Map ID。
- FloorId: [数值型](../appendix/数值型.md) 坐标所在的 Floor ID。
- X: [数值型](../appendix/数值型.md) 坐标 X。
- Y: [数值型](../appendix/数值型.md) 坐标 Y。

### 返回值

返回两个值：第一个是该坐标格上的 Object 数量，第二个是 1 基索引的 lua
table，元素为各 Object 的对象 index。地图管理器未初始化或该坐标没有对象
链表时数量为 0、table 为空表。

## 参考实例

```lua
local count, objs = Obj.GetObject(mapId, floorId, x, y);
for i = 1, count do
  NLG.SystemMessage(-1, "objIndex="..objs[i]);
end
```

### 备注

结果最多收录 1024 个对象，这是沿袭旧版的一个上限行为：当格子上的对象数
量达到 1024 个时，第 1024 个对象的 index 会先写入数组，随后计数被减 1，
因此最终 count 只有 1023，且最后写入的那个索引不会出现在返回的 table
里。本服务端按原样保留了这一行为，未做修正。
