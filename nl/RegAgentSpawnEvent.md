<!-- Generated. DO NOT EDIT. -->
# RegAgentSpawnEvent

## NL.RegAgentSpawnEvent(Dofile, FuncName)

### 函数功能

注册代理角色召出完成或召出失败时触发的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AgentSpawnCallBack(Cdkey, CharIndex, Code)

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 代理角色的账号，服务器编码的原始字节。
- CharIndex: [数值型](../appendix/数值型.md) 代理角色的对象index；召出失败时为 -1。
- Code: [字符串](../appendix/字符串.md) 结果码。`OK` 召出成功；`LOAD` 读档失败或 30 秒内没有完成；`PLACE` 找不到可放置的位置；`FULL` 服务器剩余的玩家名额不足；`CONTROLLER` 控制者已不在场。

### 返回值

无

## 参考实例

```lua
NL.RegAgentSpawnEvent(nil, "MyAgentSpawnEvent");

function MyAgentSpawnEvent(Cdkey, CharIndex, Code)
  if Code == "OK" then
    -- 代理 CharIndex 已经出现在地图上
  else
    -- 召出失败，Code 说明原因
  end
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
召出是异步的：发起召出的调用返回后，本事件在之后的某一次服务器循环里触发，不在战斗处理过程中，也不持有全局锁，回调里可以调用任何接口。
本函数是本服务端新增的接口，C 版 gmsv 没有。
