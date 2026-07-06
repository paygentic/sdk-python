# ReplaceScheduleIntervalsRequest


## Fields

| Field                                                                            | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `intervals`                                                                      | List[[models.Interval](../models/interval.md)]                                   | :heavy_check_mark:                                                               | N/A                                                                              |
| `order_line_item_id`                                                             | *Optional[str]*                                                                  | :heavy_minus_sign:                                                               | When set, scope the wipe to this line's intervals only (per-line cell-edit path) |