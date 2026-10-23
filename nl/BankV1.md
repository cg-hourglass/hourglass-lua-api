<!-- Generated. DO NOT EDIT. -->
# BankV1

## NL.BankV1(Selector, CharIndex, ItemSlot, NextPage, Token)

### 函数功能

Quote or commit a configured bank-page unlock using the existing normal Save.

### 参数说明

- Selector: [数值型](../appendix/数值型.md) 3 quotes, 4 commits. No other selector is supported.
- CharIndex: [数值型](../appendix/数值型.md) Loaded player index.
- ItemSlot: [数值型](../appendix/数值型.md) Actual bag slot holding the configured next-page card.
- NextPage: [数值型](../appendix/数值型.md) Required for selector 4; use the quoted page. [可为空]
- Token: [数值型](../appendix/数值型.md) Required for selector 4; exact integer NUMBER in 1..4294967295, never a string. [可为空]

### 返回值

Selector 3 returns status, token, nextPage, itemID, requiredQuantity. Selector 4 returns status.

## 参考实例

```lua
function UseBankCard(player, itemSlot)
  local status, token, page = NL.BankV1(3, player, itemSlot);
  if status == 0 then
    status = NL.BankV1(4, player, itemSlot, page, token);
  end
  return 0; -- The bank commit owns consumption; never consume twice.
end
```

### 备注

Quotes expire after 60 seconds and new quotes override old quotes.
9 PENDING retains new memory after an uncertain normal Save error; bank requests remain BUSY until an existing later normal Save succeeds, without consuming the card again.
11 RETRY is only returned before mutation when required save dependencies are missing. No automatic business retry is performed.
PENDING is process-local, not journaled, not crash-safe and not relogin recovery. No WAL, receipt or database migration is implemented.
Completion by a later normal Save applies only to a surviving actor. Original disconnect Save failure still tears down the actor and releases assets/account lock; its pending memory is not recoverable afterward.
