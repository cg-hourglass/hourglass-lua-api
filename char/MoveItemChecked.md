<!-- Generated. DO NOT EDIT. -->
# MoveItemChecked

## Char.MoveItemChecked(CharIndex, Spec)

### 函数功能

受 allocation 保护的自身装备或背包移动，返回 native 实际落点而非 attempted-success。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 已加载玩家或代理对象 index。
- Spec: [表](../appendix/表.md) 必填 slot、to（实际绝对携带栏位，且不同）、ref 与 to_ref 字符串；可选 expect_count 为来源预期数量。原生整件移动，不接受数量参数。

### 返回值

验证失败返回 nil, BAD_ARGS/STATE/CONTEXT/STALE/CONFLICT。
执行后结果同 TransferItem；to 是 native pairing 后的实际 destination（未移动为 -1），moved/left 是真实数量。
err 为成功时空字符串、PARTIAL、MOVE_REJECTED、POST_CHANGED（post-mutation callback 再次移动、释放或改变 ownership）或 SAVE_FROM；自身保存成功时三个保存字段都是 1。

## 参考实例

```lua
local source = Char.GetItemRef(player, 8);
local target = Char.GetItemRef(player, 9);
if source and source ~= "" and target then
    local result, code = Char.MoveItemChecked(player, {
        slot = 8, to = 9, ref = source, to_ref = target,
    });
    if not result then print("move failed: " .. code); end
end
```

### 备注

完整复用 native overlap、job/level、双手武器、饰品 pairing、crystal 与 attach/detach 管道；overlap 和装备等级 callback 后、原生第一次 mutation 前再次校验身份、数量和状态，并覆盖所有装备槽以保护 retarget sibling。
接口没有绕过原生换装限制。原生 swap 可以交换当前物品；原生 merge 可能只移动部分数量。
请求目标和实际目标可能不同，UI 必须重新读取自身携带栏。结果位置/ownership 在 attach/detach/equipChanged 执行后读回；post callback 引入矛盾 foreign ownership 时返回 POST_CHANGED 且不保存自身。保存失败不假回滚；业务归属授权由可信调用方执行。
