# ListProjectedInvoicesResponse

Projected invoices ordered by invoice moment, earliest first


## Fields

| Field                                                                          | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `object`                                                                       | [models.ListProjectedInvoicesObject](../models/listprojectedinvoicesobject.md) | :heavy_check_mark:                                                             | N/A                                                                            |
| `data`                                                                         | List[[models.Invoice](../models/invoice.md)]                                   | :heavy_check_mark:                                                             | N/A                                                                            |
| `pagination`                                                                   | [models.OffsetPagination](../models/offsetpagination.md)                       | :heavy_check_mark:                                                             | Offset-based pagination response.                                              |