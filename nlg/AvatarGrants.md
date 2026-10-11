<!-- Generated. DO NOT EDIT. -->
# AvatarGrants

## NLG.AvatarGrants(CharIndex)

### 函数功能

读取玩家或宠物的全部覆盖件解锁记录（衣橱），包括已经过期、引擎还没来得及删除的记录。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index，玩家或宠物。

### 返回值

一个从下标1开始的 Lua table，每个元素是 `{part = 覆盖件编号, source = 来源, expire = 到期时间}`，expire 是 Unix 秒，0 表示永久；没有记录时返回空 table；目标无效（或读取数据库失败）时返回 nil。

## 参考实例

```lua
local now, owned = os.time(), {};
for _, g in ipairs(NLG.AvatarGrants(player) or {}) do
  if g.expire == 0 or g.expire > now then
    owned[#owned + 1] = g.part; -- 已过期、引擎还没删除的记录不算
  end
end
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。解锁记录只是「拥有」，不会让覆盖件显示出来；显示哪些件由脚本合成后调用 NLG.SetAvatarParts。
在线玩家与其携带宠物的过期记录由引擎删除（限时道具同一个巡检循环，删除后触发 `NL.RegAvatarExpiredEvent`）；删除前读到的记录可能已经过期（例如同一秒内、离线期间到期、宠物仓库里的宠物），脚本应按 expire 过滤。宠物的记录跟着宠物本身走，换主人、存取公会仓库都保留；宠物消失时一并删除。
