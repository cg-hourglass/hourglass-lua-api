# 说明

Field 库是一个三层的键值存储接口，用来给脚本保存自定义的角色/账号/全局数据。该设计最早参考自仙境传说 Athena 模拟器的 Global Reg Value 系统。

## Field 的命名规则（按名称首字符区分层级）

- 没有特殊字符开头的 Field，默认绑定当前触发该函数调用的这一个游戏角色（裸层，每角色最多 192 条）。
- `#` 开头的 Field，默认绑定目标账号下的角色（账号层，每账号最多 192 条；同一账号左右两个角色共享同一份数据）。
- `@` 开头的 Field，默认绑定整个服务器（全局层，进程内共 128 条，不区分账号/角色，调用时传入的 CharIndex 会被忽略）。

## Field 的保存规则

角色登录游戏时，服务端会一次性把该角色（裸层）与所属账号（账号层）的 Field 数据从数据库读入内存缓存；此后 `Field.Get`/`Field.Set` 只读写这份内存缓存。缓存会在角色存档（定期存档、下线登出）时写回数据库。全局层（`@`）不跟随任何一次角色存档，而是在服务器启动时整体读入、在服务器正常关闭时整体写回。

## 例子

```lua
--chrPtr1为账号Test的左边角色的对象index
--chrPtr2为账号Test的右边角色的对象index
--chrPtr3为账号Hello的一个角色的对象index
--chrPtr1与chrPtr2账号相同，chrPtr3为不同账号

function TestField()
  Field.Set(chrPtr1, "LOCALVAR1", "100");
  print(Field.Get(chrPtr1, "LOCALVAR1")); --输出100
  Field.Set(chrPtr1, "#ACCOUNTVAR1", "Hello");
  print(Field.Get(chrPtr2, "#ACCOUNTVAR1")); --输出Hello
  Field.Set(chrPtr2, "@GLOBALVAR1", "EveryOne");
  print(Field.Get(chrPtr3, "@GLOBALVAR1")); --输出EveryOne
  print(Field.Get(chrPtr1, "@GLOBALVAR1")); --输出EveryOne
end
```
