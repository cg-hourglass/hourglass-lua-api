<!-- Generated. DO NOT EDIT. -->
# Charset

## NL.Charset()

### 函数功能

获取当前 gmsv 运行时使用的文本编码。

### 参数说明

无参数。

### 返回值

返回编码名字符串，取值为 "GBK" 或 "BIG5"（大写）。

## 参考实例

```lua
if(NL.Charset() == "BIG5")then
  print("繁体版本");
else
  print("简体版本");
end
```

### 备注

返回值按服务端运行时实际使用的编码决定，并统一为大写；历史版本是按构建时的配置固定下来的。
引擎只在 GBK 与 BIG5 两种编码之间选择，不会返回 "UTF8"。
