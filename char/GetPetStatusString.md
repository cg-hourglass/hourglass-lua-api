<!-- Generated. DO NOT EDIT. -->
# GetPetStatusString

## Char.GetPetStatusString(PetIndex)

### 函数功能

生成玩家携带的一只宠物的原生状态串，供扩展客户端的原生宠物详情浮框使用（摆摊扩展）。

### 参数说明

- PetIndex: [数值型](../appendix/数值型.md) 宠物的对象index，必须是某个玩家宠物栏里的宠物。

### 返回值

宠物状态串；宠物无效或不在玩家宠物栏里时返回 nil。
格式与摊位浏览下发的单只宠物段相同，只是去掉了开头的价格和栏位号：
`<宠物详细参数串><宠物附加参数串><升级点数>|<技能数(两位)>|<技能栏位>|<技能名>|...`，
前两部分与客户端收到的宠物详细参数、附加参数封包内容一致（各自以 `|` 结尾）。

## 参考实例

```lua
local status = Char.GetPetStatusString(Char.GetPet(player, 0));
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
