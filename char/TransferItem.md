<!-- Generated. DO NOT EDIT. -->
# TransferItem

## Char.TransferItem(From, To, Spec)

### 函数功能

在两个已加载玩家或代理的背包之间按数量转移道具，保护来源和目标 allocation。

### 参数说明

- From: [数值型](../appendix/数值型.md) 给出方对象 index。
- To: [数值型](../appendix/数值型.md) 接收方对象 index；必须不同于给出方。
- Spec: [表](../appendix/表.md) 必填 slot、to（双方真实绝对背包栏位，不接受装备栏或 -1）、count（整数且 >=1）、ref（来源字符串）、to_ref（目标字符串，空栏必须显式传空字符串）；可选 expect_count 为来源预期数量。

### 返回值

验证失败返回 nil, code：BAD_ARGS、STATE、CONTEXT、STALE、UNTRADABLE、CONFLICT、NO_SPACE。
执行后返回 {from,to,moved,left,err,saved,from_saved,to_saved}；from/to 是实际栏位（未发布接收方时 to=-1），moved 为实际转移数量，left 为原来源 allocation 剩余数量。
err 为成功时空字符串、未满足全部请求的 PARTIAL、重入回调改变位置/数量/ownership 的 POST_CHANGED 或整组保存失败 SAVE_FROM；三个保存字段为 0/1，均取整组事务的保存结果。

## 参考实例

```lua
local r, err = Char.TransferItem(owner, agent, {
    slot = 12, to = 9, count = 3,
    ref = Char.GetItemRef(owner, 12),
    to_ref = Char.GetItemRef(agent, 9), expect_count = 8,
});
```

### 备注

使用实际背包容量及 native trade 限制（登出掉落、丢弃消失、不可宠物邮件），禁止不同类目标交换；native split/copy 与 merge 决定堆叠语义，目标容量不足时只移动可容纳数量。
战斗、死亡、确认交易、摆摊及 native inventory busy/resync 门控有效。
转移前耦合双方，完成数量及所有权变更后执行一次整组事务保存；失败不回滚内存，moved/left/to 仍反映已发生的转移，三个保存字段均为 0。任一组成员下次保存时整组重试，不应重放转移请求。
sync formatter 和 house collection 可执行重入回调；整组保存前后检查真实 allocation（包括 split 新 allocation），读回实际 from/to/left；moved 保留已经真实完成的转移数量。释放或相同 index/ID/count 的 allocation replacement 不会冒充原转移；矛盾 foreign ownership 时不保存整组，POST_CHANGED 要求重新读取库存并停止追加写入。
native house collection 在快照外执行并重新验证；受保护保存使用 without-house snapshot 路径，避免再次触发 house warp 回调。自身 Move 也只保存一次。
在 serialized runtime 调用。仅可信脚本可使用，业务授权和伙伴归属校验由调用方负责。保存同步执行，不宜高频调用。
