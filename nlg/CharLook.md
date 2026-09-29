<!-- Generated. DO NOT EDIT. -->
# CharLook

## NLG.CharLook(CharIndex, Dir)

### 函数功能

让对象转向指定方向（只转身，不移动），并触发朝向两格内的对话联动检查。

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) 目标对象index。
- Dir: [数值型](../appendix/数值型.md) 朝向方向，取值范围 0-7；超出范围的值会被环绕折算到 0-7 之内，不会报错。

### 返回值

目标无效时返回 -1（数值）；否则没有返回值（nil）。

## 参考实例

```lua
NLG.CharLook(_MeIndex, 3); -- 转向南方
```

### 备注

与 WalkMove 的区别：本函数只改变朝向、不移动位置，但底层走的是与 WalkMove 相同的核心处理逻辑，因此同样会广播转身动作，并像真的走了一步一样触发“朝向前方两格”的 Talked 联动检查。
Dir 参数在这里是环绕折算（`((dir%8)+8)%8`），例如传 10 会被当成 2；WalkMove 对越界 Dir 的处理是直接报错，两者不一致，属于各自实现的行为差异。
