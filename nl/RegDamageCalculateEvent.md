<!-- Generated. DO NOT EDIT. -->
# RegDamageCalculateEvent

## NL.RegDamageCalculateEvent(Dofile, FuncName)

### 函数功能

注册战斗中计算伤害时触发的 Lua 函数，可以改写最终伤害值。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## DamageCalculateCallBack(CharIndex, DefCharIndex, OriDamage, Damage, BattleIndex, Com1, Com2, Com3, DefCom1, DefCom2, DefCom3, Flg)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 攻击者的对象index，由引擎传入。
- DefCharIndex: [数值型](../appendix/数值型.md) 防御者的对象index，由引擎传入。
- OriDamage: [数值型](../appendix/数值型.md) 未修正的原始伤害，由引擎传入。
- Damage: [数值型](../appendix/数值型.md) 服务器算出的修正后伤害（真实伤害），由引擎传入。
- BattleIndex: [数值型](../appendix/数值型.md) 当前战斗index，由引擎传入。
- Com1: [数值型](../appendix/数值型.md) 攻击者使用的动作编号，由引擎传入。
- Com2: [数值型](../appendix/数值型.md) 攻击者动作目标所在位置，由引擎传入。
- Com3: [数值型](../appendix/数值型.md) 攻击者动作对应的 tech ID，由引擎传入。
- DefCom1: [数值型](../appendix/数值型.md) 防御者使用的动作编号，由引擎传入。
- DefCom2: [数值型](../appendix/数值型.md) 防御者动作目标所在位置，由引擎传入。
- DefCom3: [数值型](../appendix/数值型.md) 防御者动作对应的 tech ID，由引擎传入。
- Flg: [数值型](../appendix/数值型.md) 命中类型。0 普通命中；1 暴击；2 未造成伤害；3 闪躲；4 防御。由引擎传入。

### 返回值

返回新的伤害值。不想改动就返回 Damage（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegDamageCalculateEvent(nil, "MyDamageCalculateEvent");

function MyDamageCalculateEvent(CharIndex, DefCharIndex, OriDamage, Damage, BattleIndex, Com1, Com2, Com3, DefCom1, DefCom2, DefCom3, Flg)
  -- 攻击者普通攻击、防御者恰好防御时伤害加倍
  if Com1 == 4 and Com3 == -1 and DefCom1 == 1 and DefCom3 == -1 then
    return Damage * 2;
  end
  return Damage;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
本事件是参数最多的一个（12 个参数），在普通攻击与法术伤害的各个环节共 8 处触发。
其中攻击序列里的两处（命中通知与闪躲通知）会丢弃返回值，把本事件当作纯通知使用，
所以无条件改写伤害时会发现有一部分答案被忽略。
