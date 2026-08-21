<!-- Generated. DO NOT EDIT. -->
# FindNpcByName

## NLG.FindNpcByName(Name)

### 函数功能

按名字查找 NPC 类对象。

### 参数说明

- Name: [字符串](../appendix/字符串.md) 要查找的NPC名字，需精确匹配。

### 返回值

目标NPC的对象index，只返回第一个匹配结果；没有找到返回 -1。

## 参考实例

```lua
local npcIdx = NLG.FindNpcByName("商店老板");
```

### 备注

扫描范围与规则同 FindNpcByPos。比较对象是角色的名字字段，本服务端以 UTF-8 存储，因此中文名字可以正常匹配；在文本编码统一之前，这里曾经只能匹配 ASCII 名字。
