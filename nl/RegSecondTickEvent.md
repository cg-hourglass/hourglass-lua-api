<!-- Generated. DO NOT EDIT. -->
# RegSecondTickEvent

## NL.RegSecondTickEvent(Dofile, FuncName)

### 函数功能

注册每秒触发一次的 Lua 函数，可以当定时器使用。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## SecondTickCallBack()

### 参数说明

无参数。

### 返回值

无

## 参考实例

```lua
NL.RegSecondTickEvent(nil, "MySecondTickEvent");

function MySecondTickEvent()
  -- 每秒执行一次的工作
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
每秒触发一次，在同一次服务器循环检查完代理控制者是否在场之后触发，不持有全局锁；不限于代理，任何脚本服务都可以用作定时器。回调不带任何参数。
回调带指令预算：可用量是本次服务器循环里与 `NL.RegAgentBattleCommandEvent` 合计约 100 万条虚拟机指令中尚未用掉的部分，超出时回调被中止；预算已经用完时本秒跳过不触发。预算只用来防止脚本缺陷造成卡服，不能防止恶意脚本。
本函数是本服务端新增的接口，C 版 gmsv 没有。
