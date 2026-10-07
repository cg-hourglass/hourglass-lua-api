<!-- Generated. DO NOT EDIT. -->
# Transfer

## Char.Transfer(From, To, Spec)

### 函数功能

在两个在线玩家之间一次性单向转移道具、宠物、金币和卡時（打卡时间），作为一笔不可拆分的事务。

### 参数说明

- From: [数值型](../appendix/数值型.md) 给出方的玩家对象index。
- To: [数值型](../appendix/数值型.md) 接收方的玩家对象index。
- Spec: [表](../appendix/表.md) 转移内容，各字段都可省略（但至少要有一项）：
`items = { {slot = 12, to = 3}, ... }`：slot 是给出方栏位 0-27；to 是接收方背包栏 8-27、一个空的装备栏 0-7，省略表示放进第一个空背包栏；
`expect = { [12] = 20001 }`：给出方栏位 -> 道具ID，不一致时整笔拒绝（STALE）；
`pets = { 2, ... }`：给出方宠物栏 0-4；
`gold`：金币数；`fever`：卡時秒数；`tag`：写进审计日志的标签。

### 返回值

成功返回结果表：
`{ items = { {from = 12, to = 3, item = <道具index>}, ... }, pets = { {from = 2, to = 0}, ... }, gold = <实际转移的金币>, fever = <转移的秒数> }`。
失败返回 nil 和错误码，且**什么都没有转移**：
`BAD_ARGS`、`STATE`（任一方不可用，或在战斗、交易、摆摊中）、`STALE`（栏位已空或与 expect 不符）、
`UNTRADABLE`（登出掉落或丢弃消失的道具）、`NO_SPACE`、`CANT_EQUIP:<job|level|slot|weapon>`（目标装备栏非空或不能装备）、
`PET_LEVEL`、`PET_FULL`、`NO_GOLD`、`NO_TIME`、`FEVER_MAX`、`FEVER_DIR`、`SAVE`、`CONTEXT`。

## 参考实例

```lua
local r, err = Char.Transfer(owner, agent, {
    items = { { slot = 12, to = 3 } },
    expect = { [12] = 20001 },
    pets = { 2 },
    tag = "partner.equip",
});
if not r then
    print("transfer failed: " .. err);
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。

- 先在锁内校验全部条件，任何一条不满足就整笔拒绝。双方的战斗、交易、摆摊门控与 NLG.MoveItem 相同；绑定道具可以转移。
- 放进装备栏时，目标栏必须为空且接收方能装备这件道具（同 Item.CanEquip 的判断）；双手武器、盾牌与另一只手、两件同类饰品的冲突会以 `CANT_EQUIP:weapon` / `CANT_EQUIP:slot` 拒绝，而不是像手动换装那样自动调换。
- 宠物只落在接收方的携带栏，到达后是休息状态，需要时再用 Pet.SetStatus 设为出战。宠物等级比接收方高 5 级以上时拒绝（PET_LEVEL），**但代理角色把宠物交还给它的控制者时不受此限制**；反方向（控制者交给代理）照常检查。
- 金币按接收方的持有上限截断，多出的部分留在给出方；给出方金币不足时 NO_GOLD。
- 卡時**只能单向**：`fever > 0` 时接收方必须是给出方当前控制的代理角色，否则 FEVER_DIR（真人之间、代理交给控制者都拒绝）。秒数不够（NO_TIME）或会超过接收方上限（FEVER_MAX）时整笔拒绝，不截断。双方原本是否在打卡保持不变；给出方的卡時被转空时打卡自动结束。
- 成功后先同步保存给出方，再保存接收方。给出方保存失败时整笔回滚并返回 SAVE；接收方保存失败只推迟到下一次定期存档。因此同一件道具、同一只宠物在数据库中最多只出现一次。
- 每转移一件道具、一只宠物或一笔金币，在给出方名下写一条审计记录，动作是 `LuaTransfer:<tag>`。
- 在 AgentDespawn 回调里或战斗循环阶段（代理战斗指令回调、BattleExit 等）调用返回 CONTEXT。
