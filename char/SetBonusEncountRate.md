<!-- Generated. DO NOT EDIT. -->
# SetBonusEncountRate

## Char.SetBonusEncountRate(CharIndex, Rate)

### 函数功能

设置玩家的遇敌率修正值。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 玩家的对象index。
- Rate: [数值型](../appendix/数值型.md) 遇敌率修正值。

### 返回值

设置后的遇敌率修正值；对象不是玩家、或该玩家没有对应连接会话时返回 0。

## 参考实例

```lua
Char.SetBonusEncountRate(Player, 100);   -- 遇敌率翻倍
Char.SetBonusEncountRate(Player, -100);  -- 关掉遇敌
```

### 备注

名词解释：全局遇敌率 ger 是 ga_setup.cf 里的 encount_rate，默认 100；
遇敌率修正 cer 就是本接口设置的值；玩家实际遇敌率 er = ger + cer。
遇敌率基准值是 100，即 er 等于 100 时是系统制定的正常遇敌率。
er 小于等于 0 时玩家不会遇敌；er 为 200 时遇敌率是平时的两倍；er 为 30 时只有平时的三成。
注意这个参数做不出“步步遇敌”的效果，只是提高随机事件的成功率，
建议不要超过 500，否则会增加服务端的运算开销。
修正值保存在连接会话上，玩家下线后不会保留。
