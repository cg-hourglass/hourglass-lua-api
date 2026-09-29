<!-- Generated. DO NOT EDIT. -->
# GetUUID

## Pet.GetUUID(PetIndex)

### 函数功能

获取宠物对象的全局唯一标识。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 目标宠物的对象index。

### 返回值

宠物的唯一标识字符串；对象不是宠物时返回字符串 "-1"。

## 参考实例

```lua
local TM_Uuid = Pet.GetUUID(_pet);
if TM_Uuid ~= "-1" then
    print("pet uuid = " .. TM_Uuid);
end
```

### 备注

返回值始终是[字符串](../appendix/字符串.md)，失败时是字符串 "-1" 而不是数值 -1，比较时要带引号。

宠物还没有唯一标识（现有值长度不超过 6 个字节）时，本函数会用 snowflake 算法生成一个新的
并写回宠物数据，因此第一次调用具有副作用。
