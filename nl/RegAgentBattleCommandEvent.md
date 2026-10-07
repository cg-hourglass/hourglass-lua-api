<!-- Generated. DO NOT EDIT. -->
# RegAgentBattleCommandEvent

## NL.RegAgentBattleCommandEvent(Dofile, FuncName)

### 函数功能

注册每回合为战斗中的代理角色下达指令的 Lua 函数。

### 参数说明

- Dofile: [字符串](../appendix/字符串.md) 要加载的脚本文件名；引擎会先 dofile 这个文件再写入事件槽。处理函数就在当前文件时传 nil 即可。 [可为空]
- FuncName: [字符串](../appendix/字符串.md) 触发时调用的全局 Lua 函数名；名字在触发时才解析。传 nil 即清空该事件槽。 [可为空]

### 返回值

注册状态码。1 表示注册成功；-1 表示 FuncName 不能转成字符串，槽位已被清空；-2 表示名字已写入槽位但当前还不是函数。

## AgentBattleCommandCallBack(CharIndex, BattleIndex, Turn)

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 代理本人的对象index（即使只剩宠物需要下指令，也是代理本人）。
- BattleIndex: [数值型](../appendix/数值型.md) 战斗index。
- Turn: [数值型](../appendix/数值型.md) 当前回合数，从 0 开始。

### 返回值

无

## 参考实例

```lua
NL.RegAgentBattleCommandEvent(nil, "MyAgentBattleCommandEvent");

function MyAgentBattleCommandEvent(CharIndex, BattleIndex, Turn)
  -- 用 Battle.ActionSelect / Battle.PetActionSelect / Battle.UseTechById
  -- 为代理本人和它的出战宠物下达本回合指令
end
```

### 备注

同一事件全局只有一个槽位，后注册者静默覆盖先注册者；名字按字节截断到 31 字节，以 `NULL` 开头的名字会被判定为未注册。
每个代理每回合恰好触发一次（第 0 回合也触发），代理本人和它的出战宠物共用这一次；在同场所有真人玩家都已下达指令之后触发。回调结束后仍未下达指令的一方由引擎代为防御；没有注册本事件时，代理每回合都由引擎代为防御。
回调带指令预算：单次最多约 10 万条虚拟机指令，超出时回调被中止（即使脚本用 pcall 包住也无法继续执行）；本事件与 `NL.RegSecondTickEvent` 在同一次服务器循环里合计最多约 100 万条，用完后本循环剩余的代理不再调用脚本。同一代理连续 3 次超出单次预算后，引擎停止为它调用本事件，直到它被收回再召出。预算只用来防止脚本缺陷造成卡服，不能防止恶意脚本：调试库开放，回调开始前创建的协程也不计入预算。
本函数是本服务端新增的接口，C 版 gmsv 没有。
