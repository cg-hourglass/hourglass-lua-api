<!-- Generated. DO NOT EDIT. -->
# CheckAddPages

## Bank.CheckAddPages(CharIndex, Pages)

### 函数功能

Check a paid page grant without changing bank rights.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.
- Pages: [数值型](../appendix/数值型.md) Positive number of additional pages.

### 返回值

Bank status (0 OK, 2 INVALID, 6 BUSY, 8 LIMIT).

## 参考实例

```lua
if Bank.CheckAddPages(player, 1) == 0 then
    Bank.AddPage(player);
end
```

### 备注

Checks the complete grant against char.bank_pages_max, pending/save state and revision overflow. Rejects hidden physical pages beyond effective rights so a paid grant cannot merely catch up. Read-only, no reservation; call and grant in the same serialized callback.
