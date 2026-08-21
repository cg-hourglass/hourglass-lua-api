<!-- Generated. DO NOT EDIT. -->
# Snapshot

## Debug.Snapshot()

### 函数功能

生成当前 Lua 状态的内存快照（本版本为占位实现），供内存诊断参考。

### 参数说明

无参数。

### 返回值

一张空 table。

## 参考实例

```lua
local snap = Debug.Snapshot();
```

### 备注

本版本该函数固定返回一张空 table，不提供 table/thread/userdata/function 间的引用关系快照；若脚本依赖返回 table 的具体内容（而不只是“调用不报错”），需要注意这一点。真正的内存诊断请使用服务端提供的进程级诊断能力。
