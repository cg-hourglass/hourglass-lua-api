<!-- Generated. DO NOT EDIT. -->
# CreateArgNpc

## NL.CreateArgNpc(Type, Arg, Name, Image, Map, Floor, Xpos, Ypos, Dir)

### 函数功能

直接创建 data/npc.txt 支持的各种内建类型 NPC，并传入该类型对应的参数。

### 参数说明

- Type: [字符串](../appendix/字符串.md) NPC 的类型名，如 "Itemshop2"、"healer"、"brushman"。
- Arg: [字符串](../appendix/字符串.md) 该 NPC 类型对应的参数，即 npc.txt 里每个 NPC 最后那一组参数。
- Name: [字符串](../appendix/字符串.md) NPC 显示出来的名字。
- Image: [数值型](../appendix/数值型.md) NPC 的图档编号。
- Map: [数值型](../appendix/数值型.md) NPC 所在的 map id。
- Floor: [数值型](../appendix/数值型.md) NPC 所在的 floor id。
- Xpos: [数值型](../appendix/数值型.md) NPC 所在的 x 坐标。
- Ypos: [数值型](../appendix/数值型.md) NPC 所在的 y 坐标。
- Dir: [数值型](../appendix/数值型.md) NPC 面朝的方向。

### 返回值

成功返回新 NPC 的对象index（正整数）。失败返回错误码：-1 表示坐标非法、类型名未知或取默认角色失败；0 表示没有空闲的角色槽位；-5 表示参数超过 512 字节；-3 表示初始化失败；-4 表示地面对象创建失败。

## 参考实例

```lua
local ret = NL.CreateArgNpc("Itemshop2", "150|100|3|10146|10147|10148|10149|10150|10151|1|1|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|14489|14479|14469|14459|14449|14439|14429|14419|14409", "贩卖卡片", 14508, 0, 1000, 235, 83, 1);
NLG.SystemMessage(CharIndex, "创建的npc的index为"..ret);
```

### 备注

注意错误码 0 与 -1 的区别：0 是“没有空闲角色槽位”，不是合法 index。
类型名按大小写不敏感匹配，写 "itemshop2" 与 "Itemshop2" 效果相同。
与 NL.CreateNpc 不同，本函数不会触发 RegNpcCreatedEvent，并且不占用 NPC 创建槽位表，这两点都沿袭旧版行为。
创建的 NPC 也算 Lua 创建的 NPC，可以用 NL.SetArgNpc 改参数、用 NL.DelNpc 删除。
