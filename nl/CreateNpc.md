<!-- Generated. DO NOT EDIT. -->
# CreateNpc

## NL.CreateNpc(Dofile, InitFuncName)

### 函数功能

用 Lua 脚本创建一个 NPC，并执行指定的初始化函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再解析初始化函数名。初始化函数就在当前文件时传 nil 即可。 [可为空]
- InitFuncName: [字符串](../appendix/字符串.md) NPC 创建后执行的初始化函数名，声明格式见下面的 InitCallBack。 [可为空]

### 返回值

成功返回新 NPC 的对象index（正整数）。失败返回错误码：-1 表示 NPC 创建槽位表已满或取默认角色失败；0 表示没有空闲的角色槽位；-2 表示 InitFuncName 没有解析成函数；-3 表示初始化回调失败（出错或返回了假值）；-4 表示地面对象创建失败。

## InitCallBack(CharIndex)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 新建 NPC 的对象index，由引擎传入。

### 返回值

必须返回真值（如 true）表示初始化成功；返回假值会让 NL.CreateNpc 失败并回收该 NPC，同时返回 -3。

## 参考实例

```lua
-- init.lua
if(TestNPC == nil)then
  TestNPC = NL.CreateNpc("lua/testnpc.lua", "MyCharInit");
end

-- lua/testnpc.lua
function MyCharInit(NpcIndex)
  return true;
end
```

### 备注

注意错误码 0：它表示“没有空闲角色槽位”，是失败，而不是一个合法的对象index。只判断“返回值小于 0 才是失败”会误判这一种情况。
新 NPC 先落在固定的出生点（map 0、floor 1000 的硬编码坐标），初始化回调里可以直接把它挪到目标位置。
创建成功后会同步触发 RegNpcCreatedEvent；在那个处理函数里再调用 NL.CreateNpc 会无限递归，引擎没有任何保护。
