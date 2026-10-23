<!-- Generated. DO NOT EDIT. -->
# EncodeMovie

## Chess.EncodeMovie(A, B, Seed, Viewer, Opts)

### 函数功能

模拟对战并编码成某一方视角下客户端原生战斗动画的 C|/M| 回合序列。

### 参数说明

- A: [表](../appendix/表.md) 甲方棋盘，格式同 Chess.Simulate。
- B: [表](../appendix/表.md) 乙方棋盘。
- Seed: [数值型](../appendix/数值型.md) 随机种子，同 Chess.Simulate。
- Viewer: [数值型](../appendix/数值型.md) 观看者所在方，0 为甲方、1 为乙方；观看者的单位排在下方（槽 0~9）。
- Opts: [表](../appendix/表.md) 可选。Chess.Simulate 的全部选项；另有 max_script_bytes 为单个 M| 的字节上限（默认 4095），超出时一个模拟回合拆成多个播放回合；name_fallback 为服务端编码无法表示的单位名的替代名（省略时遇到这种名字抛出错误）。

### 返回值

数组，每项为 {bc, m, sim_round, part}：bc 为该播放回合的阵型包，m 为动画脚本（以 FF| 结尾），sim_round 为对应的模拟回合（从 1 起），part 为该回合内的分片序号（从 0 起）。

## 参考实例

```lua
local movie = Chess.EncodeMovie(boardA, boardB, 42, 0);
print(#movie, movie[1].m);
```

### 备注

只用原生 SKL 记录（普攻、属性魔法、补血、复活），不含 ACT/CHT。单位一律标成玩家类型：被击倒时倒地并以尸体留在场上，后续回合以死亡状态保留在阵型中。
MP 恢复与指挥官技能没有自己的动画记录：每个播放回合开头的阵型（C|）带上回合开始时的血量（含 round_heal 的回血）与 MP，first_turn 体现为记录顺序。
Viewer 不是 0 或 1 时抛出参数错误，其余错误同 Chess.Simulate。
