<!-- Generated. DO NOT EDIT. -->
# Player

## Foreach.Player(PlayerFunction)

### 函数功能

对当前所有在线玩家依次执行指定的回调函数。

### 参数说明

- PlayerFunction: [函数型](../appendix/函数型.md) 对每个在线玩家调用一次的 Lua 函数，签名见 PlayerFunction。

### 返回值

成功调用（回调没有报错）的次数。

## PlayerFunction(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 在线玩家的对象 index，由引擎按角色数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 PlayerFunction
function MyForeachPlayer(CharIndex)
  print("MyForeachPlayer: "..CharIndex.." called, CDK="..Char.GetData(CharIndex, %对象_CDK%))
  return 0
end

Foreach.Player(MyForeachPlayer); -- 对在线玩家批量执行 PlayerFunction
```

### 备注

参数个数不对，或第一个参数不是函数时，会直接抛出一个可被 pcall 捕获
的 Lua 错误，函数根本不会正常返回、更不会返回 -1。

同 kind 不可重入：内部用一个「每种 kind 一个」的全局槽位保存当前正在
执行的回调引用，若在 PlayerFunction 内部再次调用 Foreach.Player（同一
kind 嵌套），内层调用会覆盖外层的槽位，外层循环剩余的迭代会解析到一个
已被释放的引用（非函数），逐次报错且不计入返回的成功次数；不同 kind
之间（例如在 Foreach.Player 内部调用 Foreach.Pet）互不影响，可以安全
嵌套。

回调内部发生的 Lua 错误会被记录日志并跳过该次调用（不计入返回次数），
循环不会中止。
