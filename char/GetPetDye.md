<!-- Generated. DO NOT EDIT. -->
# GetPetDye

## Char.GetPetDye(PetIndex)

### 函数功能

取玩家携带的一只宠物的染色记录，供扩展客户端在别人的宠物（如集市、摆摊的宠物行）上显示染色与幻彩。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 宠物的对象index，必须是某个玩家宠物栏里的宠物（离线摆摊的卖家同样适用）。

### 返回值

染色记录串；染色功能关闭（dye.enabled=false）、宠物没有染色、或宠物无效/不在玩家宠物栏里时返回 nil。
内容与服务端发给主人的 `DYM P` 记录完全相同（base64 记录串，带幻彩时为 v3 格式），客户端可直接按宠物染色记录解析。

## 参考实例

```lua
local dyeToken = Char.GetPetDye(Char.GetPet(player, 0));
if dyeToken then
    row.dye = dyeToken;
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。记录格式见 docs/dye.md §4。
