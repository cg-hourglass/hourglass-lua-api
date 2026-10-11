<!-- Generated. DO NOT EDIT. -->
# RegBattleSkillExpEvent

## NL.RegBattleSkillExpEvent(Dofile, FuncName)

### 函数功能

注册对象获得战斗技能经验时触发的 Lua 函数，可以改写实际获得的技能经验。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## GetBattleSkillExpEventCallBack(CharIndex, SkillID, Exp)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 获得技能经验的玩家对象index，由引擎传入。
- SkillID: [数值型](../appendix/数值型.md) 技能 ID，由引擎传入。
- Exp: [数值型](../appendix/数值型.md) 服务器算出的技能经验值，由引擎传入。

### 返回值

返回新的技能经验值。不想改动就返回 Exp，或者不写 return（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegBattleSkillExpEvent(nil, "MyBattleSkillExpEvent");

function MyBattleSkillExpEvent(CharIndex, SkillID, Exp)
  return Exp * 2; -- 战斗技能经验双倍
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
只对玩家触发（宠物和 NPC 在进入 Lua 之前就被过滤掉）。两个触发点分别对应抗性类技能与战斗技能、气力的经验结算。
