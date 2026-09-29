<!-- Generated. DO NOT EDIT. -->
# RegPartyEvent

## NL.RegPartyEvent(Dofile, FuncName)

### 函数功能

注册玩家组队与离队时触发的 Lua 函数，可以拦截该操作。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## PartyEventCallBack(CharIndex, TargetCharIndex, Type)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 发起本次组队操作的对象index，由引擎传入。
- TargetCharIndex: [数值型](../appendix/数值型.md) 本次操作的另一方对象index，由引擎传入。
- Type: [数值型](../appendix/数值型.md) 操作类型。0 = 加入队伍，1 = 离开队伍。由引擎传入。

### 返回值

返回1允许操作；返回0拦截（组队失败/离队失败）。未注册、解析失败或调用出错时默认允许。

## 参考实例

```lua
NL.RegPartyEvent(nil, "MyPartyEvent");

function MyPartyEvent(CharIndex, TargetCharIndex, Type)
  if(Type == 0)then
    NLG.SystemMessage(CharIndex, "现在不能组队哟！");
    return 0;
  end
  return 1;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
三个触发点：一次加入队伍（Type=0），以及离队时的自身离队与通知队长两处（Type=1）。
三个触发点里 CharIndex 与 TargetCharIndex 的身份并不固定（离队通知那一处方向相反），
不要把它们当成恒定的“队员/队长”，请脚本自行用 Char.GetData 判断身份。
