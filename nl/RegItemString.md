<!-- Generated. DO NOT EDIT. -->
# RegItemString

## NL.RegItemString(Dofile, FuncName, ItemSign)

### 函数功能

注册一个可以在 itemset 中使用的道具效果字段，道具触发该字段时会调用指定的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入注册表。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 被指向的全局 Lua 函数名；名字在触发时才解析，注册时不要求该函数已定义。超过 31 字节的部分会被截断。
- ItemSign: [字符串](../appendix/字符串.md) itemset 里对应的功能字段名。使用触发用 LUA_use 开头，初始化触发用 LUA_init 开头，装备触发用 LUA_att 开头，卸下触发用 LUA_det 开头。超过 31 字节的部分会被截断。

### 返回值

成功返回该条目落入的槽位号（0 到 127）；注册表已满返回 -1；ItemSign 已经注册过则返回 nil（并在日志里记一条重复注册的告警）。

## ItemUseCallBack(CharIndex, TargetCharIndex, ItemSlot)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 道具所有者的对象index，由引擎传入。
- TargetCharIndex: [数值型](../appendix/数值型.md) 道具使用目标的对象index；对自己使用时与 CharIndex 相同。由引擎传入。
- ItemSlot: [数值型](../appendix/数值型.md) 道具所在的栏位号，范围 8 到 27。由引擎传入。

### 返回值

返回0即可。引擎以 0 个返回值调用本函数，返回什么都不会被读取。

## 参考实例

```lua
NL.RegItemString("lua/myitem.lua", "MyItemUse", "LUA_useB1");

function MyItemUse(CharIndex, TargetCharIndex, ItemSlot)
  NLG.SystemMessage(CharIndex, "你使用了道具，栏位"..ItemSlot);
  return 0;
end
```

### 备注

注册表共 128 个槽位，全局共用且没有反注册接口，用掉的槽位不会释放。
ItemSign 与 FuncName 都按字节截断到 31 字节；重复检测比较的是“传入的完整 key”与“已存储的截断结果”，所以超过 31 字节的 key 既不会被判成重复，也永远无法在触发时匹配上——实际使用请把 key 控制在 31 字节以内。
触发时用来查表的 key 会先被截断到 63 字节再比较。
上面的 callback 小节描述的是 LUA_use（使用触发）。另外三种字段的处理函数形状如下：
LUA_init 初始化触发 —— ItemInitCallBack(ItemIndex)，只有一个道具对象index参数；
LUA_att 装备触发 —— ItemAttachCallBack(CharIndex, ItemIndex)；
LUA_det 卸下触发 —— ItemDetachCallBack(CharIndex, ItemIndex)。
四种触发在本服务端都是可用的，且 attach/detach 传入的是道具对象index而不是栏位号。
