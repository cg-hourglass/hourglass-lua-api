<!-- Generated. DO NOT EDIT. -->
# GetRider

## Pet.GetRider(PetIndex)

### 函数功能

获取骑乘该宠物的玩家对象index。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index。

### 返回值

骑乘者的对象index；宠物未被骑乘、对象不是宠物，或骑乘者不是玩家时返回 -1。

## 参考实例

```lua
if Pet.GetRider(_pet) ~= -1 then
    print("这只宠物正在被骑乘");
end
```
