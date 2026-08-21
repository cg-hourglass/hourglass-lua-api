<!-- Generated. DO NOT EDIT. -->
# RegTechOptionEvent

## NL.RegTechOptionEvent(Dofile, FuncName)

### 函数功能

注册读取技能附加参数（TECH_OPTION 字段）时触发的 Lua 函数，可以改写字段值。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## TechOptionCallBack(CharIndex, Option, TechID, Val)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 触发本次取值的对象index，由引擎传入。
- Option: [字符串](../appendix/字符串.md) TECH_OPTION 的字段标签，通常是 3 个字节（如 "AR:"、"SR:"），原样传递不做任何加工。由引擎传入。
- TechID: [数值型](../appendix/数值型.md) 当前技能的 tech ID，由引擎传入。
- Val: [数值型](../appendix/数值型.md) 服务器算出的字段值，由引擎传入。

### 返回值

返回新的字段值。不想改动就返回 Val（返回非数值时沿用服务器原值）。

## 参考实例

```lua
NL.RegTechOptionEvent(nil, "MyTechOptionEvent");

function MyTechOptionEvent(CharIndex, Option, TechID, Val)
  -- 10 级连击（TechID=9）：最少攻击次数 +2、最多攻击次数 +1、伤害 +20%
  if TechID == 9 then
    if Option == "AN:" then return Val + 2; end
    if Option == "AM:" then return Val + 1; end
    if Option == "DD:" then return Val + 20; end
  end
  return Val;
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
这是整套事件里触发最频繁的一个（全服共 85 处触发点），也是唯一带字符串参数的可改写事件；处理函数里不要做重活。
Val 传入时已经叠加过套装（ItemSuit）加成，脚本看到的是套装之后的值。
Option 的取值不要写死：除了 26 个字面量标签，还有三处动态来源，
其中舞步类技能的一组标签（"P1"…"N4"）没有结尾冒号。
