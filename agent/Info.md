<!-- Generated. DO NOT EDIT. -->
# Info

## Agent.Info(CdkeyOrIndex)

### 函数功能

获取代理角色的登记信息与身体摘要。

### 参数说明

- CdkeyOrIndex: 代理角色的账号（字符串），或已召出代理的对象index（数值）。

### 返回值

成功返回信息表，字段见说明。失败返回 `nil, 错误码`：`NO_AGENT` 没有这个代理（按对象index查询时表示它不是已召出的代理）；`NOT_LOADED` 代理的控制者不在线。

## 参考实例

```lua
local info = Agent.Info(cdkey);
if info and info.state == "spawned" then
  print(info.body.name .. " HP " .. info.body.hp);
end
```

### 备注

只读。信息表的字段：
- `cdkey`、`kind`、`key`：代理的账号与创建时的标签。
- `controller`：`{cdkey, regist}`，控制者的账号与角色编号。
- `controller_index`：控制者在场时的对象index，否则为 -1。
- `state`：`body` 未召出、`spawning` 正在召出、`spawned` 已召出。
- `char_index`：已召出时的对象index，否则为 -1。
- `ai_disabled`：1 表示代理的战斗指令回调因连续超出指令预算已被停用，收回再召出后恢复。
- `created_at`：创建时间（秒）。
- `body`：`{name, lv, job, image, hp, mp, inj, soul, fever_s, fever_on}`，分别是角色名、等级、职业、形象、HP、MP、受傷、掉魂、剩余卡時秒数、是否在打卡（1/0）。已召出时读自地图上的角色；未召出时读自上次收回或控制者登录时的摘要。`fp`、`hpm`、`mpm`、`fpm` 只有在代理召出过之后才有，服务器重启后缺失。
本函数是本服务端新增的接口，C 版 gmsv 没有。
