<!-- Generated. DO NOT EDIT. -->
# IsPet

## Pet.IsPet(CharIndex)

### 函数功能

判断对象是否为宠物。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

1 表示该对象是宠物，0 表示不是。

## 参考实例

```lua
if Pet.IsPet(_target) == 1 then
    print("这是一只宠物");
end
```

### 备注

只有类型为宠物才返回 1；敌人类型返回 0。
注意 Pet 库中的成长值、技能类函数同时接受宠物与敌人，判定口径与本函数不同。
