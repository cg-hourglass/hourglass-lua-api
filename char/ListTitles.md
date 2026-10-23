<!-- Generated. DO NOT EDIT. -->
# ListTitles

## Char.ListTitles(CharIndex)

### 函数功能

Read the player's currently owned formal titles.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player or agent index.

### 返回值

A table with current title ID (or -1) and rows of title IDs and names; nil, STATE for an unavailable or nonplayer character.

## 参考实例

```lua
local titles, err = Char.ListTitles(player);
```

### 备注

Reads the existing owned-title list and title catalog without granting titles or recalculating eligibility. Invalid IDs are filtered and duplicate IDs are collapsed. Names use the normal script text encoding.
IDs are not owned-list slots. Resolve an ID with Char.FindTitleIndex before calling Char.SelectTitle; hide with slot -1. Selection broadcasts the change and fires the title callback. Persist with Char.Save and read back with Char.GetTitle; save failure does not roll back the live selection.
Resting agent bodies are not loaded. Scripts must report this capability as unavailable instead of fabricating an empty list or spawning an agent to read it.
