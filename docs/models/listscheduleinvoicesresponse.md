# ListScheduleInvoicesResponse

List of staged invoices


## Fields

| Field                                                                        | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `object`                                                                     | [models.ListScheduleInvoicesObject](../models/listscheduleinvoicesobject.md) | :heavy_check_mark:                                                           | N/A                                                                          |
| `data`                                                                       | List[[models.ScheduleInvoice](../models/scheduleinvoice.md)]                 | :heavy_check_mark:                                                           | N/A                                                                          |
| `pagination`                                                                 | [models.OffsetPagination](../models/offsetpagination.md)                     | :heavy_check_mark:                                                           | Offset-based pagination response.                                            |