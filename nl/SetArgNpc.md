<!-- Generated. DO NOT EDIT. -->
# SetArgNpc

## NL.SetArgNpc(NpcIndex, NewArg)

### 函数功能

修改一个 Lua 创建的 NPC 的参数，并让它按新参数重新初始化。

### 参数说明

- NpcIndex: [数值型](../appendix/数值型.md) NPC 的对象index，一般是 NL.CreateArgNpc 或 NL.CreateNpc 的返回值。
- NewArg: [字符串](../appendix/字符串.md) 新的 NPC 参数字符串，即 npc.txt 里每个 NPC 最后那一组参数。

### 返回值

成功返回0。失败返回负数：-5 表示参数超过 512 字节，或该 index 不是 Lua 创建的 NPC；-3 表示重新执行初始化函数失败。

## 参考实例

```lua
local ret = NL.SetArgNpc(TestNPC, "100|100|3|10146|10147|10148|10149|10150|10151|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|1|0|0|0|0|0|0|15204|");
NLG.SystemMessage(CharIndex, "新npc参数设置返回值"..ret);
```

### 备注

参数长度上限是 512 字节，按脚本编码（GBK 或 BIG5）计量。
改完参数后 NPC 会自动重新执行初始化函数；如果此刻正好有玩家在与该 NPC 交互，可能出现异常，建议先隐藏 NPC 再改。
只对 Lua 创建的 NPC 生效（NL.CreateNpc / NL.CreateArgNpc 的产物）；对数据文件生成的 NPC 调用会返回 -5 并记一条日志。
