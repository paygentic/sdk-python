# UsageResponse


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `object`                                                                 | [Optional[models.UsageResponseObject]](../models/usageresponseobject.md) | :heavy_minus_sign:                                                       | N/A                                                                      |
| `billable_metric_id`                                                     | *str*                                                                    | :heavy_check_mark:                                                       | Unique identifier for a billable metric                                  |
| `total_value`                                                            | *float*                                                                  | :heavy_check_mark:                                                       | Total aggregated value across the query window                           |
| `windowed_values`                                                        | List[[models.WindowedValue](../models/windowedvalue.md)]                 | :heavy_minus_sign:                                                       | Time-bucketed values. Only present when windowSize is specified.         |
| `grouped_values`                                                         | List[[models.GroupedValue](../models/groupedvalue.md)]                   | :heavy_minus_sign:                                                       | Dimension-grouped values. Only present when groupBy is specified.        |