# ProfitabilityTrend


## Fields

| Field                                                                              | Type                                                                               | Required                                                                           | Description                                                                        |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `values`                                                                           | List[*str*]                                                                        | :heavy_check_mark:                                                                 | Revenue values per time bucket, oldest first, in unit currency with two decimals.  |
| `period_change`                                                                    | *Nullable[float]*                                                                  | :heavy_check_mark:                                                                 | Period-over-period % change (current half vs prior half). Null when prior is zero. |