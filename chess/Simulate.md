<!-- Generated. DO NOT EDIT. -->
# Simulate

## Chess.Simulate(A, B, Seed, Opts)

### 函数功能

用图鉴棋局规则确定性地模拟两块棋盘的对战，返回胜负摘要。

### 参数说明

- A: [表](../appendix/表.md) 甲方棋盘，单位表数组（1~10 个）。单位表字段：name、image、level、star（1~3，默认 1）、lane（0~4）、row（0 前排 / 1 后排）、hp、max_mp、atk、mag、def、spd、element（"earth"/"water"/"fire"/"wind"/"none"）、skills（规则技能键数组，省略则只普攻）、mp_bonus（开场 MP 加成，非负，默认 0）、resist（{poison=, sleep=, drunk=}，各 0~100，从状态技能的成功率里扣除，100 即免疫）。开战时 MP 为 mp_start[star] + mp_bonus，不超过 max_mp；旧字段 skill、mp、mp_gain 会报错。
- B: [表](../appendix/表.md) 乙方棋盘，格式同 A。
- Seed: [数值型](../appendix/数值型.md) 随机种子，非负整数且不超过 2^53；同速单位的出手顺序与暴击由它决定。
- Opts: [表](../appendix/表.md) 可选。round_cap 为回合上限（默认 15），到达上限按剩余血量千分比判胜；mp_regen 为 1~3 星每个战斗回合开始时的 MP 恢复量（3 个整数，默认 {10, 15, 22}）；mp_start 为 1~3 星的开场 MP（3 个整数，默认 0）；mp_on_action 为每次非技能行动后回复的 MP，mp_on_hit 为受到敌方伤害且存活时回复的 MP（均为 0~1000，默认 0）；heal_below_pct 为补血门槛（1~100，默认 100：有友方低于该血量百分比才放补血）；overtime_round 为加时开始的战斗回合（0~99，默认 0 不加时），从该回合起第 k 个加时回合的所有伤害乘以 (100 + k × overtime_pct)%，补血（含 round_heal）除以同一系数（overtime_pct 0~1000）；evade_speed_pct 与 evade_max_pct（均 0~100，默认 0 关闭）为速度闪避：普攻的目标比攻击者快时，以 (速度差 ÷ 目标速度) × evade_speed_pct% 的概率闪避（不超过 evade_max_pct%），闪避不受伤害，魔法不能闪避；poison_pct 与 drunk_mp_pct（均 0~100）为中毒、醉酒每次结算扣的最大 HP、最大 MP 百分比（至少 1；中毒不会扣掉最后 1 点 HP）；skills 为 {技能键 = {effect, area, element, power, mp_cost, level, priority, status, chance, rounds, hits, miss, drain, cure, below}}，给出时整体替换默认技能集（effect = "melee"/"magic"/"heal"/"revive"/"status"/"status_attack"/"rider"/"combo"/"heavy"/"drain"/"focus"/"guard"/"counter"/"ward"/"dodge"/"assassin"，area = "single"/"cross"/"row"/"all"）。combo（連擊）为 hits（2~9）段各 power% 的普攻，目标倒下后余下段数转给下一个普攻目标；heavy（乾坤一擲）为一击 power% 的普攻，以 miss%（0~99）的概率直接落空；drain（吸血攻擊）为 power% 的普攻，按实际扣掉 HP 的 drain%（1~100）回复自身；focus（明鏡止水）在自身 HP 低于 below%（省略则用 heal_below_pct；补血技能同样可以给 below）时回复最大 HP 的 power%（至多 100），cure = true 时还会解除自身状态，有状态时即使 HP 充足也会施放。assassin 为 power% 的普攻，打敌方后排 HP 比例最低者（后排全灭则打前排），后排近战减伤照常。guard、counter、ward、dodge 是被动（不耗 MP、不计入 MP 池，每种每个单位最多一个）：guard（護衛）以 chance% 的概率替本车道和相邻车道的友方承受普攻，只受 power%（1~100）的伤害，每个战斗回合最多 hits（1~9）次，昏睡时不护卫；counter（反擊）在受到普攻且存活、未昏睡时以 chance% 的概率用 power% 的普攻还击，还击不会再被还击，被护卫拦下的普攻不还击；ward（魔法防禦）让本车道和相邻车道的友方受到的魔法伤害减少 power%（1~100），状态技能对他们的成功率再乘以 (100 − chance)%（chance 0~100），多个取最大值；dodge（陽炎）给普攻闪避率加上 chance%（不受 evade_max_pct 限制，不需要速度差）。状态技能（status 状态魔法、status_attack 带状态的普攻技能、rider 被动：普攻命中后附带状态）需要 status（"poison"/"sleep"/"drunk"）、chance（1~100，基础成功率）、rounds（1~9，持续的目标自身回合数）；status 与 rider 不带 power，rider 不耗 MP、不计入 MP 池，每个单位最多一个。一个单位同时只有一种状态；状态在持有者自己的回合开始时结算：中毒扣 HP、醉酒扣 MP 且期间行动和受击不回 MP、昏睡跳过行动且受到伤害即醒；playback = true 时结果多一个 playback 表（见返回值）；skill_priority 为 {技能键 = 优先级}（1~1000，覆盖默认的"按 MP 消耗"排序，决定 MP 满时先放哪个技能）；commanders 为 {组键 = {kind, rows, stat, pct}}，给出时整体替换默认的 melee / ranged / heal / magic 四组；commander_a、commander_b 为甲乙双方使用的组键（省略则无指挥官技能）。

### 返回值

表 {winner, rounds, hash, alive}：winner 为 0（甲胜）、1（乙胜）或 -1（平局）；rounds 为模拟回合数；hash 为规则集的 SHA-256 十六进制串；alive 为 {{甲方各单位是否存活...}, {乙方...}}，按输入顺序。opts.playback 为 true 时另有 playback = {rounds, frames, melee, magic, status}：甲方视角编码后的播放回合数、发包节奏用的帧数下界（60 Hz，100% 速度）、普攻类与施法类动画记录数，以及状态结算与解除的记录数。

## 参考实例

```lua
local r = Chess.Simulate(boardA, boardB, 42, {round_cap = 10});
```

### 备注

同样的棋盘、种子和规则总是得到同样的结果。
每个战斗回合开始时，每个存活单位恢复 mp_regen[star]（加上 mp_regen_mod 的百分比），不超过 max_mp。max_mp 至少为该单位最贵技能的消耗（不足时自动抬高）。轮到单位行动时，MP 未满就普攻；MP 已满时按优先级从高到低找第一个有合法目标的技能释放并扣除其消耗（补血要有掉血的友方，复活要有倒下的友方），都没有合法目标就普攻。
指挥官技能只有四种战斗类型：stat_mod（rows = "front"/"back"/"all"，stat = "hp"/"atk"/"mag"/"def"/"spd"，pct 为 -90~300 且不为 0）、first_turn（rows：这些单位在第 1 个战斗回合先于所有单位行动）、round_heal（pct 1~100：每个战斗回合开始时，存活且未满血的友方回复最大血量的 pct%，不超过上限）、mp_regen_mod（pct 1~500：全队每回合 MP 恢复加 pct%）。每种类型只接受自己用到的字段。经济类类型（periodic_card、sell_bonus、interest_cap、free_reroll）由 Lua 对局逻辑处理，这里会报错（已删除的 battle_start_heal 同样报错），这些组的玩家应传空的 commander。
棋盘为空、超过 10 个单位、同一格放两个单位、lane/row 越界、star 越界、未知属性或技能键、同一技能列两次、未知指挥官组、规则参数越界、种子非法时抛出错误。
