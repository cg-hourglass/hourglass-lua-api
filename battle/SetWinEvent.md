<!-- Generated. DO NOT EDIT. -->
# SetWinEvent

## Battle.SetWinEvent(DoFile, FuncName, BattleIndex)

### 函数功能

为战斗设置胜利事件的 Lua 回调函数，战斗结束时由引擎回调。

### 函数别名

- `Battle.SetPVPWinEvent(DoFile, FuncName, BattleIndex)`

### 参数说明

- DoFile: [字符串](../appendix/字符串.md) 要先加载的脚本文件名；回调函数就在当前文件内时传 nil。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发的 Lua 全局函数名，声明格式见下方 BattleWinCallBack。
- BattleIndex: [数值型](../appendix/数值型.md) 战斗index。注意战斗index是**第三个**参数，不是第一个。

### 返回值

1 安装成功；-1 战斗index非法，或 FuncName 不是字符串（此时会卸载已安装的回调）；-2 该名字当前不是一个函数（同样卸载回调）。

## BattleWinCallBack(BattleIndex, CharIndex)

### 参数说明

- BattleIndex: [数值型](../appendix/数值型.md) 战斗index，由引擎传入。
- CharIndex: [数值型](../appendix/数值型.md) 战斗的 create 方对象index（创建这场战斗的对象），由引擎传入。

### 返回值

无需返回值，引擎忽略回调的返回结果。

## 参考实例

```lua
function MyBattleWin(TM_BattleIndex, TM_CharIndex)
    print("battle win: " .. TM_BattleIndex);
end

Battle.SetWinEvent(nil, "MyBattleWin", TM_BattleIndex);
```

### 备注

回调按**名字**在战斗结束时才解析全局表，不是注册时绑定的闭包：注册后重新定义同名全局函数会生效，
删除该全局函数则只会记录一条 pcall 失败日志，错误不会外溢。

别名 Battle.SetPVPWinEvent 与本函数是同一个实现，PVP 战斗与非 PVP 战斗并没有区别对待，
两个名字只是同一功能的两个注册名；回调始终传入两个参数。

**本版本已知行为**：只有在回调尚未安装时才会保存函数名。对同一场战斗第二次调用
SetWinEvent 换用另一个函数名时，旧名字仍然保留，新名字被丢弃。要更换回调，需要先用
一个非字符串的 FuncName 卸载，再重新注册。
