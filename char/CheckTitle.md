<!-- Generated. DO NOT EDIT. -->
# CheckTitle

## Char.CheckTitle(CharIndex)

### 函数功能

重新检定玩家的全部称号解锁条件。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标的对象index。

### 返回值

有称号发生变化返回 1，没有变化返回 0；对象不是玩家或指针无效时返回 -1。

## 参考实例

```lua
Char.CheckTitle(Player);
```

### 备注

有称号发生变化时会顺带把新的称号列表下发给客户端。
在脚本里发完称号相关的道具或旗标之后调用它，可以让“阿蒙”这类条件称号立刻生效。
