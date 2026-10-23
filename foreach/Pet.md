<!-- Generated. DO NOT EDIT. -->
# Pet

## Foreach.Pet(PetFunction)

### 函数功能

对当前所有在线宠物依次执行指定的回调函数。

### 参数说明

- PetFunction: [函数型](../appendix/函数型.md) 对每只在线宠物调用一次的 Lua 函数，签名见 PetFunction。

### 返回值

成功调用（回调没有报错）的次数。

## PetFunction(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 在线宠物的对象 index，由引擎按角色数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 PetFunction
function MyForeachPet(CharIndex)
  print("MyForeachPet: "..CharIndex.." called, CDK="..Char.GetData(CharIndex, %对象_CDK%))
  return 0
end

Foreach.Pet(MyForeachPet); -- 对所有在线宠物批量执行 PetFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。
