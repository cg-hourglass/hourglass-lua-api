# 说明

Agent 库管理**代理角色**（agent character）：一种没有帐号、没有客户端连线，由脚本代为操控的玩家角色。引擎只提供角色本身的存取、召出与收回、战斗兜底这些通用机制；代理角色用来做什么（陪练队友、驻守采集、跑腿……）完全由脚本决定，引擎不解释。

## 什么是代理角色

代理角色是一个完整的玩家角色：它与真人玩家走同一套战斗、经验、技能经验、升级、受傷、掉魂、卡時、背包、装备、宠物、队伍跟随和存档逻辑，只在下面几处被区别对待。

- **没有帐号，不能登录。** 它的帐号（`Cdkey`）由控制者、kind、key 确定性生成，以 `#a` 开头。以 `#` 开头的帐号、角色名对真人玩家保留：不能注册、登录、建角，`NL.CreateAccount`、`NL.CreateCharacter`、`NL.DeleteCharacter`、`Offline.OfflineLogin` 也一律拒绝。
- **必须绑定一名控制者。** 控制者是一个真人角色，创建时指定，之后不能更改。同一控制者、同一 kind、同一 key 只会有一个代理角色。
- **没有客户端连线。** 发给它的网络包是空操作；它不触发登录类事件，不登记名片，不发通讯录上线通知，不计入在线人数，玩家枚举和按名字找人都不会返回它；代理不占用名字，真人可以和它同名。
- **自定义数据（meta）。** 每个代理有一段最长 4096 字节的自定义数据，引擎原样保存，用 `Agent.GetMeta`、`Agent.SetMeta` 读写；控制者在线即可读写，不需要召出代理。建议只存 ASCII 内容。
- **kind 与 key。** 都是脚本自定的 ASCII 标签（kind 最长 16 字节，key 最长 32 字节，不能含空格和 `|`），引擎只保存不解释。

## 生命周期

引擎只区分三种状态，由 `Agent.Info` 的 `state` 字段给出：

| 状态 | 含义 | 可以做的事 |
|---|---|---|
| `body` | 只存在于数据库里：控制者在线时可以读到登记信息和身体摘要，但不在地图上 | `Agent.Info`、`Agent.List`、`Agent.GetMeta`、`Agent.SetMeta`、`Agent.Spawn`、`Agent.Delete` |
| `spawning` | 正在读取完整角色数据，最多 30 秒 | 再次 `Agent.Spawn` 返回 `ONLINE`，`Agent.Delete` 返回 `SPAWNING` |
| `spawned` | 已经出现在地图上，可以被 `Char.*`、`Battle.*`、`Item.*`、`Pet.*` 等接口像普通玩家一样操作 | 除 `Agent.Delete` 外的全部接口 |

状态转换：

- `Agent.Create` 创建 `body` 状态的代理；`Agent.Spawn` 把它变成 `spawning`，读档完成并放置到地图上后变成 `spawned`，结果通过 `NL.RegAgentSpawnEvent` 送达；读档失败、找不到落点、名额不足或 30 秒超时，都会回到 `body` 并以相应的结果码触发同一个事件。
- `Agent.Despawn` 或引擎自己的收回（控制者不在场、为真人让出名额、GM 操作）把 `spawned` 变回 `body`：先触发 `NL.RegAgentDespawnEvent`，再存档并离开地图。事件的第四个参数 InParty 告诉脚本代理被收回时是否还在控制者的队伍里；因为控制者登出会先解散队伍，原因为 `controller` 时它取的是控制者最后一次在场时的状态。
- **`spawned` 状态不跨服务器重启。** 重启之后没有任何代理在场，需要脚本重新召出。崩溃时最多回到最近一次定期存档或 `Char.Save` 的状态。
- 召出时读取的是与真人登录同一份完整数据（物品、宠物、技能、Field、通讯录、染色、头像），收回时与真人登出一样存档，所以代理的数据不会因为召出收回而丢失。召出期间代理进入定期存档；需要立刻落盘时用 `Char.Save`。
- 登出掉落的道具也按真人登出的规则处理：不论收回原因，收回事件之后、存档之前，引擎把它们丢在代理身边的地面上（带丢弃消失标志的直接消失），存档与下次召出都不再有它们；丢不出去的（例如代理阵亡）留在存档里，下次召出时再丢一次。借给代理的装备不受影响，因为 `Char.Transfer` 本来就拒绝转移这类道具（`UNTRADABLE`），受影响的只有代理自己拾取的道具。
- 召出需要空闲的玩家名额：剩余名额少于配置项 `agent.reserve_player_slots`（默认 10）时 `Agent.Spawn` 返回 `FULL`。真人登录永远不会因为代理占名额而被拒：名额已满时，引擎会先收回一个代理（收回原因 `capacity`），优先选不在任何队伍里的，其次选不在战斗中的，最后选最近召出的。

