# CreateGrantRequest


## Fields

| Field                                                                        | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `amount`                                                                     | *float*                                                                      | :heavy_check_mark:                                                           | The number of credits to grant.                                              |
| `effective_at`                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)         | :heavy_minus_sign:                                                           | When the grant becomes effective. Defaults to now.                           |
| `expires_at`                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects)         | :heavy_minus_sign:                                                           | When the grant expires. If omitted, the grant does not expire.               |
| `idempotency_key`                                                            | *str*                                                                        | :heavy_check_mark:                                                           | Idempotency key to prevent duplicate grants. Must be unique per entitlement. |