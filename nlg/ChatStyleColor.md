<!-- Generated. DO NOT EDIT. -->
# ChatStyleColor

## NLG.ChatStyleColor(StyleID)

### 函数功能

Resolve a registered style ID to its native chat color wire value.

### 参数说明

- StyleID: [数值型](../appendix/数值型.md) A registered integer style ID, 1..65535.

### 返回值

65536 + StyleID on success; otherwise nil, error.

## 参考实例

```lua
local color = assert(NLG.ChatStyleColor(1));
NLG.TalkToCli(player, -1, "Styled message", color, 0);
```

### 备注

Reserved wire values are 65537..131071. TalkToCli, Say, and TalkToFloor retain their existing signatures and business behavior; registered style colors are downgraded per recipient when not ready. Unknown reserved colors on direct sends become white. Native talk keeps EVENT_TALK and NPC callbacks on the legacy fallback color, preserves the original routing and veto behavior, and stores only fallback_color in PopupNameColor. Existing legacy, MIC, and FM color values are unchanged. Styles do not implement item or pet links.
