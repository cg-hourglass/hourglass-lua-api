<!-- Generated. DO NOT EDIT. -->
# GetCharPointer

## Char.GetCharPointer(CharIndex)

### 函数功能

获取对象的稳定标识。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

对象index本身；对象不可用时返回 -1。

## 参考实例

```lua
local Token = Char.GetCharPointer(Player);
if Token ~= -1 then
    Char.GetData(Token, %对象_名字%);
end
```

### 备注

本服务端返回的就是对象index本身，务必注意这与历史版本的差异：旧版返回的是角色数据在进程里的内存地址。
对象index正是整套 Lua 接口到处传递的令牌，所以“取出来做相等比较”“再传回其他 Char.* 函数”
这类脚本写法照常工作；但任何把返回值当内存地址、拿去做偏移或传给其他原生接口的脚本都不再成立。