## 控制者在场

**代理角色只在它的控制者在场时存在。** 「在场」指控制者的**同一次登录**还在世界里，并且没有进入离线挂机或离线摆摊。只要不满足，引擎会在一个服务器循环内（约 100 毫秒）收回它的全部代理，收回原因 `controller`，不论代理当时在做什么：

- 控制者登出、断线、被踢，或者进入离线挂机、离线摆摊；
- 控制者在两次循环之间登出又重新登录——登录次数不同，仍然视为不在场，被收回；
- 控制者再次登录**不会**让代理恢复到 `spawned`：引擎不会自动召出任何代理，脚本需要在控制者登录后自己决定要不要重新召出。

由此得到的脚本规则：

- 受控代理只能加入控制者的队伍，永远不当队长；
- 想让代理在控制者离线时继续存在，是不可能的，这是引擎的保证，不是可以配置的选项；
- 在 `NL.RegAgentDespawnEvent` 里把「下次登录要不要自动召回」之类的状态写进 meta，再在控制者登录事件里读出来重新召出；InParty 为 0（例如控制者逃跑后队伍已解散再登出）时，代理在控制者离开前就已经不在队伍里，通常不应自动召回。

## 事件：哪些会触发，哪些不会

代理角色走的是玩家的完整逻辑，所以大多数对玩家生效的事件同样会对它触发。脚本需要区分时，用 `Agent.IsAgent(CharIndex)` 判断。

| 不会触发 | 会触发 |
|---|---|
| 登录类事件：Login、Logout、Drop、LoginGate、GetLoginPoint；Talk（代理不会说话）；任何依赖客户端网络包的事件 | BattleStart、BattleExit、BattleOver、AfterBattleExit、GetExp、BattleSkillExp、ProductSkillExp、FPConsume、LevelUp、PetLevelUp、Warp、DamageCalc 等战斗内事件、EquipChanged、PetGained、Party（`Agent.JoinParty` 的加入与 `Char.DischargeParty` 的离队，两者都可以被事件否决） |

注意：

- `Agent.IsAgent` 返回的是 0 或 1，而 0 在 Lua 里是真值，判断要写 `== 1`。
- BattleExit 的 ExitType 在战斗正常结束时也可能是逃跑类型，不要用它判断角色是不是逃跑了。
- 代理名下的宠物战后经验，按宠物当前主人（代理）的卡時状态计算，与真人宠物的规则相同。
- 为真人写的奖励类事件（例如战后奖池）如果不希望代理参与，需要自己在处理函数里用 `Agent.IsAgent` 排除。

## 战斗指令回调

代理没有客户端替它选择指令，所以每个回合由脚本通过 `NL.RegAgentBattleCommandEvent` 注册的回调来下达；引擎保证战斗不会被代理卡住。

**触发规则**

