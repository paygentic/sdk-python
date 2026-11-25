# CreditPoolLedgerItemizedResponse


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `starting_balance`                                                       | *float*                                                                  | :heavy_check_mark:                                                       | Pool's total balance at the requested window's `from`.                   |
| `ending_balance`                                                         | *float*                                                                  | :heavy_check_mark:                                                       | Pool's total balance at the requested window's `to`.                     |
| `entries`                                                                | List[[models.CreditPoolLedgerEntry](../models/creditpoolledgerentry.md)] | :heavy_check_mark:                                                       | Ledger entries within the requested window, ordered oldest first.        |
| `pagination`                                                             | [models.OffsetPagination](../models/offsetpagination.md)                 | :heavy_check_mark:                                                       | Offset-based pagination response.                                        |