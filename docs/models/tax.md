# Tax

Tax reconciliation metadata (only present when plan has taxEnabled)


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `actual_tax`                                                         | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Actual tax calculated (in atomic units)                              |
| `adjustment_applied`                                                 | *Optional[bool]*                                                     | :heavy_minus_sign:                                                   | Whether wallet adjustment was applied during tax reconciliation      |
| `adjustment_needed`                                                  | *Optional[bool]*                                                     | :heavy_minus_sign:                                                   | Whether wallet adjustment is needed (difference >= $0.01)            |
| `difference`                                                         | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Difference between actual and estimated (in atomic units)            |
| `estimated_tax`                                                      | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Tax estimated from subscription rate (in atomic units)               |
| `reconciled`                                                         | *Optional[bool]*                                                     | :heavy_minus_sign:                                                   | Whether reconciliation was performed                                 |
| `reconciled_at`                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | When reconciliation occurred                                         |