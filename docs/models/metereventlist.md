# MeterEventList


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `object`                                                                   | [Optional[models.MeterEventListObject]](../models/metereventlistobject.md) | :heavy_minus_sign:                                                         | N/A                                                                        |
| `billable_metric_id`                                                       | *str*                                                                      | :heavy_check_mark:                                                         | Unique identifier for a billable metric                                    |
| `events`                                                                   | List[[models.MeterEvent](../models/meterevent.md)]                         | :heavy_check_mark:                                                         | N/A                                                                        |
| `pagination`                                                               | [models.OffsetPagination](../models/offsetpagination.md)                   | :heavy_check_mark:                                                         | Offset-based pagination response.                                          |