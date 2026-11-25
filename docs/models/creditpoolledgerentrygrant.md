# CreditPoolLedgerEntryGrant

The grant this entry relates to — the grant that funded the pool for `increment`, or the grant whose balance changed for `decrement`, `void`, and `expiration`.


## Fields

| Field                                                                        | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `id`                                                                         | *str*                                                                        | :heavy_check_mark:                                                           | N/A                                                                          |
| `expires_at`                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects)         | :heavy_check_mark:                                                           | The grant's own expiry, or null if it never expires.                         |
| `conversion_rate`                                                            | *str*                                                                        | :heavy_check_mark:                                                           | The pool's pricing-unit conversion rate ($ per credit), as a decimal string. |