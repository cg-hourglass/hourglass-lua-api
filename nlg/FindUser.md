<!-- Generated. DO NOT EDIT. -->
# FindUser

## NLG.FindUser(CdKey)

### 函数功能

按帐号（CdKey）查找当前在线玩家的对象index。

### 参数说明

- CdKey: [字符串](../appendix/字符串.md) 要查找的帐号/CdKey。

### 返回值

找到时返回对应玩家的对象index；没有匹配的在线玩家返回 -1。

## 参考实例

```lua
local idx = NLG.FindUser("TESTACCOUNT01");
```

### 备注

比较方式只比较前32字节（含NUL语义），按对象顺序找第一个匹配。CdKey本身是ASCII，不受legacy字节截断在字符边界上取整的影响。
