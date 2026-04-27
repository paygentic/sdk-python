# PriorPeriod

Prior-period comparison data. Present only when comparePriorPeriod=true.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `cost`                                                               | *float*                                                              | :heavy_check_mark:                                                   | N/A                                                                  |
| `change_percent`                                                     | *Nullable[float]*                                                    | :heavy_check_mark:                                                   | Percentage change vs prior period. Null when prior period cost is 0. |