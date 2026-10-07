<!-- Generated. DO NOT EDIT. -->
# AvatarRevoke

## NLG.AvatarRevoke(CharIndex, Part, Source)

### 函数功能

删除玩家或宠物的覆盖件解锁记录。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index，玩家或宠物。
- Part: [数值型](../appendix/数值型.md) 覆盖件编号；传 0 表示删除该来源的全部记录。
- Source: [字符串](../appendix/字符串.md) 来源名，规则同 NLG.AvatarGrant。

### 返回值

成功返回 0（记录本来就不存在也返回 0）；目标无效、参数不合法或写入数据库失败时返回 -1。

## 参考实例

```lua
NLG.AvatarRevoke(player, 102, "mall");  -- 删除一条
NLG.AvatarRevoke(player, 0, "event");   -- 活动结束，删除该来源的全部记录
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。立即写入数据库。
