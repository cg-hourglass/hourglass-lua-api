<!-- Generated. DO NOT EDIT. -->
# SetData

## Item.SetData(ItemIndex, Dataline, Data)

### 函数功能

设置道具实例的指定信息栏位。

### 参数说明

- ItemIndex: [数值型](../appendix/数值型.md) 目标的道具实例 index。
- Dataline: [数值型](../appendix/数值型.md) 指定的道具实例信息栏位常量，取值范围与 Item.GetData 相同。
- Data: 新的值：整数栏位/工作整数栏位传数值，字符串栏位传字符串。

### 返回值

整数带、工作整数带：返回写入前的旧值（无效道具 index 时返回 -1）。
字符串带：写入成功返回 1，失败（含无效道具 index）返回 0。
Dataline 为负数，或超出三个带的范围：打印告警并返回 nil。

## 参考实例

```lua
local ok = Item.SetData(item, %道具_名字%, "传说之剑");
```

### 备注

工作带的 4000 号栏位是内部防重入用途，写入请求会被直接拒绝（返回 0，
不写入），脚本不应该尝试改写它。