- 每个代理每回合恰好触发一次回调（第 0 回合也触发），代理本人和它的出战宠物共用这一次；回调参数里的 `CharIndex` 永远是代理本人，即使只剩宠物需要下指令。
- 回调在同场所有真人玩家都已下达指令（或已无法下达）之后才触发，所以代理不会增加回合等待时间。离线挂机的真人玩家如果还没下达指令，代理的回调也会等待，与现有的战斗超时规则一致。
- 回调里可以直接用 `Battle.ActionSelect`、`Battle.PetActionSelect`、`Battle.UseTechById` 为代理本人和它的出战宠物下达指令；`Battle.UseTechById` 返回 1 表示指令已经提交，返回 0 表示没有提交成功。

**兜底（回退指令）**

回调结束后，代理名下仍然没有下达指令的一方，由引擎代为提交：

- 代理活着：防御（没有出战宠物时提交两次）；代理已倒下：空指令；
- 出战宠物活着：防御；宠物已倒下：空指令。

没有注册回调时，每个回合每个代理都直接走兜底。以下情况也走兜底：回调抛出错误、超出指令预算、该代理的回调已被停用、本次服务器循环的合计预算已用完。兜底的防御与真人的防御一样会计入防御次数。

**指令预算**

| 层 | 限制 | 超出时 |
|---|---|---|
| 单次回调 | 约 10 万条虚拟机指令 | 回调被中止，本次走兜底 |
| 每个服务器循环（约 100 毫秒）合计 | 约 100 万条，战斗指令回调与 `NL.RegSecondTickEvent` 回调共用 | 本循环剩余的代理不再调用脚本，直接走兜底；秒回调在预算用完时本秒跳过 |
| 连续超出 | 同一代理连续 3 次超出单次预算 | 停用该代理的回调，之后每回合直接走兜底，直到它被收回再召出；`Agent.Info` 的 `ai_disabled` 为 1 |

预算**只用来防止脚本缺陷造成卡服，不能防止恶意脚本**：调试库（`debug`）是开放的，脚本可以用 `debug.sethook` 换掉计数钩子；回调开始前创建、回调内恢复运行的协程也不计入预算。预算超出时回调会被中止，即使脚本用 `pcall` 包住也无法继续执行。

## 调用上下文（CONTEXT）

有些接口不能在特定的处理阶段里调用，否则返回 `nil, "CONTEXT"`：

| 当前阶段 | 返回 `CONTEXT` 的接口 |
|---|---|
| 战斗处理阶段：代理战斗指令回调，以及 BattleStart、BattleExit、BattleOver、AfterBattleExit 等战斗内事件的处理函数 | `Agent.Spawn`、`Agent.Despawn`、`Agent.Delete`、`Char.Transfer` |
| `NL.RegAgentDespawnEvent` 的回调里 | 上面四个，加上 `Char.Save`（收回本身就会存档） |

`Char.Save` 在战斗阶段可以调用，存档是快照，与战斗不冲突。`Agent.SetMeta` 在任何阶段都可以调用，包括收回回调里，用它记录收回前的状态。

需要在战斗相关事件里触发这些操作时，把意图记在脚本自己的变量里，等 `NL.RegSecondTickEvent` 的回调再执行。

## 模式是脚本状态

引擎只知道代理是 `body`、`spawning` 还是 `spawned`。「随队」「驻守」「访问」这类**模式**是脚本自己的簿记，服务器不存储、不解释，也不会因为模式不同而区别对待：

- 随队：代理在控制者的队伍里跟随并参加战斗；
- 驻守：代理不在队伍里，停在某个格子上运行一个工作循环；
- 访问：代理不在队伍里，被短暂召出做一件事（例如取回物品）后马上收回。

对所有模式，引擎的保证完全一样：

