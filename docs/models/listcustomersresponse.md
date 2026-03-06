# ListCustomersResponse

List of customers retrieved successfully


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `object`                                                       | [models.ListCustomersObject](../models/listcustomersobject.md) | :heavy_check_mark:                                             | N/A                                                            |
| `data`                                                         | List[[models.Customer](../models/customer.md)]                 | :heavy_check_mark:                                             | N/A                                                            |
| `pagination`                                                   | [models.OffsetPagination](../models/offsetpagination.md)       | :heavy_check_mark:                                             | Offset-based pagination response.                              |