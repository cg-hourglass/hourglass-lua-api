<!-- Generated. DO NOT EDIT. -->
# Create

## Agent.Create(Spec)

### 函数功能

为一名在场的玩家（控制者）创建一个代理角色，或补全一个已存在的代理角色。

### 参数说明

- Spec: [表](../appendix/表.md) 代理角色的规格表，字段见说明。

### 返回值

成功返回两个值 `Cdkey, Created`：Cdkey 是代理角色的账号（服务器编码的原始字节），Created 为 1 表示本次新建了角色数据、为 0 表示代理已存在。失败返回 `nil, 错误码`：`BAD_SPEC` 规格表缺字段、字段类型不对或数值不合法；`CONTROLLER` 控制者不在场；`DB` 写库失败。

## 参考实例

```lua
local cdkey, created = Agent.Create({
  controller = player,
  kind = "partner", key = "linke",
  name = "林克",
  job = 452, level = 5, tribe = 0,
  image = 100027, face = 34000,
  element = { earth = 10, water = 0, fire = 0, wind = 0 },
  bp = { vit = 12, str = 10, tgh = 10, qui = 8, mgc = 12 },
  fever_seconds = 0,
  skills = { { id = 225, lv = 1 } },
});
if cdkey == nil then
  print("创建失败：" .. created); -- 失败时第二个返回值是错误码
end
```

### 备注

同步执行：返回时角色数据与登记都已写库。
代理角色是没有帐号、没有客户端连线的玩家角色，绑定一名控制者，只在控制者在场（以同一次登录在世界中，且不处于离线挂机或离线摆摊）时才能召出。
Spec 的字段：
- `controller`（必填）：控制者的对象index，必须是在场的真人玩家。
- `kind`、`key`（必填）：ASCII 标签（可打印字符），分别为 1 到 16 和 1 到 32 字节，不能含空格和 `|`。引擎只保存不解释，可用 kind 区分玩法、key 区分同一玩法下的不同代理。
- `name`（必填）：角色名，不超过角色名长度上限；不检查重名，代理不占用名字。
- `job`、`level`、`tribe`、`image`、`face`（必填）：职业、等级（至少 1）、种族、形象与头像编号。
- `element`（必填）：`{earth, water, fire, wind}` 四项属性值，只校验非负，属性组合规则由脚本自行检查。
- `bp`（必填）：`{vit, str, tgh, qui, mgc}` 五项能力点数，与玩家建角时分配的点数同一单位，五项之和必须大于 0。
- `fever_seconds`（可选）：初始卡時秒数，默认 0。
- `skills`（可选）：`{ {id = 技能编号, lv = 等级}, ... }`，写入角色原生技能栏，技能经验取该等级的起点。每个技能必须存在、不重复，等级在 1 到该职业可学的上限之间，技能栏占用合计不超过技能栏上限（默认 10），否则返回 `BAD_SPEC`。
Cdkey 由控制者、kind、key 确定性生成：同一控制者以相同 kind 与 key 重复调用总是得到同一个代理，不同控制者之间不会冲突。代理已存在时只补全缺失的那一步，并返回 Created = 0，所以中途失败后重新调用即可修复。
代理不能登录，以 `#` 开头的账号与角色名对玩家保留。召出后可以用 `Char.AddSkill` 为代理追加技能。
本函数是本服务端新增的接口，C 版 gmsv 没有。
