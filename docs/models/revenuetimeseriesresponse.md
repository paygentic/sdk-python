# RevenueTimeSeriesResponse


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `object`                                                         | *Literal["revenue_time_series"]*                                 | :heavy_check_mark:                                               | Object type identifier                                           |
| `buckets`                                                        | List[[models.RevenueTimeBucket](../models/revenuetimebucket.md)] | :heavy_check_mark:                                               | Time-bucketed revenue data                                       |