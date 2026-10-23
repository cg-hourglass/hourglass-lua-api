<!-- Generated. DO NOT EDIT. -->
# AddPage

## Bank.AddPage(CharIndex)

### 函数功能

Grant one bank page to each asset class.

### 参数说明

- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.

### 返回值

Bank status (0 OK, 2 INVALID, 6 BUSY, 8 LIMIT).

## 参考实例

```lua
local status = Bank.AddPage(player);
```

### 备注

Grants clamp at char.bank_pages_max, retain original rights fields, schedule the existing dump/save behavior, and do not consume cards. Use NL.BankV1 selectors 3/4 for configured paid unlock.
