<!-- Generated. DO NOT EDIT. -->
# GetGameTime

## NLG.GetGameTime()

### 函数功能

获取游戏内当前所处的时段。

### 参数说明

无参数。

### 返回值

0＝白天（现实时间7-16点）、1＝黄昏（16-19点）、2＝夜晚（19点-次日4点）、3＝清晨（4-7点）。

## 参考实例

```lua
local t = NLG.GetGameTime();
if t == 2 then
  NLG.SystemMessage(-1, "夜深了。");
end
```

### 备注

本函数不检查参数个数，多传参数也不会报错，纯粹被忽略。
