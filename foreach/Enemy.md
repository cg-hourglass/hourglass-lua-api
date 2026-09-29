<!-- Generated. DO NOT EDIT. -->
# Enemy

## Foreach.Enemy(EnemyFunction)

### 函数功能

对当前地图上所有敌人（战斗单位）角色依次执行指定的回调函数。

### 参数说明

- EnemyFunction: [函数型](../appendix/函数型.md) 对每个敌人角色调用一次的 Lua 函数，签名见 EnemyFunction。

### 返回值

成功调用（回调没有报错）的次数。

## EnemyFunction(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 敌人角色的对象 index，由引擎按角色数组顺序依次传入。

### 返回值

返回值被忽略（引擎以 0 个返回值调用该回调）。

## 参考实例

```lua
-- 定义一个 EnemyFunction
function MyForeachEnemy(CharIndex)
  print("MyForeachEnemy: "..CharIndex.." called")
  return 0
end

Foreach.Enemy(MyForeachEnemy); -- 对所有敌人角色批量执行 EnemyFunction
```

### 备注

参数校验失败的返回值修正、同 kind 不可重入、错误不计入返回次数等说明，
与 Foreach.Player 一致，参见该条目 notes。
