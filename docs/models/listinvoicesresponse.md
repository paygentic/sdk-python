# ListInvoicesResponse

List of invoices


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `object`                                                           | [models.ListInvoicesObject](../models/listinvoicesobject.md)       | :heavy_check_mark:                                                 | N/A                                                                |
| `data`                                                             | List[[models.Invoice](../models/invoice.md)]                       | :heavy_check_mark:                                                 | N/A                                                                |
| `pagination`                                                       | [Optional[models.OffsetPagination]](../models/offsetpagination.md) | :heavy_minus_sign:                                                 | Offset-based pagination response.                                  |