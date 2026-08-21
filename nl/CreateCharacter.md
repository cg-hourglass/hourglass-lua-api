<!-- Generated. DO NOT EDIT. -->
# CreateCharacter

## NL.CreateCharacter(Cdkey, Dataplace, Name, Img, Faceimg, Vital, Str, Tgh, Dex, Magic, Earth, Water, Fire, Wind)

### 函数功能

异步在指定帐号的指定栏位创建一个游戏角色，结果通过固定名回调函数返回。

### 参数说明

- Cdkey: [字符串](../appendix/字符串.md) 帐号（cdkey），长度必须小于 32 字节。
- Dataplace: [数值型](../appendix/数值型.md) 角色栏位，0 或 1。
- Name: [字符串](../appendix/字符串.md) 角色名，长度 1 到 31 字节，且不能命中服务器的名字黑名单。
- Img: [数值型](../appendix/数值型.md) 角色形象图档编号。
- Faceimg: [数值型](../appendix/数值型.md) 头像图片编号。
- Vital: [数值型](../appendix/数值型.md) 五维之体力。
- Str: [数值型](../appendix/数值型.md) 五维之腕力。
- Tgh: [数值型](../appendix/数值型.md) 五维之强度。
- Dex: [数值型](../appendix/数值型.md) 五维之速度。
- Magic: [数值型](../appendix/数值型.md) 五维之魔法。
- Earth: [数值型](../appendix/数值型.md) 地属性点数。
- Water: [数值型](../appendix/数值型.md) 水属性点数。
- Fire: [数值型](../appendix/数值型.md) 火属性点数。
- Wind: [数值型](../appendix/数值型.md) 风属性点数。

### 返回值

返回1表示请求已成功入队，返回0表示未入队（角色名不合法、形象非法、五维不满足建号条件、队列已满或未接入异步执行器）。这只代表指令发出成功，建号结果要通过 CreateCharacterCallback 获取。

## CreateCharacterCallback(cdkey, dataplace, regist, ret)

### 参数说明

- cdkey: [字符串](../appendix/字符串.md) 发起创建时传入的帐号，由引擎传回。
- dataplace: [数值型](../appendix/数值型.md) 角色栏位，由引擎传回。
- regist: [数值型](../appendix/数值型.md) 角色的 regist number，由引擎传回。
- ret: [数值型](../appendix/数值型.md) 创建结果。1 表示成功，其它值表示失败。由引擎传回。

### 返回值

无返回值，引擎不读取本函数的返回值。

## 参考实例

```lua
NL.CreateCharacter("testuser", 0, "小明", 100530, 30840, 6, 5, 5, 5, 4, 3, 3, 3, 3);

function CreateCharacterCallback(cdkey, dataplace, regist, ret)
  if(ret == 1)then
    print("帐号"..cdkey.."的第"..dataplace.."个角色创建成功");
  end
end
```

### 备注

回调函数名是固定的全局名 CreateCharacterCallback，需要脚本自行在入口文件里定义；引擎按名字查找，没定义就静默跳过。
同步校验按这个顺序进行：角色名长度、名字黑名单（含 "|"、"\\"、"[GM"、"gm"、"GM" 等片段以及本地化的屏蔽词）、形象编号、五维分配。任一步不通过都直接返回 0，不会入队。
角色名的长度上限按 UTF-8 字节数计量（不是脚本编码的字节数），因为它还必须完整存进角色结构里的定长字段。
请确保五维属性满足建号条件，否则只会建号失败。
