<!-- Generated. DO NOT EDIT. -->
# Warp

## Foreach.Warp(WarpFunction)

### 函数功能

对当前所有可用的 Warp 传送点角色依次执行指定的回调函数。

### 参数说明

- WarpFunction: [函数型](../appendix/函数型.md) 对每个 Warp 传送点调用一次的 Lua 函数，签名见 WarpFunction。

### 返回值

成功调用（回调没有报错）的次数。

## WarpFunction(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Warp 传送点的对象 index，由引擎按角色数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 WarpFunction
function MyForeachWarp(CharIndex)
  print("MyForeachWarp: "..CharIndex.." called")
  return 0
end

Foreach.Warp(MyForeachWarp); -- 对所有 Warp 传送点批量执行 WarpFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。Warp 传送点在角色数组里也是
一种角色类型，因此回调参数名沿用 CharIndex。