1. 控制者不在场就收回，驻守也不例外；
2. 代理只能加入控制者的队伍；离队之后它仍然是代理，拒绝规则照常生效（其他玩家无法邀请它；它的决斗开关恒为关，原生决斗不能直接挑战它）。决斗是否允许代理参与由配置项 `agent.allow_duel` 决定（默认 `false`）：关闭时，任一参战者是代理或其队伍里有代理，决斗就被拒绝（提示「隊伍中有夥伴，無法決鬥」，`Battle.PVP` 返回 -4）；打开时，有代理的队伍照常决斗，`Battle.PVP` 也可以直接以代理为对手，代理按回合回调出手，决斗点数与真人相同。无论开关如何，代理都不进决斗排行榜；
3. 为真人让出名额时，只看「是否在队伍里」和「是否在战斗中」，不看脚本认为的模式；
4. 周期存档包含代理，脚本可以随时 `Char.Save`；
5. 脚本的秒回调和战斗回调共享同一份指令预算。

因此脚本应当：

- 把模式放在自己的表里，以代理的 `Cdkey` 为键，并在 `NL.RegAgentDespawnEvent` 里清理；
- 只在 meta 里保存**需要跨登录保留**的内容（例如「下次登录是否自动召回」）；不要保存「正在运行」之类只在 `spawned` 期间有意义的状态，因为服务器重启后没有代理在场；
- 脚本被重新加载（进程没有重启）时，用 `Agent.ListSpawned` 重建自己的簿记，再根据代理的位置、队伍状态和 meta 恢复模式；
- 判断「代理在不在战斗中」时，把任何不处于空闲的战斗状态都当作战斗中，不要在战斗收尾阶段做楼层或队伍检查——被秒杀的代理会留在队伍里，而队长的战斗可能还在继续。

## 工作循环约定

驻守采集、驻守制作这类「让一个已召出、不在队伍里的代理反复做同一件事」的玩法，建议用一个统一的工作循环约定来写。引擎本身不提供循环、调度、停工判断和报告，这些都在脚本里，运行在 `NL.RegSecondTickEvent` 的回调中，所以受上面说的合计指令预算限制。

一个「工作」由 `start` 与 `step` 两个函数描述，驱动器不关心具体做什么：

```lua
-- A work kind: the driver never knows what a kind does.
local kind = {
  -- Returns true, or nil, reason. w.spec is the caller's spec.
  start = function(w) return true end,
  -- Returns the seconds until the next step, or nil, stop_reason.
  step = function(w, now) return 6 end,
}
-- w = { ci, cdkey, owner, kind, spec, started, next_at, stats = {}, state = "running" | "stopped" }
```

驱动器的规则：

1. 每次 `step` 之前先确认 `Agent.Get(w.cdkey) == w.ci`，不一致就以 `"EXTERNAL"` 停工（对象 index 可能被复用）；
2. 每个服务器循环最多执行 8 个 `step`，其余的留到下一个循环；
3. `step` 抛出错误时以 `"ERROR"` 停工并记录日志，不影响其它工作；
4. 停工不会收回代理，接下来怎么处理由调用方决定；
5. 工作结束时产出一份报告：`{ kind, spec, started, ended, stop, stats }`；
6. 控制者离开时，在 `NL.RegAgentDespawnEvent` 里结束工作，把报告写进 meta，等控制者下次登录时告诉他；不要在登录后自动回到工作地点——每一班工作都应当由控制者在现场开始。

新增一种工作只需要新增一个 kind 表；驱动器本身不需要改动。

## 用 Agent.UseTech 写采集工作

驻守采集的 `step` 里，用 `Agent.UseTech` 做一次采集尝试。它只做一次、不移动、不循环，间隔、停工和报告仍由上面的驱动器负责。

要点：

- 只支持采集类技能（伐木、狩猎、挖掘、采伐）；
- 采集操作间隔与玩家相同（普通 6 秒，宠物协助 4 秒），每个代理单独计时，不受反作弊开关影响；间隔未到时返回 `reason == "GATE"`，不算失败；
- 代理站在哪里就在哪里采集。要判断某个格子能不能采，用 `Data.TechAreaAt`；
- 服务器不会广播采集动作，需要动画或头顶图标时，脚本自己调用 `NLG.SetHeadIcon`。

