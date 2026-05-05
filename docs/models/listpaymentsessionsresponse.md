# ListPaymentSessionsResponse

List of payment sessions


## Fields

| Field                                                                      | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `object`                                                                   | [models.ListPaymentSessionsObject](../models/listpaymentsessionsobject.md) | :heavy_check_mark:                                                         | N/A                                                                        |
| `data`                                                                     | List[[models.PaymentSession](../models/paymentsession.md)]                 | :heavy_check_mark:                                                         | N/A                                                                        |
| `pagination`                                                               | [models.OffsetPagination](../models/offsetpagination.md)                   | :heavy_check_mark:                                                         | Offset-based pagination response.                                          |