<!-- Generated. DO NOT EDIT. -->
# AvatarGrant

## NLG.AvatarGrant(CharIndex, Part, Source, Expire)

### 函数功能

为玩家或宠物记录一条覆盖件解锁（衣橱），同一件同一来源再次调用会覆盖到期时间。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index，玩家或宠物。
- Part: [数值型](../appendix/数值型.md) 覆盖件编号，1~65535。
- Source: [字符串](../appendix/字符串.md) 来源名，1~16 个字符，只能用小写字母、数字和下划线，例如 `"mall"`、`"scroll"`、`"event"`。
- Expire: [数值型](../appendix/数值型.md) 到期时间（Unix 秒）；0 表示永久。

### 返回值

成功返回 0；目标无效、参数不合法或写入数据库失败时返回 -1。

## 参考实例

```lua
NLG.AvatarGrant(player, 102, "mall", os.time() + 7 * 86400); -- 商城租用 7 天
NLG.AvatarGrant(player, 101, "gm", 0);                        -- 永久
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。立即写入数据库。同一目标的同一件可以来自多个来源，各自一条记录。
限时记录（Expire 大于 0）写入后即由引擎负责到期（见 `NL.RegAvatarExpiredEvent`），续期直接再调用一次即可。
