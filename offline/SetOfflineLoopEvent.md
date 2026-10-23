<!-- Generated. DO NOT EDIT. -->
# SetOfflineLoopEvent

## Offline.SetOfflineLoopEvent(Dofile, FuncName, CharIndex, Interval)

### 函数功能

为指定对象设置离线循环事件回调，每隔 Interval 毫秒触发一次，直到被清除或对象登出。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 回调函数所在的脚本文件；若为字符串会先 dofile 该文件，通常传 nil 表示回调函数已在当前脚本中定义。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发的 Lua 函数名（按名字解析，见 OfflineCharLoopCallBack）。
- CharIndex: [数值型](../appendix/数值型.md) 设置的对象 index。
- Interval: [数值型](../appendix/数值型.md) 循环间隔，单位毫秒。

### 返回值

对象无效返回 -1；对象有效则恒定返回 1（无论本次是新安装、已安装保持不变、还是被清除，均返回 1）。

## OfflineCharLoopCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 响应事件的对象 index，由引擎传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
Offline.SetOfflineLoopEvent(nil, "myOfflineLoop", player, 5000); -- 每 5 秒触发一次

function myOfflineLoop(charIndex)
  NLG.SystemMessage(-1, "离线循环触发："..charIndex);
end
```

### 备注

FuncName 是否已注册决定的是「安装/保持不变/卸载」三条分支，但无论走
哪条分支，只要 CharIndex 能解析出有效对象，最终返回值都是 1。回调按
名字在每次触发时刻解析，不是注册时绑定的闭包。
