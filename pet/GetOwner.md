<!-- Generated. DO NOT EDIT. -->
# GetOwner

## Pet.GetOwner(PetIndex)

### 函数功能

获取宠物的拥有者对象index。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index。

### 返回值

拥有者的对象index；对象不是宠物、或主人指针为空／不是玩家时返回 -1。

## 参考实例

```lua
local TM_Owner = Pet.GetOwner(_pet);
if TM_Owner ~= -1 then
    print("owner = " .. Char.GetData(TM_Owner, %对象_名字%));
end
```
