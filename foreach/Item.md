<!-- Generated. DO NOT EDIT. -->
# Item

## Foreach.Item(ItemFunction)

### 函数功能

对所有已使用且状态可用的道具实例依次执行指定的回调函数。

### 参数说明

- ItemFunction: [函数型](../appendix/函数型.md) 对每个道具对象调用一次的 Lua 函数，签名见 ItemFunction。

### 返回值

成功调用（回调没有报错）的次数。

## ItemFunction(ItemIndex)

### 参数说明

- ItemIndex: [数值型](../appendix/数值型.md) 道具对象 index，可用 Item 库进行操作，由引擎按道具数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 ItemFunction
function MyForeachItem(ItemIndex)
  print("MyForeachItem: "..ItemIndex.." called")
  return 0
end

Foreach.Item(MyForeachItem); -- 对所有 Item 对象批量执行 ItemFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。遍历范围是道具管理器内的
全部道具槽位，跳过未使用及工作状态不是“可用”的道具。
