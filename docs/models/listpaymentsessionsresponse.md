# ListPaymentSessionsResponse

List of payments


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `object`                                                                   | [models.ListPaymentSessionsObject](../models/listpaymentsessionsobject.md) | :heavy_check_mark:                                                         | N/A                                                                        |
| `data`                                                                     | List[[models.Payment](../models/payment.md)]                               | :heavy_check_mark:                                                         | N/A                                                                        |
| `pagination`                                                               | [models.OffsetPagination](../models/offsetpagination.md)                   | :heavy_check_mark:                                                         | Offset-based pagination response.                                          |