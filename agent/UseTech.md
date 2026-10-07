<!-- Generated. DO NOT EDIT. -->
# UseTech

## Agent.UseTech(CharIndex, SkillId, Opts)

### 函数功能

让已召出的代理角色用一项采集技能做一次采集。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 已召出代理的对象index。
- SkillId: [数值型](../appendix/数值型.md) 代理持有的技能 ID（不是 tech id），例如伐木、狩猎、挖掘、采伐对应的技能。
- Opts: [表](../appendix/表.md) 选项表。`tech` 为要使用的 tech id，省略（或 0）时用代理在该技能下已学会的、所需等级最高的采集 tech。`success_pct`（0–100）把这次采集的原生成功几率缩放为原来的百分之几：1–99 生效，省略、0 或 100 保持原生；被削掉的那部分按原生失败处理（照常消耗 FP，不得物品），超出范围返回 `BAD_ARGS`。`to` 和 `data` 是保留字段，只能省略、为 0 或为空字符串，否则返回 `BAD_ARGS`。 [可为空]

### 返回值

成功执行一次采集尝试（无论采到与否）时返回结果表；失败返回 `nil, 错误码`。

结果表字段：`done` 采集是否走完了结算（1 是，0 否）；`ok` 是否采到了物品（1 是，0 否）；`reason` 结果原因（见下表）；`item` 采到的物品 `{id, count}`，没有采到时没有这个字段；`exp` 获得的技能经验；`levelup` 技能是否升级（1 是，0 否）；`fame` 获得的声望；`fp` 这次实际消耗的 FP；`injury` 这次增加的受傷值。

`reason` 取值与工作循环的处理建议：

| reason | 含义 | 工作循环该怎么做 |
|---|---|---|
| `OK` | 采到了物品 | 记账，按间隔继续 |
| `FAILED` | 走完了结算但这次没有采到物品（命中了采集失败概率），已照常扣 FP、增加受傷 | 记账，按间隔继续 |
| `GATE` | 距离上一次采集不足间隔（见备注），本次没有执行，也没有消耗 | 不算失败，等到间隔后重试 |
| `BAG_FULL` | 背包没有空位 | 停工，通知控制者 |
| `NO_FP` | FP 不足 | 停工，或等 FP 恢复 |
| `NO_AREA` | 代理当前的格子上没有这项技能可采的区域，或区域里没有它的等级能采的物品 | 停工，或用 `Data.TechAreaAt` 找到区域后移动 |
| `FP_VETO` | FP 扣除被否决：物品和经验已经给出，FP 没有扣。`NL.RegFpConsumeEvent` 的回调只能改扣除量、不能否决，返回 0 时本次照常 `OK` 且不扣 FP，所以 Lua 回调不会触发这个码 | 产出计入统计，然后停工 |
| `STATE` | 其他原因没有走完采集（例如代理正处在不能采集的状态、区域没有可用概率、物品生成失败） | 停工并记录日志 |

错误码：`NOT_AGENT` 不是已召出的代理；`CONTROLLER` 控制者不在场；`NO_SKILL` 代理没有这项技能，或该技能下没有可用的采集 tech；`BAD_ARGS` 参数类型不对，或使用了保留字段；`CONTEXT` 当前上下文不允许调用。

## 参考实例

```lua
local r, code = Agent.UseTech(charIndex, skillId);
if r == nil then
  print("采集失败：" .. code);
elseif r.reason == "OK" then
  print("采到物品 " .. r.item.id .. " x" .. r.item.count);
elseif r.reason == "BAG_FULL" or r.reason == "NO_FP" then
  -- 停工
end
```

### 备注

同步执行，一次调用只做一次采集尝试，不循环、不移动、不选择地点；这些由脚本的工作循环负责。代理在哪个格子上就在哪个格子采集，采集所用的区域、概率、物品、经验、受傷、宠物协助等规则与玩家使用同一项技能时完全相同，脚本不能改写。
只支持采集类技能：路由函数为 `TECH_Lumb`、`TECH_Hunting`、`TECH_Mining`、`TECH_Cutting` 的 tech；其他 tech（制作、治疗、战斗技能等）一律视为没有可用 tech，返回 `NO_SKILL`。
采集有操作间隔：与玩家相同，普通 6 秒，带着宠物协助时 4 秒。间隔按每个代理单独计时，召出后的第一次尝试总是放行；它不受反作弊开关控制，被间隔拦下时只返回 `GATE`，不计作弊次数，也不会踢人。
采集过程会照常触发 `NL.RegFpConsumeEvent` 和 `NL.RegProductSkillExpEvent`，升级照常触发升级事件。
服务器不会替代理广播采集动作。需要让周围的玩家看到采集动画或头顶图标时，由脚本调用 `NLG.SetHeadIcon`。
不能在战斗处理阶段（包括代理战斗指令回调和各战斗事件回调）以及 `NL.RegAgentDespawnEvent` 的回调里调用，否则返回 `nil, "CONTEXT"`。
本函数是本服务端新增的接口，C 版 gmsv 没有。