```lua
-- A gather step: one attempt, then map the reason to "next step" or "stop".
local gather = {
  start = function(w)
    if Agent.IsAgent(w.ci) ~= 1 then return nil, "NOT_AGENT" end
    return true
  end,
  step = function(w, now)
    local r, code = Agent.UseTech(w.ci, w.spec.skill);
    if r == nil then
      return nil, code;                   -- NOT_AGENT / CONTROLLER / NO_SKILL / ...
    end
    local reason = r.reason;
    if reason == "OK" or reason == "FAILED" or reason == "FP_VETO" then
      w.stats.tries = (w.stats.tries or 0) + 1;
      if r.item then
        w.stats.items = (w.stats.items or 0) + r.item.count;
      end
      return 6;
    elseif reason == "GATE" then
      return 1;                           -- too early, not a failure
    end
    return nil, reason;                   -- BAG_FULL / NO_FP / NO_AREA / STATE
  end,
}
```

## 治疗 NPC 与代理

医生（受傷）、精神治疗师（掉魂）和收费治疗师这三类治疗 NPC，会在对话者控制着代理时多出一步，让对话者选择要治疗谁。**这些行为是引擎内置的，脚本不需要做任何事。**

- 对话者在队伍里带着自己已召出的代理（同楼层、双方都不在战斗中）时，医生和精神治疗师先显示选择窗口「請選擇治療對象」，每一行是一个候选者的名字、受傷和掉魂；精神治疗师只列出有掉魂的候选者。选定之后，原有的窗口、价格和治疗都作用在选中的对象上，**费用由对话者付**。选中的对象在后续步骤里每一步都会重新检查，离队、进入战斗或被收回时中止，不扣费也不治疗；
- 收费治疗师的菜单不会发给代理队员；它的 LP、FP+LP 和宠物治疗确认，会连同对话者名下的代理一起治疗，价格是各自原价之和。总价付不起时，只治疗对话者本人并提示一条系统消息；
- 对话者没有带代理时，所有治疗 NPC 显示的窗口与原版完全一致；
- 治疗受傷和除掉魂的道具可以对自己名下的代理使用，效果与对玩家使用相同，代理的属性和队伍参数会随之刷新。

## 例子

```lua
-- Create a resting agent for a player, then bring it to the player's side and into the party.
NL.RegAgentSpawnEvent(nil, "OnAgentSpawn");
NL.RegAgentDespawnEvent(nil, "OnAgentDespawn");
NL.RegAgentBattleCommandEvent(nil, "OnAgentCommand");

function OnAgentSpawn(cdkey, charIndex, code)
  if code == "OK" then
    Agent.JoinParty(charIndex);
  end
end

function OnAgentDespawn(cdkey, charIndex, reason, inParty)
  -- Only Agent.SetMeta may write here; return at the next login only if the
  -- agent was still in the party when the controller left.
  if reason == "controller" and inParty == 1 then
    Agent.SetMeta(cdkey, "active=1");
  else
    Agent.SetMeta(cdkey, "active=0");
  end
end

function OnAgentCommand(charIndex, battleIndex, turn)
  -- Commit commands for the agent and its battle pet; anything left open is
  -- filled with a guard command by the server.
end

function Recruit(player)
  local cdkey = Agent.Create({
    controller = player,
    kind = "ally", key = "scout",
    name = "Scout",
    job = 452, level = 5, tribe = 0,
    image = 100027, face = 34000,
    element = { earth = 10, water = 0, fire = 0, wind = 0 },
    bp = { vit = 12, str = 10, tgh = 10, qui = 8, mgc = 12 },
  });
  if cdkey ~= nil then
    Agent.Spawn(cdkey, { near = player });
  end
end
```
