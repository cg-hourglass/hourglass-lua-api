<!-- Generated. DO NOT EDIT. -->
# LocalizeUtf8

## NLG.LocalizeUtf8(Text)

### 函数功能

把 UTF-8 文本换成本服务器玩家使用的中文字形：GBK 服务器上把繁体转成简体，Big5 服务器上原样返回。

### 参数说明

- Text: [字符串](../appendix/字符串.md) UTF-8 编码的文本，通常是以 UTF-8 保存的脚本源文件或配置里的中文常量。

### 返回值

UTF-8 字符串；Text 不是字符串时返回 nil。

## 参考实例

```lua
-- 本文件以 UTF-8 保存，用繁体书写
local MSG = NLG.FromUtf8(NLG.LocalizeUtf8("離線擺攤已開啟"));
NLG.SystemMessage(player, MSG); -- GBK 服务器上显示「离线摆摊已开启」
```

### 备注

本函数是本服务端新增的接口，C 版 gmsv 没有。
只改字形、不改编码，结果仍是 UTF-8，要显示还需再经过 NLG.FromUtf8。转换采用 OpenCC 的繁转简词典（先按词、后按字，最长匹配），并把「伺服器」「視窗」等界面用语换成大陆习惯的说法；转换结果在 GBK 里没有的字保留原样。
只用于要显示给玩家的文字。拿来与玩家输入或游戏数据比较的字符串不要转换，或者两边都转换后再比较。
纯 ASCII 文本原样返回。客户端对 profile 脚本的显示文字做同样的转换（GBK 客户端），两边用的是同一份词表。
