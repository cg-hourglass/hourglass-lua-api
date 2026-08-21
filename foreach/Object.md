<!-- Generated. DO NOT EDIT. -->
# Object

## Foreach.Object(ObjectFunction)

### 函数功能

对世界对象表中所有已使用（非 NOUSE）的 Object 依次执行指定的回调函数。

### 参数说明

- ObjectFunction: [函数型](../appendix/函数型.md) 对每个 Object 调用一次的 Lua 函数，签名见 ObjectFunction。

### 返回值

成功调用（回调没有报错）的次数。

## ObjectFunction(ObjectIndex)

### 参数说明

- ObjectIndex: [数值型](../appendix/数值型.md) Object 对象 index，可用 Obj 库进行操作，由引擎按对象数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 ObjectFunction
function MyForeachObject(ObjectIndex)
  print("MyForeachObject: "..ObjectIndex.." called")
  return 0
end

Foreach.Object(MyForeachObject); -- 对所有 Object 对象批量执行 ObjectFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。遍历的是世界对象表本身
（`Obj.*` 系列函数操作的同一张表），而不是某一类实体。
